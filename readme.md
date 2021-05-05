# Test of ecmc on ESS pico zed platform

## Connect to unit
Connect as normal with ssh, user iocuser

```
ssh iocuser@192.168.86.77

```

## Start ethercat service

```
localhost:~$ sudo systemctl start ethercat
localhost:~$ lsmod | grep ec_
ec_generic             16384  0
ec_master             327680  1 ec_generic

```

## Connect slaves and check if available
```
localhost:~$ ethercat slaves
 0  0:0   PREOP  +  EK1100 EtherCAT Coupler (2A E-Bus)
 1  0:1   PREOP  +  EL1018 8K. Dig. Eingang 24V, 10�s
 2  0:2   PREOP  +  EL2808 8K. Dig. Ausgang 24V, 0.5A
 3  0:3   PREOP  +  EL5101 1K. Inc. Encoder 5V
 4  0:4   PREOP  +  EL5101 1K. Inc. Encoder 5V
 5  0:5   PREOP  +  EL9505 Netzteilklemme 5V
 6  0:6   PREOP  +  EL1252-0050 2K. Fast Dig. Eingang 5V, 1�s, DC Latch
 7  0:7   PREOP  +  EL9410 E-Bus Netzteilklemme (Diagnose)
 8  0:8   PREOP  +  EL7037 1K. Schrittmotor-Endstufe (24V, 1.5A)
 9  0:9   PREOP  +  EL7037 1K. Schrittmotor-Endstufe (24V, 1.5A)
10  0:10  PREOP  +  EL7411 BLDC Terminal with incremental encoder/Hall, 50 V DC, 4.

```

## Change prio on ecmc_rt thread
Example: change prio to 80 and fifo for pid 1670 (ecmc_rt in this case)
```
localhost:~$ chrt -f --pid 80 1670
```
