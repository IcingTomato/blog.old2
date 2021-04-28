---
layout: post
title: "How to Use Powershell to configure Docker on Windows Server 2016"
description: "Powershell is useless."
comments: false
keywords: "Docker, Windows, Windows Server, Powershell, Windows Server 2016"
---

# Enabled TLS1.2 in Powershell for downloading repositories

TLS 1.0 is a security protocol first defined in 1999 for establishing encryption channels over computer networks. Microsoft has supported this protocol since Windows XP/Server 2003. While no longer the default security protocol in use by modern OSes, TLS 1.0 is still supported for backwards compatibility. Evolving regulatory requirements as well as new security vulnerabilities in TLS 1.0 provide corporations with the incentive to disable TLS 1.0 entirely.

So first of all, you should enabled the TLS1.2 in Powershell. 

Windows PowerShell uses .NET Framework 4.5, which does not include TLS 1.2 as an available protocol. To work around this, two solutions are available:

```shell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```
Or
```shell
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:64
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:32
```

Solutions (1) and (2) are mutually-exclusive, meaning they need not be implemented together. I recommand using the Solutions (1).

# Get the latest version from PowerShell Gallery

Before updating PowerShellGet , you should always install the latest NuGet provider. From an elevated PowerShell session, run the following command.

```shell
Install-PackageProvider -Name NuGet -Force
Install-Module -Name PowerShellGet -Force
```

# Install Docker

Docker is required in order to work with Windows containers. Docker consists of the Docker Engine and the Docker client.


Install the OneGet PowerShell module.
```shell
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
```

Use OneGet to install the latest version of Docker and enable the Hyper-V feature.
```shell
Install-Package -Name docker -ProviderName DockerMsftProvider
Install-WindowsFeature hyper-v
```
When the installation is complete, reboot the computer.
```shell
Restart-Computer -Force
```

# Install base container images

Before working with Windows containers, a base image needs to be installed. Base images are available with either Windows Server Core or Nano Server as the container operating system. For detailed information on Docker container images, see [Build your own images on docker.com](https://docs.docker.com/engine/tutorials/dockerimages/).

First of all, we should enable the Docker Daemon process.
```shell
cd "C:\Program Files\Docker"
.\dockerd.exe
```

Then open another Powershell window as Administrator, I used the Windows Server 2016 Version 1607.\

To install the 'Windows Server Core' base image run the following:
```shell
docker pull mcr.microsoft.com/windows/servercore:1607
```

To install the 'Nano Server' base image run the following:
```shell
docker pull mcr.microsoft.com/windows/nanoserver:1607
```

![](//panzhifei.fun/img/2021/04/20/01/01.jpg)

# Links

[Solving the TLS 1.0 Problem, 2nd Edition](https://docs.microsoft.com/en-us/security/engineering/solving-tls1-problem)

[Installing PowerShellGet (zh-cn available)](https://docs.microsoft.com/zh-cn/powershell/scripting/gallery/installing-psget?view=powershell-7.1)

[Container host deployment: Windows Server (zh-cn available)](https://docs.microsoft.com/zh-cn/virtualization/windowscontainers/deploy-containers/deploy-containers-on-server)
