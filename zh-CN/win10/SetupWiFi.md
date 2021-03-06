---
layout: default
title: 在 Windows 10 IoT 核心版设备上使用 WiFi。
permalink: /zh-CN/win10/SetupWiFi.htm
lang: zh-CN
---

##在 Windows 10 IoT 核心版设备上使用 WiFi

在使用 USB WiFi 适配器的过程中，WiFi 在 Windows 10 IoT 核心版设备上受支持。使用 WiFi 可提供有线连接的所有功能，包括 [SSH]({{site.baseurl}}/{{page.lang}}/win10/samples/SSH.htm)、[Powershell]({{site.baseurl}}/{{page.lang}}/win10/samples/PowerShell.htm)、[Web 设备管理]({{site.baseurl}}/{{page.lang}}/win10/tools/DevicePortal.htm)以及应用程序调试和部署。

	注意: 插入一个有线的网络将会覆盖无线设置而成为缺省网络接口

### <a name="WiFi_Devices"></a>受支持的适配器
以下 WiFi 适配器已在 Windows 10 IoT 核心版上进行测试：

| Raspberry Pi 2                                                     || MinnowBoard Max                                                    | 
|--------------------------------------------------------------------||--------------------------------------------------------------------| 
|[Raspberry Pi 无线适配器](http://swag.raspberrypi.org/collections/frontpage/products/official-raspberry-pi-Wifi-dongle){:target="_blank"}||[Airlink Wireless N 150 微型 USB 适配器](http://www.amazon.com/Airlink101-AWLL5077-150Mbps-Wireless-Adapter/dp/B002VFWY9M){:target="_blank"}| 
|||[Panda PAU06](http://www.amazon.com/Panda-300Mbps-Wireless-N-Adapter-button/dp/B00JDVRCI0){:target="_blank"}| 
|||[TP-LINK TL\_WN725N](http://www.amazon.com/TP-LINK-TL-WN725N-Wireless-Adapter-150Mbps/dp/B008IFXQFU){:target="_blank"}| 
|||[NET-DYN USB 适配器](http://www.amazon.com/Adapter-NET-DYN%C2%AE-Perfect-Desktop-Laptop/dp/B00LWE14TO){:target="_blank"}| 
|||[Realtek 8191](http://www.amazon.com/Realtek-300Mbps-802-11n-Wireless-Network/dp/B00AVSRLTO){:target="_blank"}|

### 配置 WiFi
若要使用 WiFi，将需要向 Windows 10 IoT 核心版提供 WiFi 网络凭据。可通过以下几种不同选项执行此操作：

###选项 1： 启动配置
**先决条件：** Windows 10 IoT 核心版设备需要插入鼠标、键盘、显示器和 USB WiFi 适配器

首次使用受支持的 USB WiFi 适配器启动 Windows 10 IoT 核心版时，将呈现配置屏幕。在配置屏幕上，选择想要连接到的 WiFi 网络，并提供密码。单击“连接”以启动连接。

![启动 WiFi 配置屏幕]({{site.baseurl}}/images/SetupWiFi/WiFiStartupConfig.png)

###选项 2： 默认应用配置
**先决条件：** Windows 10 IoT 核心版设备需要插入鼠标、键盘、显示器和 USB WiFi 适配器

配置 WiFi 的替代方法是使用默认应用。可使用此方法在启动设备后配置或修改 WiFi 设置。

1. 单击主页上的齿轮形设置图标
2. 在左侧窗格中选择“网络和 Wi-Fi”
3. 单击要连接到的 WiFi 网络。在提示时提供密码，并单击“连接”

![默认应用 WiFi 配置]({{site.baseurl}}/images/SetupWiFi/DefaultAppWiFiConfig.png)

###选项 3： 基于 Web 的配置
**先决条件：** 设备已需要通过以太网连接到本地网络，并且插入了 USB WiFi 适配器

如果设备缺少 UI、显示器或输入设备，仍可通过[基于 Web 的管理]({{site.baseurl}}/{{page.lang}}/win10/tools/DevicePortal.htm)配置该设备。

1. 通过使用 Web 浏览器，导航到 `http://[device_ip]:8080/`，其中 **\[device\_ip\]** 是 Windows 10 IoT 核心版设备的 IP 地址 \(ex: **192.168.1.4**\)。输入用户名的“管理员”，并提供密码。
2. 单击左侧窗格中的“网络”
3. 在“可用网络”下，选择要连接到的网络，并提供连接凭据。单击“连接”以启动连接

![基于 Web 的 WiFi 配置]({{site.baseurl}}/images/SetupWiFi/WebBWiFiConfig.png)

###选项 4： 使用 WiFi 配置文件进行连接
**先决条件：** 设备已需要通过以太网连接到本地网络，并且插入了 USB WiFi 适配器。还需要具有 WiFi 功能的 Windows 电脑。

Windows 10 IoT 核心版支持使用无线配置文件设置 WiFi。有关详细信息和示例，请参阅 [MSDN](https://msdn.microsoft.com/zh-CN/library/windows/desktop/aa369853)。

1. 将 Windows 电脑连接到所需的无线网络，并使用以下命令创建 WiFi 配置文件 XML 文件：

    * `netsh wlan show profiles` -\> 查找刚添加的配置文件名称

    * `netsh wlan export profile name=<your profilename>`。这会将配置文件导出到某个 XML 文件

2. 打开“文件资源管理器”窗口，并在地址栏中键入 `\\<TARGET_DEVICE>\C$\`，然后点击 Enter。在此特定情况下，`<TARGET_DEVICE>` 可以是 Windows 10 IoT 核心版设备的名称或 IP 地址：

    ![使用文件资源管理器的 SMB]({{site.baseurl}}/images/DriverLab/smb1.png)

    如果系统提示输入用户名和密码，请使用以下凭据：

        User Name: <TARGET_DEVICE>\Administrator
        Password:  p@ssw0rd

    ![使用文件资源管理器的 SMB]({{site.baseurl}}/images/DriverLab/cred1.png)
	
    注意： **强烈建议**你更新默认的管理员帐户密码。请按照在[此处]({{site.baseurl}}/{{page.lang}}/win10/samples/PowerShell.htm)获取的说明进行操作。

3. 将导出的 WiFi 配置文件 XML 文件从 Windows 电脑复制到 Windows 10 IoT 核心版设备

4. 通过执行以下命令，使用 [PowerShell]({{site.baseurl}}/{{page.lang}}/win10/samples/PowerShell.htm) 连接到设备，并向设备添加新的 WiFi 配置文件

    * `netsh wlan add profile filename=<copied XML path>`

    * `netsh wlan show profiles`

5. 通过 netsh，将 Windows 10 IoT 核心版设备连接到无线网络

    * `netsh wlan connect name=<profile name>`

6. 请验证设备是否连接到无线网络并且可访问 Internet

    * `netsh wlan show interfaces`

    * `ipconfig /all`

    * `ping /S <your WiFi adapter ip address> bing.com`

 

#### 连接到 WPA2-PSK 个人网络

如果需要连接到 WPA2-PSK 个人 WiFi 网络，请首先按照上述说明进行操作，但要对 XML 文件作出以下更改。唯一的区别是，在 Windows 电脑导出 XML 时，它将对密码进行加密。

    NOTE: this will make your connection insecure

从 Windows 电脑导出的配置文件 XML：

    <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>true</protected>
        <keyMaterial><Your Encrypted password></keyMaterial>
    </sharedKey>

 

需要在 Windows 10 IoT 核心版上生效的更改：

    <sharedKey>
        <keyType>passPhrase</keyType>
        <protected>false</protected>
        <keyMaterial><Your Unencrypted password></keyMaterial>
    </sharedKey>
