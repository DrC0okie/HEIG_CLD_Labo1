# HEIG_CLD_Labo1

**Group U : A. David, T.Van Hove**

## Introduction

This document describes the successive steps necessary to successfully complete laboratory #1 of the CLD course. It will also allow our group to answer the various questions asked in the lab instructions.

The objectives of this lab is to gain experience with an Infrastructure-as-a-Service. We are going to use  AWS to create a service from scratch and measure its performance and resource consumption. Finally we will estimate the price tag of such a service using AWS.

## Part 1 & 2 : Setting up a virtual server

In this part, we are going to configure and launch a virtual ubuntu server with Amazon Elastic Compute Cloud (Amazon EC2). 

#### Creating key pairs

To later connect to our instance with SSH, we need to generate a key pair for the authentication. Here's how to proceed:

1. From the left menu on the EC2 dashboard, go to to "Network & Security" -> "Key Pairs".
2. Click on "Create key pair" on the top right corner.
3. Select RSA or ED25519 encryption
   1. Note that ED25519 work only with mac or linux **instances**
4. Depending of the SSH client on your local machine:
   1. With OpenSSH select .pem file
   2. With PuTTY .ppk file
5. Click on "Create key pair"

![Menu to create a key pair](img/keyPair.png)

The private key file will automatically be downloaded in you browser.

If you are using a linux/mac OS on your local machine, yo will need do change the access rights of the key file:

```bash
chmod 400 yourFileName.pem
```

#### Setting up the security groups

We will set the security group to allow any incoming SSH connection.

1. From the left menu on the EC2 dashboard, go to to "Network & Security" -> "Security groups".
2. Click on "Create security group" on the top right corner.
3. Type a name and eventually a description for the security group.
4. Add an inbound rule by clicking on the "Add rule" button.
5. Select "SSH" from the "Type" drop down menu.
6. Select "Anywhere-IPv4" from the "Source type" drop down menu.
7. Add an optionnal description
8. Click on the "Add rule" button.
9. Click on "Create security group" button on the bottom right of the page.

![Create a security group](img/CreateSecurityGroup.png)

Now we have the 2 mandatory components to create and access our future instance.

#### Create and launch an Amazon EC2 instance

Now we will create our instance.

1. From the left menu on the EC2 dashboard, go to to "Instances" -> "Instances".

2. Click on "Launch instances" on the top right corner.

3. Give a name to your instance

4. Select the OS image you want to use (In this context we'll be using ubuntu).

5. Select the version of the specific image you want in the drop down menu (ubuntu Server LTS 18.04 SSD Volume type)

6. Select the CPU architecture of you OS from the drop down menu

7. You can choose the instance type from the drop down menu. It will define the performance level of the virtualized instance with more or less CPU threads, memory and network performance. In this context we are using the t2.micro instance type :
   |   Type   | vCPU | Architecture | Memory | Network perf |
   | :------: | :--: | :----------: | :----: | :----------: |
   | t2.micro |  1   |    x86_64    |  1 GB  | Low/Moderate |

8. In the Key pair section, select the Key pair you configured [previously](#Creating-key-pairs) from the drop down list.

9. In the Network settings section, select the existing security group you configured [previously](#Setting-up-the-security-groups) from the drop down list

10. You can configure the number of volumes, the amount and type of storage memory you want to use in the "Configure storage" section. We have chosen 8GB genera purpose SSD (gp2) that was selected by default.

11. It is possible to configure advanced parameters such as shutdown behavior, or credit specification. We left this section configures by default.

12. Finally, click on the "Launch instance" button at the bottom of the page

Note: the instance will quickly start (within 1-10 seconds), however, when the instance has started for the first time, some status check will be performed. During those check, it is possible to be unable to connect to your instance with SSH. In this case, just wait until the status checks are passed.

#### Connection to the running instance

Once the instance is running

## Part 3 : Install a web application

## Part 4 : Create volumes and use snapshots

## Part 5 Performance analysis

## Part 6 : Resource consumption and pricing

## Conclusion



task2 commands on the remote machine:



id:
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),108(lxd),114(netdev)



date:

Thu Feb 23 16:54:02 UTC 2023



lsb_release -a:

No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.6 LTS
Release:        18.04
Codename:       bionic



sudo lshw -short:

H/W path    Device  Class      Description
==========================================
                    system     HVM domU
/0                  bus        Motherboard
/0/0                memory     96KiB BIOS
/0/401              processor  Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
/0/1000             memory     1GiB System Memory
/0/1000/0           memory     1GiB DIMM RAM
/0/100              bridge     440FX - 82441FX PMC [Natoma]
/0/100/1            bridge     82371SB PIIX3 ISA [Natoma/Triton II]
/0/100/1.1          storage    82371SB PIIX3 IDE [Natoma/Triton II]
/0/100/1.3          bridge     82371AB/EB/MB PIIX4 ACPI
/0/100/2            display    GD 5446
/0/100/3            generic    Xen Platform Device
/1          eth0    network    Ethernet interface



lscpu:

Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              1
On-line CPU(s) list: 0
Thread(s) per core:  1
Core(s) per socket:  1
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               63
Model name:          Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
Stepping:            2
CPU MHz:             2400.034
BogoMIPS:            4800.01
Hypervisor vendor:   Xen
Virtualization type: full
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            30720K
NUMA node0 CPU(s):   0
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology cpuid pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm cpuid_fault invpcid_single pti fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt



free -h:

              total        used        free      shared  buff/cache   available
Mem:           974M        127M        257M        788K        588M        707M
Swap:            0B          0B          0B



lsblk:

NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0      7:0    0 49.6M  1 loop /snap/snapd/17883
loop1      7:1    0 55.6M  1 loop /snap/core18/2667
loop2      7:2    0 24.4M  1 loop /snap/amazon-ssm-agent/6312
xvda     202:0    0    8G  0 disk
├─xvda1  202:1    0  7.9G  0 part /
├─xvda14 202:14   0    4M  0 part
└─xvda15 202:15   0  106M  0 part /boot/efi



### df -h

Filesystem      Size  Used Avail Use% Mounted on
udev            473M     0  473M   0% /dev
tmpfs            98M  788K   97M   1% /run
/dev/xvda1      7.6G  1.3G  6.3G  17% /
tmpfs           488M     0  488M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           488M     0  488M   0% /sys/fs/cgroup
/dev/xvda15     105M  5.2M  100M   5% /boot/efi
/dev/loop0       50M   50M     0 100% /snap/snapd/17883
/dev/loop1       56M   56M     0 100% /snap/core18/2667
/dev/loop2       25M   25M     0 100% /snap/amazon-ssm-agent/6312
tmpfs            98M     0   98M   0% /run/user/1000



```

```