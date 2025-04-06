# Dummy modules compilation:
IIO dummy driver setup was successfully completed by enabling the required kernel configs and compiling the necessary modules. A dummy device was created under configfs to validate events, buffers, and event generation functionality.
## Task 1
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

## Task 2
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

## Task 3
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
