# 版本不支持
## 报错如下
```
Add-AppxPackage : 部署失败，原因是 HRESULT: 0x80073CFD, 无法满足安装的先决条件。
由于程序包 MicrosoftCorporationII.WindowsSubsystemForAndroid_2407.40000.0.0_x64__8wekyb3d8bbwe 与设备不兼容，Windows 无
法安装该程序包。该程序包要求 Windows.Desktop 设备系列运行操作系统版本 10、0、22000、120 或更高版本。该设备当前运行的操
作系统版本为 10、0、19044、4651。
```

## 解决方法
修改AppxManifest.xml文件，把最低支持的版本(`MinVersion`)修改为本机的版本
``` xml
 <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.22000.120" MaxVersionTested="10.0.22000.120" />
```

# 系统无法注册 windows.customInstall
## 报错如下
```
错误 0x80080204: 在准备处理请求时，由于以下错误，系统无法注册 windows.customInstall 扩展: Appx 包的清单无效。
。
```

## 解决方法
修改AppxManifest.xml文件，注释掉与windows.customInstall有关的配置
``` xml
<Capabilities>
    <Capability Name="internetClient" />
    <Capability Name="internetClientServer" />
    <Capability Name="privateNetworkClientServer" />
    <rescap:Capability Name="runFullTrust" />
    <rescap:Capability Name="unvirtualizedResources" />
    <rescap:Capability Name="packagedServices" />
    <rescap:Capability Name="localSystemServices" />
    <rescap:Capability Name="packageManagement" />
    <rescap:Capability Name="packageQuery" />
<!-- 与windows.customInstall有关的   
	<rescap:Capability Name="customInstallActions" />
    <uap4:CustomCapability Name="Microsoft.classicAppInstaller_8wekyb3d8bbwe" /> -->
    <uap4:CustomCapability Name="Microsoft.delegatedWebFeatures_8wekyb3d8bbwe" />
    <DeviceCapability Name="webcam" />
    <DeviceCapability Name="microphone" />
    <DeviceCapability Name="location" />
  </Capabilities>
  <Extensions>
<!--   注释掉与windows.customInstall有关的配置 
	  <desktop6:Extension Category="windows.customInstall">
      <desktop6:CustomInstall Folder="CustomInstall" desktop8:RunAsUser="true">
        <desktop6:RepairActions>
          <desktop6:RepairAction File="WsaSetup.exe" Name="Repair" Arguments="repair" />
        </desktop6:RepairActions>
        <desktop6:UninstallActions>
          <desktop6:UninstallAction File="WsaSetup.exe" Name="Uninstall" Arguments="uninstall" />
        </desktop6:UninstallActions>
      </desktop6:CustomInstall>
    </desktop6:Extension> -->
    <Extension Category="windows.activatableClass.proxyStub">
      <ProxyStub ClassId="76913B52-F9EB-4FAE-8DE7-24C20BDCF37B">
        <Path>WsaProxy\WsaProxy.dll</Path>
        <Interface Name="IWsaClient" InterfaceId="BC35C837-7915-45DE-AC1B-7A743AAD7188" />
      </ProxyStub>
    </Extension>
    ...
  </Extensions>
```