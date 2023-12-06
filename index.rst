Welcome to 6TOPS OpenAIA Manual
===============================

.. _contents: Table of contents

.. toctree::
   :maxdepth: 1
   :caption: Contents:

List of 6TOPS NPU-based AI Accelerators supported by OpenAIA.

   -  Edgeble NCM6A (consumer grade, 0°C to +80°C)
   -  Edgeble NCM6B (industrial grade, -40°C to +85°C)

Quick Start
-----------

-  **NCM6B Kit**

   -  Power
   -  Debug UART
   -  4G/5G Connections

-  **Factory Boot**

   -  MaskROM
   -  Boot from eMMC
   -  Boot from SDMMC

OpenAIA
-------

OpenAIA v1.0
~~~~~~~~~~~~

-  **Compile OpenAIA**

   -  `Debmodel <https://github.com/openaia/debmodel#readme>`__ - For
      Debos based OpenAIA
   -  `meta-openaia <https://github.com/openaia/meta-openaia#readme>`__
      - For Yocto/OE layer based OpenAIA

-  **Compile Linux Kernel**

-  **Compile U-Boot**

-  **Flash Program**

   -  Program eMMC
   -  Program SDMMC
   -  Program SATA
   -  Program M.2 M-Key

IO-NCM6B Ports
--------------

-  PMIC (rk806)
-  eMMC
-  LPDDR4X
-  OTP

WiFi5/BT
~~~~~~~~

-  **Check chip detection**

   lspci must show the Wireless 8260

   ::

      $ lspci | grep 8260
      0003:31:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)

   Check dmesg

   ::

      dmesg | grep iwl
      [   12.320238] iwlwifi 0003:31:00.0: enabling device (0000 -> 0002)
      [   12.394382] iwlwifi 0003:31:00.0: loaded firmware version 36.ca7b901d.0 8000C-36.ucode op_mode iwlmvm
      [   12.687080] iwlwifi 0003:31:00.0: Detected Intel(R) Dual Band Wireless AC 8260, REV=0x208
      [   12.807858] iwlwifi 0003:31:00.0: base HW address: a4:34:d9:0b:85:ce
      [   12.881632] ieee80211 phy0: Selected rate control algorithm 'iwl-mvm-rs'
      [   12.892142] iwlwifi 0003:31:00.0 wlP3p49s0: renamed from wlan0

   Check firmware

   ::

      $ ls /lib/firmware/iwlwifi-8000C-36.ucode 
      /lib/firmware/iwlwifi-8000C-36.ucode

-  **Check ifconfig**

   ::

      $ sudo ifconfig
      wlP3p49s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            ether 36:be:f6:1c:24:34  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

-  **Enable Wifi**

   ::

      $ nmcli r wifi on

-  **Scam Wifi**

   ::

      $ nmcli dev wifi
        IN-USE  BSSID              SSID                 MODE   CHAN  RATE        SIGNAL>
            *   D4:6E:0E:E6:A7:5A      AP-1                 Infra  11    270 Mbit/s  89    >
                9C:53:22:8A:15:0E      AP-2                 Infra  6     130 Mbit/s  52    >

-  **Connect**

   ::

      $ sudo nmcli dev wifi connect "wifi_name" password "wifi_password"
      Device 'wlP3p49s0' successfully activated with 'd0d1f61e-6093-4830-9dea-fa2e0d21b2d5'.

-  **Check IP address**

   ::

      $ sudo ifconfig
      wlP3p49s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
             inet 192.168.0.113  netmask 255.255.255.0  broadcast 192.168.0.255
             inet6 fe80::a577:9922:977e:e49b  prefixlen 64  scopeid 0x20<link>
             ether a4:34:d9:0b:85:ce  txqueuelen 1000  (Ethernet)
             RX packets 34  bytes 5022 (4.9 KiB)
             RX errors 0  dropped 0  overruns 0  frame 0
             TX packets 33  bytes 4427 (4.3 KiB)
             TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
      $ ping google.com
      Device 'wlP3p49s0' successfully activated with 'd0d1f61e-6093-4830-9dea-fa2e0d21b2d5'.
      PING google.com (142.250.195.238) 56(84) bytes of data.
      64 bytes from maa03s43-in-f14.1e100.net (142.250.195.238): icmp_seq=1 ttl=59 time=44.4 ms
      64 bytes from maa03s43-in-f14.1e100.net (142.250.195.238): icmp_seq=2 ttl=59 time=18.4 ms

-  **Check BT**

   lsusb must show the Bluetooth

   ::

      $ lsusb -v | grep Blue
      Bus 004 Device 003: ID 8087:0a2b Intel Corp. Bluetooth wireless interface
      bDeviceProtocol         1 Bluetooth
      idProduct          0x0a2b Bluetooth wireless interface

   Check dmesg

   ::

      $ dmesg | grep Blue
      [   12.651614] Bluetooth: Core ver 2.22
      [   12.651669] Bluetooth: HCI device and connection manager initialized
      [   12.651680] Bluetooth: HCI socket layer initialized
      [   12.651685] Bluetooth: L2CAP socket layer initialized
      [   12.651694] Bluetooth: SCO socket layer initialized
      [   12.767911] Bluetooth: hci0: Bootloader revision 0.0 build 2 week 52 2014
      [   12.774176] Bluetooth: hci0: Device revision is 5
      [   12.774180] Bluetooth: hci0: Secure boot is enabled
      [   12.774183] Bluetooth: hci0: OTP lock is enabled
      [   12.774185] Bluetooth: hci0: API lock is enabled
      [   12.774187] Bluetooth: hci0: Debug lock is disabled
      [   12.774190] Bluetooth: hci0: Minimum firmware build 1 week 10 2014
      [   12.846564] Bluetooth: hci0: Found device firmware: intel/ibt-11-5.sfi
      [   13.053246] Bluetooth: hci0: Failed to send firmware data (-38)
      [   13.053425] Bluetooth: hci0: Intel reset sent to retry FW download
      [   13.201689] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
      [   13.201695] Bluetooth: BNEP filters: protocol multicast
      [   13.201713] Bluetooth: BNEP socket layer initialized
      [   20.731470] Bluetooth: hci0: Bootloader revision 0.0 build 2 week 52 2014
      [   20.737537] Bluetooth: hci0: Device revision is 5
      [   20.737546] Bluetooth: hci0: Secure boot is enabled
      [   20.737551] Bluetooth: hci0: OTP lock is enabled
      [   20.737555] Bluetooth: hci0: API lock is enabled
      [   20.737559] Bluetooth: hci0: Debug lock is disabled
      [   20.737564] Bluetooth: hci0: Minimum firmware build 1 week 10 2014
      [   20.738200] Bluetooth: hci0: Found device firmware: intel/ibt-11-5.sfi
      [   25.491676] Bluetooth: hci0: Waiting for firmware download to complete
      [   25.492579] Bluetooth: hci0: Firmware loaded in 4651839 usecs
      [   25.492877] Bluetooth: hci0: Waiting for device to boot
      [   25.505452] Bluetooth: hci0: Device booted in 12551 usecs
      [   25.506794] Bluetooth: hci0: Found Intel DDC parameters: intel/ibt-11-5.ddc
      [   25.514610] Bluetooth: hci0: Applying Intel DDC parameters completed
      [   25.516684] Bluetooth: hci0: Reading supported features failed (-16)
      [   25.518557] Bluetooth: hci0: Setting Intel telemetry ddc write event mask failed (-95)
      [   25.520587] Bluetooth: hci0: Firmware revision 0.0 build 14 week 44 2021
      [   25.668689] Bluetooth: RFCOMM TTY layer initialized
      [   25.668720] Bluetooth: RFCOMM socket layer initialized
      [   25.668752] Bluetooth: RFCOMM ver 1.11

-  **Bring BT**

   hci0 must up,

   ::

      $ hciconfig hci0 up
      $ hciconfig -a
      hci0:   Type: Primary  Bus: USB
              BD Address: A4:34:D9:0B:85:D2  ACL MTU: 1021:4  SCO MTU: 96:6
              UP RUNNING 
              RX bytes:15089 acl:0 sco:0 events:2438 errors:0
              TX bytes:599636 acl:0 sco:0 commands:2436 errors:0
              Features: 0xbf 0xfe 0x0f 0xfe 0xdb 0xff 0x7b 0x87
              Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
              Link policy: RSWITCH SNIFF 
              Link mode: SLAVE ACCEPT 
              Name: 'fakemachine'
              Class: 0x2c0000
              Service Classes: Rendering, Capturing, Audio
              Device Class: Miscellaneous, 
              HCI Version: 4.2 (0x8)  Revision: 0x100
              LMP Version: 4.2 (0x8)  Subversion: 0x100
              Manufacturer: Intel Corp. (2)

-  **Connect BT**

   ::

      $ bluetoothctl 
      Agent registered
      [CHG] Controller A4:34:D9:0B:85:D2 Pairable: yes
      [bluetooth]# default-agent 
      Default agent request successful
      [bluetooth]# power on
      Changing power on succeeded
      [bluetooth]# scan on
      Discovery started
      [CHG] Controller A4:34:D9:0B:85:D2 Discovering: yes
      [NEW] Device A8:93:4A:0D:20:88 manoj-ThinkPad-E14-Gen-3
      [NEW] Device 94:65:2D:99:C8:CE OnePlus 5
      [bluetooth]# trust 94:65:2D:99:C8:CE
      [CHG] Device 94:65:2D:99:C8:CE Trusted: yes
      Changing 94:65:2D:99:C8:CE trust succeeded
      [bluetooth]# pair 94:65:2D:99:C8:CE
      Attempting to pair with 94:65:2D:99:C8:CE
      [CHG] Device 94:65:2D:99:C8:CE Connected: yes
      Request confirmation
      [agent] Confirm passkey 484339 (yes/no): yes                      
      [CHG] Device 94:65:2D:99:C8:CE Modalias: bluetooth:v001Dp1200d1436
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001103-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001105-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110a-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110c-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110e-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001112-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001115-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001116-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000111f-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000112d-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000112f-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001132-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001200-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001800-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001801-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE ServicesResolved: yes
      [CHG] Device 94:65:2D:99:C8:CE Paired: yes
      Pairing successful
      [CHG] Device 94:65:2D:99:C8:CE ServicesResolved: no
      [CHG] Device 94:65:2D:99:C8:CE Connected: no
      [CHG] Device 94:65:2D:99:C8:CE RSSI: -61
      [NEW] Device B8:C6:AA:F9:6F:DF MiTV-AESP0 2755
      [DEL] Device B8:C6:AA:F9:6F:DF MiTV-AESP0 2755

WiFi6/BT
~~~~~~~~

-  **Check WiFi**

   lspci must show the Wireless 8260

   ::

      $ lspci -m | grep 5480
      0003:31:00.0 "Network controller" "Realtek Semiconductor Co., Ltd." "Device b852" "AzureWave" "Device 5480"

   Check dmesg

   ::

      $ dmesg | grep rtw
      [    8.708631] rtw89_8852be 0003:31:00.0: loaded firmware rtw89/rtw8852b_fw-1.bin
      [    8.710215] rtw89_8852be 0003:31:00.0: enabling device (0000 -> 0003)
      [    8.722915] rtw89_8852be 0003:31:00.0: Firmware version 0.29.29.5 (da87cccd), cmd version 0, type 5
      [    8.723727] rtw89_8852be 0003:31:00.0: Firmware version 0.29.29.5 (da87cccd), cmd version 0, type 3
      [    9.013652] rtw89_8852be 0003:31:00.0: chip rfe_type is 5
      [    9.084340] rtw89_8852be 0003:31:00.0 wlP3p49s0: renamed from wlan0

   Check firmware

   ::

      $ ls /lib/firmware/rtw89/
      rtw8852b_fw-1.bin  rtw8852b_fw.bin

-  **Check ifconfig**

   ::

      $ sudo ifconfig
      wlP3p49s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            ether 36:be:f6:1c:24:34  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

-  **Enable Wifi**

   ::

      $ nmcli r wifi on

-  **Scam Wifi**

   ::

      $ nmcli dev wifi
        IN-USE  BSSID              SSID                 MODE   CHAN  RATE        SIGNAL>
            *   D4:6E:0E:E6:A7:5A      AP-1                 Infra  11    270 Mbit/s  89    >
                9C:53:22:8A:15:0E      AP-2                 Infra  6     130 Mbit/s  52    >

-  **Connect**

   ::

      $ sudo nmcli dev wifi connect "wifi_name" password "wifi_password"
      Device 'wlP3p49s0' successfully activated with 'd0d1f61e-6093-4830-9dea-fa2e0d21b2d5'.

-  **Check IP address**

   ::

      $ sudo ifconfig
      wlP3p49s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
             inet 192.168.0.113  netmask 255.255.255.0  broadcast 192.168.0.255
             inet6 fe80::a577:9922:977e:e49b  prefixlen 64  scopeid 0x20<link>
             ether a4:34:d9:0b:85:ce  txqueuelen 1000  (Ethernet)
             RX packets 34  bytes 5022 (4.9 KiB)
             RX errors 0  dropped 0  overruns 0  frame 0
             TX packets 33  bytes 4427 (4.3 KiB)
             TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
      $ ping google.com
      Device 'wlP3p49s0' successfully activated with 'd0d1f61e-6093-4830-9dea-fa2e0d21b2d5'.
      PING google.com (142.250.195.238) 56(84) bytes of data.
      64 bytes from maa03s43-in-f14.1e100.net (142.250.195.238): icmp_seq=1 ttl=59 time=44.4 ms
      64 bytes from maa03s43-in-f14.1e100.net (142.250.195.238): icmp_seq=2 ttl=59 time=18.4 ms

-  **Check BT**

   lsusb must show the Bluetooth

   ::

      $ lsusb -v | grep Blue
      Bus 004 Device 002: ID 13d3:3572 IMC Networks Bluetooth Radio
      bDeviceProtocol         1 Bluetooth
      iProduct                2 Bluetooth Radio

   Check dmesg

   ::

      $ dmesg | grep Blue
      [   11.192691] usb 4-1: Product: Bluetooth Radio
      [   17.430191] Bluetooth: Core ver 2.22
      [   17.430280] Bluetooth: HCI device and connection manager initialized
      [   17.430297] Bluetooth: HCI socket layer initialized
      [   17.430305] Bluetooth: L2CAP socket layer initialized
      [   17.430322] Bluetooth: SCO socket layer initialized
      [   17.660674] Bluetooth: hci0: RTL: examining hci_ver=0b hci_rev=000b lmp_ver=0b lmp_subver=8852
      [   17.662659] Bluetooth: hci0: RTL: rom_version status=0 version=1
      [   17.662662] Bluetooth: hci0: RTL: loading rtl_bt/rtl8852bu_fw.bin
      [   18.100228] Bluetooth: hci0: RTL: loading rtl_bt/rtl8852bu_config.bin
      [   18.110309] rtk_btusb: Realtek Bluetooth USB driver ver 3.1.6d45ddf.20220519-142432
      [   18.126013] Bluetooth: hci0: RTL: cfg_sz 6, total sz 58003
      [   18.444296] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
      [   18.444304] Bluetooth: BNEP filters: protocol multicast
      [   18.444317] Bluetooth: BNEP socket layer initialized
      [   18.664166] Bluetooth: hci0: RTL: fw version 0xdbc6b20f
      [   25.805029] Bluetooth: RFCOMM TTY layer initialized
      [   25.805056] Bluetooth: RFCOMM socket layer initialized
      [   25.805092] Bluetooth: RFCOMM ver 1.11

   Check firmware

   ::

      $ ls /lib/firmware/rtl_bt/
      rtl8852bu_config.bin  rtl8852bu_fw.bin

-  **Bring BT**

   hci0 must up,

   ::

      $ hciconfig hci0 up
      $ hciconfig -a
      hci0:   Type: Primary  Bus: USB
            BD Address: CC:47:40:A3:15:01  ACL MTU: 1021:6  SCO MTU: 255:12
            UP RUNNING PSCAN 
            RX bytes:2432 acl:0 sco:0 events:293 errors:0
            TX bytes:62179 acl:0 sco:0 commands:293 errors:0
            Features: 0xff 0xff 0xff 0xfe 0xdb 0xfd 0x7b 0x87
            Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
            Link policy: RSWITCH HOLD SNIFF PARK 
            Link mode: SLAVE ACCEPT 
            Name: 'fakemachine'
            Class: 0x2c0000
            Service Classes: Rendering, Capturing, Audio
            Device Class: Miscellaneous, 
            HCI Version:  (0xc)  Revision: 0xdbc6
            LMP Version:  (0xc)  Subversion: 0xb20f
            Manufacturer: Realtek Semiconductor Corporation (93)

-  **Connect BT**

   ::

      $ bluetoothctl 
      Agent registered
      [CHG] Controller CC:47:40:A3:15:01 Pairable: yes
      [bluetooth]# default-agent 
      Default agent request successful
      [bluetooth]# power on
      Changing power on succeeded
      [bluetooth]# scan on
      Discovery started
      [CHG] Controller CC:47:40:A3:15:01 Discovering: yes
      [NEW] Device A8:93:4A:0D:20:88 manoj-ThinkPad-E14-Gen-3
      [NEW] Device 94:65:2D:99:C8:CE OnePlus 5
      [bluetooth]# trust 94:65:2D:99:C8:CE
      [CHG] Device 94:65:2D:99:C8:CE Trusted: yes
      Changing 94:65:2D:99:C8:CE trust succeeded
      [bluetooth]# pair 94:65:2D:99:C8:CE
      Attempting to pair with 94:65:2D:99:C8:CE
      [CHG] Device 94:65:2D:99:C8:CE Connected: yes
      Request confirmation
      [agent] Confirm passkey 484339 (yes/no): yes                      
      [CHG] Device 94:65:2D:99:C8:CE Modalias: bluetooth:v001Dp1200d1436
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001103-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001105-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110a-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110c-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000110e-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001112-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001115-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001116-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000111f-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000112d-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 0000112f-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001132-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001200-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001800-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE UUIDs: 00001801-0000-1000-8000-00805f9b34fb
      [CHG] Device 94:65:2D:99:C8:CE ServicesResolved: yes
      [CHG] Device 94:65:2D:99:C8:CE Paired: yes
      Pairing successful
      [CHG] Device 94:65:2D:99:C8:CE ServicesResolved: no
      [CHG] Device 94:65:2D:99:C8:CE Connected: no
      [CHG] Device 94:65:2D:99:C8:CE RSSI: -61
      [NEW] Device B8:C6:AA:F9:6F:DF MiTV-AESP0 2755
      [DEL] Device B8:C6:AA:F9:6F:DF MiTV-AESP0 2755

-  CAM0

-  CAM1

.. _io-ncm6b-ports-1:

IO-NCM6B Ports
--------------

-  SD Card
-  PWM Fan
-  RTC
-  RS232
-  RS485
-  CAN
-  Buttons
-  LED
-  POE
-  40PIN Header
-  USB 2.0
-  USB 3.0

2.5G ETH
~~~~~~~~

-  **Check ETH**

   ::

      $ lsmod | grep r8169
        r8169                  90112  0
      $ lspci | grep Ethernet
        0002:21:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller (rev 05)

-  **Check IP address**

   ::

      $ sudo ifconfig enP2p33s0
      enP2p33s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.29.169  netmask 255.255.255.0  broadcast 192.168.29.255
        inet6 2405:201:c00a:a208:d2f2:553c:fd24:67a3  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::94e3:a26c:1938:8b45  prefixlen 64  scopeid 0x20<link>
        ether 0a:31:5d:75:01:ab  txqueuelen 1000  (Ethernet)
        RX packets 506  bytes 38898 (37.9 KiB)
        RX errors 0  dropped 72  overruns 0  frame 0
        TX packets 106  bytes 10049 (9.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

-  **Ping**

   ::

      $ sudo ping google.com
      PING google.com(maa05s23-in-x0e.1e100.net (2404:6800:4007:81e::200e)) 56 data bytes
      64 bytes from maa05s23-in-x0e.1e100.net (2404:6800:4007:81e::200e): icmp_seq=1 ttl=118 time=17.8 ms
      64 bytes from maa05s23-in-x0e.1e100.net (2404:6800:4007:81e::200e): icmp_seq=2 ttl=118 time=17.0 ms

-  Audio Playback

-  Audio Record

-  SATA

-  M.2 M-Key (WiFi)

M.2 B-Key (4G)
~~~~~~~~~~~~~~

-  **Link peripheral**

   First, connect 4G Module to board . You can check if the device is
   connected by the following command:

   ::

      $ lsusb | grep -i Quectel
      Bus 001 Device 003: ID 2c7c:0125 Quectel Wireless Solutions Co., Ltd. EC25 LTE modem

   The modem usually communicates with the host computer through a
   serial port. Check whether the system correctly enumerates the
   corresponding serial port devices:

   ::

      $ ls /dev/ttyUSB*
      /dev/ttyUSB0  /dev/ttyUSB1  /dev/ttyUSB2  /dev/ttyUSB3

-  **Test the modem**

   First, open the serial port using picocom :

   ::

      $ sudo picocom -b 115200 /dev/ttyUSB3

   After the program starts, you can enter the following at command to
   check the status of the modem:

   ::

      Terminal ready
      at+cpin?
      +CPIN: READY
      OK  #Check whether the SIM card is in place

      at+csq
      +CSQ: 11,99

      OK  #Detection signal. 99 means no signal

      at+cops?
      +COPS: 0,0,"JIO 4G Jio",7

      OK #View Carrier

      at+creg?
      +CREG: 0,1

      OK  #Get the registration status of the phone (0,1: indicates normal registration)

      at+qeng="servingcell"
      +QENG: "servingcell","NOCONN","LTE","FDD",405,854,49E31,91,2450,5,3,3,74,-124,-16,-91,-5,3

      OK  #Signal strength and quality of the currently connected service cell

   If the modems return to normal, you can use the Ctrl+A Ctrl+X key
   combination to exit picocom .

   ::

      Terminating...
      Thanks for using picocom
      $

-  **Dial-up Internet via ppp**

   You can now try dialing using ppp :

   ::

      $ sudo pppd call rasppp &    #Background dialing

   The complete dial-up process is shown as follows:

   ::

      $ sudo pppd call rasppp &

      [1] 540
      $
      pppd options in effect:
      debug           # (from /etc/ppp/peers/rasppp)
      nodetach                # (from /etc/ppp/peers/rasppp)
      dump            # (from /etc/ppp/peers/rasppp)
      noauth          # (from /etc/ppp/peers/rasppp)
      user ctnet@mycdma.cn            # (from /etc/ppp/peers/rasppp)
      password ??????         # (from /etc/ppp/peers/rasppp)
      remotename 3gppp                # (from /etc/ppp/peers/rasppp)
      /dev/ttyUSB3            # (from /etc/ppp/peers/rasppp)
      115200          # (from /etc/ppp/peers/rasppp)
      lock            # (from /etc/ppp/peers/rasppp)
      connect /usr/sbin/chat -s -v -f /etc/ppp/peers/rasppp-chat-connect              # (from /etc/ppp/peers/rasppp)
      disconnect /usr/sbin/chat -s -v -f /etc/ppp/peers/rasppp-chat-disconnect                # (from /etc/ppp/peers/rasppp)
      crtscts         # (from /etc/ppp/peers/rasppp)
      local           # (from /etc/ppp/peers/rasppp)
      asyncmap 0              # (from /etc/ppp/options)
      lcp-echo-failure 4              # (from /etc/ppp/options)
      lcp-echo-interval 30            # (from /etc/ppp/options)
      hide-password           # (from /etc/ppp/peers/rasppp)
      novj            # (from /etc/ppp/peers/rasppp)
      novjccomp               # (from /etc/ppp/peers/rasppp)
      ipcp-accept-local               # (from /etc/ppp/peers/rasppp)
      ipcp-accept-remote              # (from /etc/ppp/peers/rasppp)
      ipparam 3gppp           # (from /etc/ppp/peers/rasppp)
      noipdefault             # (from /etc/ppp/peers/rasppp)
      defaultroute            # (from /etc/ppp/peers/rasppp)
      usepeerdns              # (from /etc/ppp/peers/rasppp)
      noccp           # (from /etc/ppp/peers/rasppp)
      noipx           # (from /etc/ppp/options)
      timeout set to 15 seconds
      abort on (BUSY)
      abort on (ERROR)
      abort on (NO ANSWER)
      abort on (NO CARRTER)
      abort on (NO DIALTONE)
      send (AT^M)
      expect (OK)
      AT^M^M
      OK
      -- got it

      send (^MATZ^M)
      expect (OK)
      ^M
      ATZ^M^M
      OK
      -- got it

      send (^MAT+CGDCONT=1,"IP",""^M)
      expect (OK)
      ^M
      AT+CGDCONT=1,"IP",""^M^M
      OK
      -- got it

      send (ATDT#777^M)
      expect (CONNECT)
      ^M
      ATDT#777^M^M
      CONNECT
      -- got it

      send (\d)
      Script /usr/sbin/chat -s -v -f /etc/ppp/peers/rasppp-chat-connect finished (pid 555), status = 0x0
      Serial connection established.
      using channel 1
      Using interface ppp0
      Connect: ppp0 <--> /dev/ttyUSB3
      sent [LCP ConfReq id=0x1 <asyncmap 0x0> <magic 0xfb465ca3> <pcomp> <accomp>]
      rcvd [LCP ConfReq id=0x0 <asyncmap 0x0> <auth chap MD5> <magic 0x2bd81892> <pcomp> <accomp>]
      sent [LCP ConfAck id=0x0 <asyncmap 0x0> <auth chap MD5> <magic 0x2bd81892> <pcomp> <accomp>]
      rcvd [LCP ConfAck id=0x1 <asyncmap 0x0> <magic 0xfb465ca3> <pcomp> <accomp>]
      sent [LCP EchoReq id=0x0 magic=0xfb465ca3]
      rcvd [LCP DiscReq id=0x1 magic=0x2bd81892]
      rcvd [CHAP Challenge id=0x1 <7767d88a1a163c58bfa43a909cb088d7>, name = "UMTS_CHAP_SRVR"]
      sent [CHAP Response id=0x1 <780ce605b4caf11cb42905af945adf04>, name = "ctnet@mycdma.cn"]
      rcvd [LCP EchoRep id=0x0 magic=0x2bd81892 fb 46 5c a3]
      rcvd [CHAP Success id=0x1 ""]
      CHAP authentication succeeded
      CHAP authentication succeeded
      kernel does not support PPP filtering
      sent [IPCP ConfReq id=0x1 <addr 0.0.0.0> <ms-dns1 0.0.0.0> <ms-dns2 0.0.0.0>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      rcvd [IPCP ConfReq id=0x0]
      sent [IPCP ConfNak id=0x0 <addr 0.0.0.0>]
      rcvd [IPCP ConfRej id=0x1 <ms-dns2 0.0.0.0>]
      sent [IPCP ConfReq id=0x2 <addr 0.0.0.0> <ms-dns1 0.0.0.0>]
      rcvd [IPCP ConfReq id=0x1]
      sent [IPCP ConfAck id=0x1]
      rcvd [IPCP ConfNak id=0x2 <addr 10.221.128.38> <ms-dns1 49.45.0.1>]
      sent [IPCP ConfReq id=0x3 <addr 10.221.128.38> <ms-dns1 49.45.0.1>]
      rcvd [IPCP ConfAck id=0x3 <addr 10.221.128.38> <ms-dns1 49.45.0.1>]
      Could not determine remote IP address: defaulting to 10.64.64.64
      Script /etc/ppp/ip-pre-up started (pid 567)
      Script /etc/ppp/ip-pre-up finished (pid 567), status = 0x0
      local  IP address 10.221.128.38
      remote IP address 10.64.64.64
      primary   DNS address 49.45.0.1
      Script /etc/ppp/ip-up started (pid 570)
      Script /etc/ppp/ip-up finished (pid 570), status = 0x0
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      sent [IPV6CP ConfReq id=0x1 <addr fe80::8c4f:5739:ce37:d292>]
      $ IPV6CP: timeout sending Config-Requests

   From the output of the program we can get the following information:

   ::

      1.local IP address   : 10.221.128.38
      2.primary DNS server : 49.45.0.1

   We can now configure the network based on the above information:

   ::

      # configure the gateway
      $ sudo ip route add default via 10.221.128.38

      # configure primary DNS
      $ echo "nameserver 49.45.0.1" | sudo tee -a /etc/resolv.conf

   Check the updated config of ppp using ifconfig

   ::

      $ sudo ifconfig
      ppp0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
          inet 10.221.128.38   netmask 255.255.255.255  destination 10.64.64.64
          ppp  txqueuelen 3  (Point-to-Point Protocol)
          RX packets 5  bytes 50 (50.0 B)
          RX errors 0  dropped 0  overruns 0  frame 0
          TX packets 47  bytes 2032 (1.9 KiB)
          TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

   You can now use the ping command to check if you are connected to the
   Internet:

   ::

      $ ping google.com
      PING google.com (142.250.196.46) 56(84) bytes of data.
      64 bytes from maa03s45-in-f14.1e100.net (142.250.196.46): icmp_seq=2 ttl=113 time=308 ms
      64 bytes from maa03s45-in-f14.1e100.net (142.250.196.46): icmp_seq=3 ttl=113 time=1626 ms
      64 bytes from maa03s45-in-f14.1e100.net (142.250.196.46): icmp_seq=4 ttl=113 time=1570 ms

-  M.2 B-Key (5G)

-  HDMI Out

-  Display Port 0

-  Display Port 1

-  MIPI DSI 0

-  MIPI DSI 1

-  eDP

-  HDMI In

-  CAM2

-  CAM3

-  CAM4

-  CAM5
