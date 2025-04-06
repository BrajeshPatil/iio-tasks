# iio-tasks
An environment was set up using QEMU and libvirt specifically for the development and testing of Linux IIO kernel modules on an ARM64 virtual machine. The IIO kernel repository was shallowly cloned from the testing branch to quickly access recent changes with minimal download overhead. This repository was then used to generate a kernel configuration compatible with the one in which the IIO drivers were written, ensuring proper integration and testing. This kernel configuration was then installed on the VM. 

## Detailed Outputs
For full logs and outputs, see: 
- [Dummy Modules Setup](/dummy-modules-compilation.txt)  
- [IIO Event Monitor](/iio-event-monitor.txt)  
- [Generic Buffer Testing](/generic-buffer.txt)
