# iio-tasks
An environment was set up using QEMU and libvirt specifically for the development and testing of Linux IIO kernel modules on an ARM64 virtual machine. The IIO kernel repository was shallowly cloned from the testing branch to quickly access recent changes with minimal download overhead. This repository was then used to generate a kernel configuration compatible with the one in which the IIO drivers were written, ensuring proper integration and testing. This kernel configuration was then installed on the VM. 

## Detailed Outputs
For full logs and outputs, see: 
- [Dummy Modules Setup](/dummy-modules-compilation.txt)  
- [IIO Event Monitor](/iio-event-monitor.txt)  
- [Generic Buffer Testing](/generic-buffer.txt)

## Dummy modules compilation:
IIO dummy driver setup was successfully completed by enabling the required kernel configs and compiling the necessary modules. A dummy device was created under configfs to validate events, buffers, and event generation functionality.
### Task 1
```
$ grep CONFIG_IIO ${IIO_TREE}/.config
CONFIG_IIO=y
CONFIG_IIO_BUFFER=y
CONFIG_IIO_BUFFER_CB=m
CONFIG_IIO_KFIFO_BUF=m
CONFIG_IIO_TRIGGERED_BUFFER=m
CONFIG_IIO_CONFIGFS=m
CONFIG_IIO_TRIGGER=y
CONFIG_IIO_CONSUMERS_PER_TRIGGER=2
CONFIG_IIO_SW_DEVICE=m
CONFIG_IIO_SW_TRIGGER=m
CONFIG_IIO_DUMMY_EVGEN=m
CONFIG_IIO_SIMPLE_DUMMY=m
CONFIG_IIO_SIMPLE_DUMMY_EVENTS=y
CONFIG_IIO_SIMPLE_DUMMY_BUFFER=y
```

### Task 2
Loaded Modules
```
root@localhost:~# lsmod | grep dummy
iio_dummy              12288  0
industrialio_triggered_buffer    12288  1 iio_dummy
industrialio_sw_device    12288  1 iio_dummy
iio_dummy_evgen        16384  1 iio_dummy
```
Dummy Device in ConfigFS
```
root@localhost:~# ls -l /config/iio/devices/dummy/
total 0
drwxr-xr-x 2 root root 0 Apr  5 19:47 my_dummy_device
```
Created IIO Device Sysfs Interface
```
root@localhost:~# ls -l /sys/bus/iio/devices/iio:device0/
total 0
drwxr-xr-x 2 root root    0 Apr  5 19:48 buffer
-rw-r--r-- 1 root root 4096 Apr  5 19:48 current_timestamp_clock
-r--r--r-- 1 root root 4096 Apr  5 19:48 dev
drwxr-xr-x 2 root root    0 Apr  5 19:48 events
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_calibbias
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_calibscale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_activity_running_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_activity_walking_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_sampling_frequency
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_calibheight
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_en
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage-voltage_scale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_offset
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_scale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage1-voltage2_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage3-voltage4_raw
-r--r--r-- 1 root root 4096 Apr  5 19:47 name
-rw-r--r-- 1 root root 4096 Apr  5 19:48 out_voltage0_raw
drwxr-xr-x 2 root root    0 Apr  5 19:48 power
drwxr-xr-x 2 root root    0 Apr  5 19:48 scan_elements
lrwxrwxrwx 1 root root    0 Apr  5 19:48 subsystem -> ../../bus/iio
drwxr-xr-x 2 root root    0 Apr  5 19:48 trigger
-rw-r--r-- 1 root root 4096 Apr  5 19:47 uevent
```
Event Generator Presence
```
root@localhost:~# ls -l /sys/bus/iio/devices/iio_evgen/
total 0
--w------- 1 root root 4096 Apr  5 19:53 poke_ev0
--w------- 1 root root 4096 Apr  5 19:53 poke_ev1
--w------- 1 root root 4096 Apr  5 19:53 poke_ev2
--w------- 1 root root 4096 Apr  5 19:53 poke_ev3
--w------- 1 root root 4096 Apr  5 19:53 poke_ev4
--w------- 1 root root 4096 Apr  5 19:53 poke_ev5
--w------- 1 root root 4096 Apr  5 19:53 poke_ev6
--w------- 1 root root 4096 Apr  5 19:53 poke_ev7
--w------- 1 root root 4096 Apr  5 19:53 poke_ev8
--w------- 1 root root 4096 Apr  5 19:53 poke_ev9
drwxr-xr-x 2 root root    0 Apr  5 19:53 power
lrwxrwxrwx 1 root root    0 Apr  5 19:53 subsystem -> ../../bus/iio
-rw-r--r-- 1 root root 4096 Apr  5 19:39 uevent
```

### Task 3
IIO Device Directory
```
root@localhost:~# ls -l /sys/bus/iio/devices/iio:device0/
total 0
drwxr-xr-x 2 root root    0 Apr  5 19:48 buffer
drwxr-xr-x 2 root root    0 Apr  5 19:48 buffer0
-rw-r--r-- 1 root root 4096 Apr  5 19:48 current_timestamp_clock
-r--r--r-- 1 root root 4096 Apr  5 19:48 dev
drwxr-xr-x 2 root root    0 Apr  5 19:48 events
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_calibbias
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_calibscale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_accel_x_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_activity_running_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_activity_walking_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_magn_scale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_magn_x_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_magn_y_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_magn_z_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_sampling_frequency
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_calibheight
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_en
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_steps_input
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage-voltage_scale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_offset
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage0_scale
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage1-voltage2_raw
-rw-r--r-- 1 root root 4096 Apr  5 19:48 in_voltage3-voltage4_raw
-r--r--r-- 1 root root 4096 Apr  5 19:47 name
-rw-r--r-- 1 root root 4096 Apr  5 19:48 out_voltage0_raw
drwxr-xr-x 2 root root    0 Apr  5 19:48 power
drwxr-xr-x 2 root root    0 Apr  5 19:48 scan_elements
lrwxrwxrwx 1 root root    0 Apr  5 19:48 subsystem -> ../../bus/iio
drwxr-xr-x 2 root root    0 Apr  5 19:48 trigger
-rw-r--r-- 1 root root 4096 Apr  5 19:47 uevent
```
Scan Elements
```
root@localhost:~# ls -l /sys/bus/iio/devices/iio:device0/scan_elements
total 0
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_accel_x_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_accel_x_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_accel_x_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_magn_x_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_x_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_x_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_magn_y_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_y_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_y_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_magn_z_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_z_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_magn_z_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_timestamp_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_timestamp_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_timestamp_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_voltage0_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage0_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage0_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_voltage1-voltage2_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage1-voltage2_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage1-voltage2_type
-rw-r--r-- 1 root root 4096 Apr  5 19:59 in_voltage3-voltage4_en
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage3-voltage4_index
-r--r--r-- 1 root root 4096 Apr  5 19:59 in_voltage3-voltage4_type
```
Patch

## IIO event monitor
### Task 4
IIO Event Monitor Compilation - The `iio_event_monitor` executable will be created. It can be used to read events from iio devices.  
```
$ make -C ${IIO_TREE}/tools/iio/ iio_event_monitor
make: Entering directory '/home/lk_dev/iio/tools/iio'
mkdir -p include/linux/iio 2>&1 || true
ln -sf /home/lk_dev/iio/tools/iio/../../include/uapi/linux/iio/buffer.h include/linux/iio
ln -sf /home/lk_dev/iio/tools/iio/../../include/uapi/linux/iio/events.h include/linux/iio
ln -sf /home/lk_dev/iio/tools/iio/../../include/uapi/linux/iio/types.h include/linux/iio
make[1]: Entering directory '/home/lk_dev/iio/tools/iio'
  CC      iio_utils.o
  LD      iio_utils-in.o
make[1]: Leaving directory '/home/lk_dev/iio/tools/iio'
make[1]: Entering directory '/home/lk_dev/iio/tools/iio'
  CC      iio_event_monitor.o
  LD      iio_event_monitor-in.o
make[1]: Leaving directory '/home/lk_dev/iio/tools/iio'
  LINK    iio_event_monitor
make: Leaving directory '/home/lk_dev/iio/tools/iio'
```

### Task 5 - Reading events using `iio_event_monitor`
Execute `iio_event_monitor` without arguments
```
root@localhost:~# ./iio_event_monitor 
Usage: iio_event_monitor [options] <device_name>
Listen and display events from IIO devices
  -a         Auto-activate all available events
```

Read events from iio_dummy module
```
root@localhost:~# ./iio_event_monitor /dev/iio\:device0
```

Generate Events from dummy event generator. Execute this command in a different terminal
```
$ echo 1 > /sys/bus/iio/devices/iio_evgen/poke_ev0
```
You will see such an output in the terminal executing `./iio_event_monitor /dev/iio\:device0`
```
Event: time: 1743933861206532857, type: activity(running), channel: 0, evtype: thresh, direction: rising
```

## Generic Buffer
### Task 6
First we need to enable hrtimer using `make menuconfig`. Follow this path: 
`Device Drivers -> Industrial I/O support -> Triggers-standalone -> High resolution timer trigger`
Then use moddules_prepare to prepare kernel build system for compiling the modules. Then compile the `drivers/iio/trigger` directory. Then copy the iio-trig-hrtimer.ko to the VM and insmod it. Make sure that configfs is mounted on /config. 

Create hrtimer software trigger named t1.
```
root@localhost:~# mkdir /config/iio/triggers/hrtimer/t1
```

The trigger resides in the `/sys/bus/iio/devices` directory. Use theses commands to verif:
```
root@localhost:~# ls /sys/bus/iio/devices/
iio_evgen  trigger0


root@localhost:~# ls /sys/bus/iio/devices/trigger0
name  power  sampling_frequency  subsystem  uevent
```

### Task 7 -Read samples from buffer generated by the iio_dummy module
Compile `iio_generic_buffer.c` from `tools/iio`
```
$ make -C ${IIO_TREE}/tools/iio/ iio_generic_buffer
```

Copy `iio_generic_buffer` to VM.
```
$ scp ${IIO_TREE}/tools/iio/iio_generic_buffer root@<VM-IP>:/root/
```

Then the command `./iio_generic_buffer -h` was executed. Then reading the usage I decided to use the following options:
1. -a : Auto-activate all available channels
2. -n : To mention the iio_dummy device
3. -t : To include the hrtimer t1
4. -c : To control the number of reads
```
root@localhost:~# ./iio_generic_buffer -a -n my_dummy_device -t t1 -c 5
iio device number being used is 0
iio trigger number being used is 0
Enabling all channels
.
.
/sys/bus/iio/devices/iio:device0 t1
0.018662 -0.000044 -0.000003 344.000000 0 0.067140 0.032392 0.093944 
0.018662 -0.000044 -0.000003 344.000000 0 0.127440 0.032702 0.093944 
0.018662 -0.000044 -0.000003 344.000000 0 0.097726 0.033016 0.093944 
0.018662 -0.000044 -0.000003 344.000000 0 0.115968 0.033340 0.093944 
0.018662 -0.000044 -0.000003 344.000000 0 0.125850 0.033622 0.093944 
Disabling all channels
.
.
```
We can enable specific channels using `/sys/bus/iio/devices/iio:device0/scan_elements/` directory
