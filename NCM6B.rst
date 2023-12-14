AI Accelerator
##############
NCM6B
*****
-  PMIC (rk806)
-  eMMC
-  LPDDR4X
-  OTP

WiFi5/BT
--------

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
--------

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

