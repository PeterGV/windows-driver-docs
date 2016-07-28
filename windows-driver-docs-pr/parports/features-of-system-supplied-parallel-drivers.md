---
title: Features of System-Supplied Parallel Drivers
author: windows-driver-content
description: Features of System-Supplied Parallel Drivers
MS-HAID:
- 'sspd\_73eda256-542a-4967-8b5f-183f45723b1d.xml'
- 'parports.features\_of\_system\_supplied\_parallel\_drivers'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 6d579a88-4608-4333-9789-e10c562fc644
keywords: ["system-supplied parallel drivers WDK , about system-supplied parallel drivers", "Parclass driver", "Parport driver", "functional device objects WDK ports", "FDOs WDK ports", "IEEE 1284 WDK"]
---

# Features of System-Supplied Parallel Drivers


## <a href="" id="ddk-features-of-system-supplied-parallel-drivers-kg"></a>


This section describes the features of the system-supplied parallel drivers for parallel ports and devices that are attached to parallel ports.

Except for 64-bit versions of Microsoft Windows, Windows 2000 and later provides a parallel port function driver and a parallel port bus driver for Plug and Play devices that are attached to a parallel port. Microsoft does not provide parallel drivers for 64-bit versions of Windows.

Windows 2000 includes the following drivers:

-   *Parclass* is the parallel port bus driver for devices that are attached to parallel ports. The executable image of Parclass is *parallel.sys*.

-   *Parport* is the parallel port function driver. The executable image of Parport is *parport.sys*.

The operation of Parclass and Parport is closely connected through [internal device control requests for parallel ports](https://msdn.microsoft.com/library/windows/hardware/ff543963) and [parallel port callback routines](https://msdn.microsoft.com/library/windows/hardware/ff544307).

In Windows XP and later, Parclass is removed, and Parport provides the function of both the parallel port function driver and the parallel port bus driver. The executable image of Parport in Windows XP is *parport.sys*.

The system-supplied function driver for parallel ports creates a functional device object (FDO) that represents each parallel port enumerated in the system. The system-supplied bus driver for parallel ports creates a physical device object (PDO) that represents each parallel device that the bus driver enumerates on a port. Clients, for example [vendor-supplied parallel drivers](vendor-supplied-parallel-drivers.md), operate a parallel device through the interfaces provided by a parallel device's PDO and the FDO of the device's parent port.

Except for minor operational differences described throughout the parallel documentation, the [client interfaces to system-supplied parallel drivers](https://msdn.microsoft.com/library/windows/hardware/ff543926) is the same in Windows 2000 as in Windows XP and later.

The system-supplied parallel drivers support:

-   Legacy parallel ports, standard parallel port devices, IEEE 1284-compatible devices, IEEE 1284-compliant devices, and IEEE 1284.3 daisy chain devices

-   Most communication modes, including Centronics mode, IEEE 1284 modes, extended capabilities port (ECP) mode, and enhanced parallel port (EPP) mode

-   Plug and Play, power management, and Windows Management Instrumentation (WMI)

-   Shared access to all the parallel ports installed on the system

-   Raw access to all parallel devices

-   IOCTLs and callbacks to operate parallel ports and devices -- see [IOCTL and Callback Support for Parallel Ports and Devices](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

The system-supplied parallel drivers provide the following *partial* support for IEEE 1284.3 devices:

-   A combination of device control requests and callback routines that is functionally equivalent to the *Service Provider Interface*. See *Service Provider Interface (SPI)* in the IEEE P1284.3 specification.

-   The selection and operation of more than one IEEE 1284.3 daisy chain device and an end-of-chain device*, as* defined in the *Daisy Chaining* clause of the IEEE P1284.3 specification.

-   Basic services to support the data link layer, as specified in the *Data link layer* clause of the IEEE P1284.3 specification -- see [Connecting to an IEEE 1284.3 Data Link Device](connecting-to-an-ieee-1284-3-data-link-device.md).

The system-supplied parallel drivers *do not support* the following IEEE 1284.3 specifications:

-   Multiplexors, as specified in the *Multiplexor* clause of the IEEE P1284.3 specification.

    There are no plans to support this feature in future releases of Windows.

-   Interrupts for IEEE 1284.3 daisy chain devices.

The system-supplied parallel drivers create:

-   Device objects, interfaces, and unprotected symbolic links, as described in [Device Stacks for Parallel Ports and Devices](device-stacks-for-parallel-ports-and-devices.md).

-   A work queue for each parallel port.

    The system-supplied function driver for parallel ports queues I/O requests to allocate a parallel port and to select an IEEE 1284.3 device attached to a parallel port.

-   A worker thread and work queue for each parallel device.

    The system-supplied bus driver for parallel ports queues the following I/O requests if it cannot immediately complete them: read, write, device control, and internal device control.

For more information about how to operate parallel ports and devices attached to parallel ports, see:

[Introduction to Parallel Ports and Devices](introduction-to-parallel-ports-and-devices.md)

[Vendor-Supplied Parallel Drivers](vendor-supplied-parallel-drivers.md)

[Client Interfaces to System-Supplied Parallel Drivers](https://msdn.microsoft.com/library/windows/hardware/ff543926)

For information about parallel port and device standards, see the following specifications:

-   IEEE Std 1284-1994, IEEE Standard Signaling Method for a Bidirectional Parallel Peripheral Interface for Personal Computers

-   IEEE P1284.3, Standard for Interface and Protocol Extensions to IEEE 1284-1994 Compliant Peripherals and Host Adapters, Draft D6.00, December 3, 1998

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bparports\parports%5D:%20Features%20of%20System-Supplied%20Parallel%20Drivers%20%20RELEASE:%20%287/25/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

