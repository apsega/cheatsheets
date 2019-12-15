# hpssacli

## common commands

### Show configuration

```bash
hpssacli ctrl all show config
```

### Controller status

```bash
hpssacli ctrl all show status
```

### Show detailed controller information for all controllers

```bash
hpssacli ctrl all show detail
```

### Show detailed controller information for controller in slot 3

```bash
hpssacli ctrl slot=3 show detail
```

### Create New RAID 0 Logical Drive

```bash
/opt/hp/hpssacli/bin/hpssacli ctrl slot=0 create type=ld drives=1I:1:2 raid=0
```

### Show detailed Logical Volume information

```bash
hpssacli ctrl slot=3 ld 13 show
```

## workflow

### Get HP controller slot

```bash
hpssacli ctrl all show config
```

### Let's make all drives in that slot raid 0

```bash
SLOT=3;for (( i = 1; i <= 8; i++ )); do hpssacli ctrl slot=$SLOT create type=ld drives=1I:1:$i raid=0; done
```

### Information about our current raid status

```bash
SLOT=3;hpssacli ctrl all show detail | grep "Cache Ratio" && for (( i = 1; i <= 19; i++ )); do hpssacli ctrl slot=$SLOT ld $i show | grep array && hpssacli ctrl slot=$SLOT ld $i show | grep -i caching && hpssacli ctrl slot=$SLOT ld $i show | grep "LD Acceleration Method" ; done
```

### SSD Smart path should be enabled on SSD disks

```bash
hpssacli ctrl slot=1 array A modify ssdsmartpath=enable
hpssacli ctrl slot=1 array N modify ssdsmartpath=enable
hpssacli ctrl slot=1 array O modify ssdsmartpath=enable
hpssacli ctrl slot=1 array P modify ssdsmartpath=enable
hpssacli ctrl slot=1 array Q modify ssdsmartpath=enable
hpssacli ctrl slot=1 array R modify ssdsmartpath=enable
```

### Non-ssd disks should have cache enabled

```bash
for (( i = 2; i <= 18; i++ )); do hpssacli ctrl slot=1 logicaldrive $i modify arrayaccelerator=enable; done
```

### Change cache settings

```bash
hpssacli ctrl slot=3 modify cacheratio=10/90
```

```bash
SLOT=3;hpssacli ctrl all show detail | grep "Cache Ratio" && for (( i = 1; i <= 19; i++ )); do hpssacli ctrl slot=$SLOT ld $i show | grep array && hpssacli ctrl slot=$SLOT ld $i show | grep -i caching && hpssacli ctrl slot=$SLOT ld $i show | grep "LD Acceleration Method" ; done
```

## Random

```bash
for (( i = 1; i <= 8; i++ )); do hpssacli ctrl slot=3 create type=ld drives=1I:1:$i raid=0; done
for (( i = 2; i <= 13; i++ )); do hpssacli ctrl slot=3 logicaldrive $i modify arrayaccelerator=enable; done
hpssacli ctrl all show detail | grep "Cache Ratio" && for (( i = 1; i <= 13; i++ )); do hpssacli ctrl slot=3 ld $i show | grep array && hpssacli ctrl slot=3 ld $i show | grep -i caching && hpssacli ctrl slot=3 ld $i show | grep "LD Acceleration Method" ; done
hpssacli ctrl slot=3 array A modify cacheratio=10/90
```

```bash
for (( i = 2; i <= 18; i++ )); do hpssacli ctrl slot=1 logicaldrive $i modify arrayaccelerator=disable; done
```

[Back to main](../README.md)