Clang AST matchers
------------------

### References
- [LibTooling docs](https://clang.llvm.org/docs/LibASTMatchersReference.html)

### Strategy

My strategy when writing matchers is to start by dumping the ast:
```
clang -Xclang -ast-dump -fsyntax-only file.cpp
```
With the ast I find the top level node I want, then open `file.cpp` in `clang-query` and create a matcher from the ast i dumped
some examples below.

From there I can write a matcher in code and run my tool in a debugger with a breakpoint on my match handler. In the debugger I can call
`dump` on the object and see a more detailed ast of that match and refine my matcher until I only get the case I'm looking for. 

### Examples
Given:

```cpp
class ExampleRunner {
public:
    ExampleRunner(){
        _eventClient = std::make_unique<Example::EventClient>(_cfg.EventNames.ExampleEvent);
    }
    void run(int time) {
        auto outOfTimeEvent = Example::EventClient("OutOfTime");

        if (time > 10) {
            outOfTimeEvent.raise();
        }
        else
        {
            _eventClient->raise();
        }
    }
private:
    std::unique_ptr<Example::EventClient> _eventClient{nullptr};
    Example::Cfg::RunnerApi _cfg;
}
```
--------
To match on top level namespace:
```
nestedNameSpecifierLoc(hasPrefix(loc(specificesNamespace(hasName("Example")))))
```
matches:
```
Example::Cfg::RunnerApi _cfg;
```
but only the `Example` part. How to match `Cfg`

--------

To match `make_unique` was called with our example class as the template declaration:
```
callExpr(callee(functionDecl(hasName("make_unique"), hasAnyTemplateArgument(refersToType(hasDeclaration(namedDecl(hasName("Example::EventClient"))))))))
```

#### Tool Example

Here is an example of a clang tool to match against the class above
```cpp
#include "clang/ASTMatchers/ASTMatchers.h"
#include "clang/ASTMatchers/ASTMatchFinder.h"
#include "clang/Frontend/FrontendActions.h"
#include "clang/Tooling/CommonOptionsParser.h"
#include "clang/Tooling/Tooling.h"

// Declares llvm::cl::extrahelp.
#include "llvm/Support/CommandLine.h"

using namespace clang;
using namespace clang::ast_matchers;
using namespace clang::tooling;
using namespace llvm;

StatementMatcher EventRaiseMatcher = memberExpr(
  hasObjectExpression(hasType(asString("Example::EventClient"))),
  member(functionDecl(hasName("raise"))),
  hasDescendant(memberExpr(member(hasType(asString("Example::EventClient")))).bind("client")),
).bind("raise");
class EventRaiseHandler : public MatchFinder::MatchCallback
{
public:
  virtual void run(const MatchFinder::MatchResult &Result)
  {
    auto *hcr = Result.Nodes.getNodeAs<clang::MemberExpr>("raise");
    auto *client = Result.Nodes.getNodeAs<clang::MemberExpr>("client");
    if (!hcr || !client) return;
    auto clietName = client->getMemberDecl()->getQualifiedNameAsString();
  }

};
// Apply a custom category to all command-line options so that they are the
// only ones displayed.
static llvm::cl::OptionCategory MyToolCategory("my-tool options");

// CommonOptionsParser declares HelpMessage with a description of the common
// command-line options related to the compilation database and input files.
// It's nice to have this help message in all tools.
static cl::extrahelp CommonHelp(CommonOptionsParser::HelpMessage);

// A help message for this specific tool can be added afterwards.
static cl::extrahelp MoreHelp("\nMore help text...\n");

int main(int argc, const char **argv)
{
  CommonOptionsParser OptionsParser(argc, argv, MyToolCategory);
  ClangTool Tool(OptionsParser.getCompilations(),
                 OptionsParser.getSourcePathList());

  MatchFinder finder;
  EventRaiseHandler erHandler;
  finder.addMatcher(EventRaiseMatcher, &erHandler);

  return Tool.run(newFrontendActionFactory(&finder).get());
}

```


