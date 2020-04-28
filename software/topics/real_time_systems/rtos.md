RTOS
====


### Thread packages

- Simple task-based execution model
- Libraries instead of kernel calls
- preemptive or cooperative
- Usually no MMU or virtual memory

### Microkernels

- basic functionality inside kernel
- message passing instead of kernel calls
- Other functionality as separate OS services
- memory protection of address space
- can support virtual memory

### Monothlithic

- Device drivers can run in privileged mode
- Real-time applications in user mode
- Often mixture of real-time and non real-time
