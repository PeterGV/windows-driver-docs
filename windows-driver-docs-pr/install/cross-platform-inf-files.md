---
title: Cross-Platform INF Files
description: Cross-Platform INF Files
ms.assetid: 5f7e80d2-b8b5-4ce9-9e70-cacc51223deb
keywords: ["cross-platform INF files WDK", "INF files WDK device installations , cross-platform", "operating systems WDK , cross-operating system INF files"]
---

# Cross-Platform INF Files


The simplest strategy for cross-platform INF files is to create a separate INF file for each platform type because this approach is the easiest to create and maintain. For more information about how to create platform-specific INF files, see the following topics:

[Creating INF Files for x64-Based Systems (Windows XP and later)](inf-file-platform-extensions-and-x64-based-systems.md#creating-inf-files-for-x64-based-systems--windows-xp-and-later-)

[Creating INF Files for x86-Based Systems (Windows 2000 and Later)](inf-file-platform-extensions-and-x86-based-systems.md#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

You can create a single cross-operating system and cross-platform INF file for a device if the device does not have operating system-specific installation requirements. For example, if the files or registry settings that support a device differ between operating system versions for a given platform, you cannot, in general, create a single INF file for that platform type that is supported by all operating system versions.

To create a single cross-operating system and cross-platform INF file for Windows 2000 and later versions of Windows, the simplest approach is as follows:

-   Use **.ntia64** platform extensions on the names of sections that are required to install components on Itanium-based systems, and use **.ntamd64** platform extensions on the names of sections that are required to install components on x64-based systems.

-   Because **.nt** and **.ntx86** platform extensions are optional on all sections that support platform extensions, do not use an **.nt** or **.ntx86** platform extension on the names of sections that install components on x86-based systems.

To create a single cross-operating system and cross-platform INF file for Microsoft Windows 2000 and later versions of Windows, use the following process:

-   Use **.ntia64** platform extensions on the names of sections that are required to install components on Itanium-based systems, and use **.ntamd64** platform extensions on the names of sections that are required to install components on x64-based systems.

To create a single cross-operating system and cross-platform INF file for a device that does not have operating system-specific requirements, supports all platform types, and that supports Windows 2000 and later versions of Windows, do the following:

1.  Create a valid INF file that contains the generic entries that are required in all INF files, as described in [General Guidelines for INF Files](general-guidelines-for-inf-files.md).

2.  Include an INF **Manufacturer** section that includes a *manufacturer-identifier* that specifies the *Models* section name for a device and a platform extension entry for each platform that the device supports. For example, the following Manufacturer section specifies a *Models* section name of "AbcModelSection" and the platform extensions **.ntia64** and **.ntamd64**. (Do not specify the **.ntx86** platform extension.)

    ```
    [Manufacturer]
    ; The manufacturer-identifier for the Abc device.
    %ManufacturerName%=AbcModelSection,ntia64,ntamd64
    ```

3.  Include a *Models* section whose name does not include a platform extension. Starting with Windows 2000, the operating system processes this section for x86-based systems. For example, the following AbcModelSection section specifies an *install-section-name* of "AbcInstallSection" for an Abc device.

    ```
    [AbcModelSection]
    %AbcDeviceName%=AbcInstallSection,Abc-hw-id
    ```

4.  Include a *Models***.ntia64** section. Windows Server 2003 SP1 and later versions require a *Models***.ntia64** section for Itanium-based systems. If a *Models***.ntia64** section exists, Windows Server 2003 and Windows XP also use this section for Itanium-based systems. For example, the following AbcModelSection**.ntia64** section specifies an *install-section-name* of "AbcInstallSection.ntia64" for an Abc device.

    ```
    [AbcModelSection.ntia64]
    %AbcDeviceName%=AbcInstallSection.ntia64,Abc-hw-id
    ```

5.  Include a *Models***.ntamd64** section. Windows Server 2003 SP1 and later versions require a *Models***.ntamd64** section for x64-based systems. If a *Models***.ntamd64** section exists, Windows Server 2003 and Windows XP also use this section for x64-based systems. For example, the following AbcModelSection**.ntamd64** section specifies an *install-section-name* of "AbcInstallSection.ntamd64" for an Abc device.

    ```
    AbcModelSectionName.ntamd64
    %AbcDeviceName%=AbcInstallSection.ntamd64,Abc-hw-id
    ```

6.  Include a *DDInstall* section whose name is the same as the *install-section-name* that is specified by the *Models* section that does not include a platform extension. For example, the AbcModelSection section specifies the following AbcInstallSection section. Windows processes this section to install the Abc device on x86-based systems that run Windows 2000 or later versions of Windows.

    ```
    [AbcInstallSection]
    ; Install section entries go here.
    ...
    ```

7.  Include a *DDInstall***.ntia64** section whose name is the same as the *install-section-name* that is specified by the *Models***.ntia64** section. For example, the AbcModelSection**.ntia64** section specifies the following AbcInstallSection**.ntia64** section. Windows processes this section to install the Abc device on Itanium-based systems that run Windows XP or later versions of Windows.

    ```
    [AbcInstallSection.ntia64]
    ; Install section entries go here.
    ...
    ```

8.  Include a *DDInstall***.ntamd64** section whose name is the same as the *install-section-name* that is specified by the *Models***.ntamd64** section. For example, the AbcModelSection**.ntamd64** section specifies the following AbcInstallSection**.ntamd64** section. Windows processes this section to install the Abc device on x64-based systems that run Windows XP or later versions of Windows.

    ```
    [AbcInstallSection.ntamd64]
    ; Install section entries go here.
    ...
    ```

9.  Include additional device-specific sections that are required for an x86-based installation. Do not include an **.ntx86** platform extension on the names of these sections. Windows processes these sections by default to install the device on x86-based systems that run Windows 2000 or later versions of Windows.

10. Include additional device-specific sections that are required for Itanium-based systems that run Windows XP or later versions of Windows. Include the **.ntia64** extension on these section names.

11. Include additional device-specific sections that are required for x64-based systems that run Windows XP or later versions of Windows. Include the **.ntamd64** extension on these section names.

For more information about INF file sections and directives, see [Summary of INF Sections](summary-of-inf-sections.md) and [Summary of INF Directives](summary-of-inf-directives.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bdevinst\devinst%5D:%20Cross-Platform%20INF%20Files%20%20RELEASE:%20%287/22/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



