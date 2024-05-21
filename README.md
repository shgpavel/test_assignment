# test_task

**To build**\
Just run `make` at src/ directory

**To install**
```shell
#  insmod $(PWD)/dmp.ko
```

**To test**
```shell
First create the example device and proxy device by doing

#  dmsetup create zero1 --table "0 _SIZE_ zero" # You should define the _SIZE_
#  dmsetup create dmp1  --table "0 _SIZE_ dmp /dev/mapper/zero1"

Then make sure everything was successfully created with
#  dmsetup ls
Or
$  ls -al /dev/mapper/*

After try to read and write to a proxy device
#  dd if=/dev/random of=/dev/mapper/dmp1 bs=4k count=1
#  dd of=/dev/null if=/dev/mapper/dmp1 bs=4k count=1

For statistics
#  cat /sys/module/dmp/stat/volumes
```

**To remove**
```shell
First you need to remove created devices, so run
#  dmsetup remove dmp1 zero1

Then unload the module
#  rmmod dmp

And clean src directory
make clean
```
