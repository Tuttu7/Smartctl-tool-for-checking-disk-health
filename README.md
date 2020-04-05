> Smartctl (Self-Monitoring, Analysis and Reporting Technology) is a command line utility. It is useful on physical Linux servers where smart disks can be checked for errors and extract info regarding the disks. 


To install it on the ubuntu based systems :

```
apt-get install smartmontools
```


> Check Whether Smart Capability is enabled or not for the disk

```
~# smartctl -i /dev/sda
smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.10.0-28-generic] (local build)
Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Device Model:     ST1000LM048-2E7172
Serial Number:    WL1JZGBL
LU WWN Device Id: 5 000c50 0be14e033
Firmware Version: SDM1
User Capacity:    1,000,204,886,016 bytes [1.00 TB]
Sector Sizes:     512 bytes logical, 4096 bytes physical
Rotation Rate:    5400 rpm
Form Factor:      2.5 inches
Device is:        Not in smartctl database [for details use: -P showall]
ATA Version is:   ACS-3 T13/2161-D revision 3b
SATA Version is:  SATA 3.1, 6.0 Gb/s (current: 6.0 Gb/s)
Local Time is:    Sun Apr  5 16:46:43 2020 IST
SMART support is: Available - device has SMART capability.
SMART support is: Enabled
```


> Display Overall health of the Disk :

```
# smartctl -H /dev/sda
smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.10.0-28-generic] (local build)
Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF READ SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED
```


> Test Hard drive using long & short option

> Long test 

```
~# smartctl --test=long /dev/sda
smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.10.0-28-generic] (local build)
Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF OFFLINE IMMEDIATE AND SELF-TEST SECTION ===
Sending command: "Execute SMART Extended self-test routine immediately in off-line mode".
Drive command "Execute SMART Extended self-test routine immediately in off-line mode" successful.
Testing has begun.
Please wait 176 minutes for test to complete.
Test will complete after Sun Apr  5 19:56:29 2020

Use smartctl -X to abort test.
```

> Short Test

```
smartctl --test=short /dev/sda > test.txt
```

Short test will take maximum 2 minutes whereas in long test there is no time restriction because it read & verify every segment of the entire disk.

> To View Drive’s Self Test result

```
# smartctl -l selftest /dev/sda
smartctl 6.5 2016-01-24 r4214 [x86_64-linux-4.10.0-28-generic] (local build)
Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF READ SMART DATA SECTION ===
SMART Self-test log structure revision number 1
Num  Test_Description    Status                  Remaining  LifeTime(hours)  LBA_of_first_error
# 1  Short offline       Completed without error       00%       152         -
# 2  Extended offline    Aborted by host               90%       152         -
```
