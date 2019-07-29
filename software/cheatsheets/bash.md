Bash
====


### Add suffix to a file
Expanding with `${f%.json}` expands filename without the `.json` filename
```
for f in `ls | grep XXX*.json`; do
    mv "$f" "${f%.json}_v1.json"
done
```
