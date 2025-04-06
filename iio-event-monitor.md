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
