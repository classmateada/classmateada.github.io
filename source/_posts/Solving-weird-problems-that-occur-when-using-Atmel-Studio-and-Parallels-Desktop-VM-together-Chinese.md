---
title: >-
  解决在 Parallels Desktop 虚拟机中使用 Microchip Studio 时出现的问题（中文版）
lang: zh
date: 2023-09-14 23:05:48
tags:
  - 汇编语言
  - AVR 汇编
  - Parallels Desktop
categories:
  - Troubleshooting
---

## 问题的背景

这学期选了一门以讲解 AVR 汇编为主的课，在实验课中需要用到 `Microchip Studio`（也称 `Atmel Studio`）编写、调试 AVR 汇编程序。由于我平常使用的操作系统是 macOS，但这个软件只支持 Windows，所以我需要通过虚拟机使用这个软件。

我使用我最常用的虚拟机软件 `Parallels Desktop` 官方提供的创建 Windows 11 虚拟机的向导程序（`Get Windows 11 from Microsoft`）创建了一个 Windows 11 虚拟机，并成功地在虚拟机中安装了 Microchip Studio。但是，在完成安装并开始使用 Microchip Studio 时，我遇到了一些奇怪的问题。

## 问题的表现

### 启动时弹出警告框

每次启动 Microchip Studio 都会弹出如下图所示的警告框：

![警告框](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915000402.png)

### 界面布局怪异

Microchip Studio 的布局与其他 Windows PC 上运行的不一样。

正常界面布局如下：

![正常布局](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915003845.png)

此时的错误界面布局如下：

![错误布局](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915001655.png)

### 构建解决方案时不输出内存占用信息

创建 `ATmega2560` 汇编项目后，正常情况下每次构建都会输出程序的内存占用信息，但此时尝试构建并不会输出任何信息。

正常构建输出如下：

![正常构建输出](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915003745.png)

此时的错误构建输出如下：

![错误构建输出](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915001847.png)

### 断点工作不正常

调试时，Microchip Studio 会忽略用户设置的断点并自行插入新的断点。

我们在 `mov c, a` 这一行（第 20 行）下断点，在开始调试后程序应该停在断点处，但开始调试后却发现断点被自动修改为 `ldi a, 10` 这一行（第 16 行），并且在调试过程中无法向除了该行之外的其他行添加断点。

开始调试前的断点情况如下，可以看到断点打在 `mov c, a` 处：

![开始调试前的断点情况](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915002409.png)

开始调试后的断点情况如下，可以看到断点被自动修改到 `ldi a, 10` 处：

![开始调试后的断点情况](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915002544.png)

## 如何解决这些问题

### 重置为默认配置

点击菜单栏中的 `Tools` - `Import and Export Settings...`，选择 `Reset all settings` 并点击 `Next >`，选择 `Yes, save my current settings` 并在 `Store my settings file in this directory:` 输入框中指定一个 Windows 11 虚拟机内部的目录（如 `C:\Visual Studio 2015\Settings\Microchip Studio`），点击 `Finish`，如果弹出警告框则选择 `Yes`。如图所示。

![重置配置 1](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915002751.png)

![重置配置 2](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915003133.png)

重启 Microchip Studio，可以发现之前每次启动都弹出的警告框消失了。

### 重新创建项目

此时断点问题和没有内存输出的问题仍然存在，我们需要重建项目来解决这个问题。重新创建一个项目，并在 `Location:` 输入框中指定一个 Windows 11 虚拟机内部的目录（如 `c:\users\adamagnus\Documents\Microchip Studio\7.0`），如图所示。

![新建项目](https://cdn.jsdelivr.net/gh/classmateada/site-pictures/img/20230915031044.png)

在这个新项目中重新编写代码并尝试构建和调试，会发现断点问题和没有内存输出的问题全部消失了。

## 造成问题的原因

Parallels Desktop 出于方便使用的目的，将宿主机 macOS 的文件系统在 Windows 虚拟机中映射为一个可以通过 SMB 协议访问的**网络地址**，并对虚拟机中的大部分软件默认提供 macOS 文件系统的目录作为文件保存路径。但是 Microchip Studio 无法识别网络地址，也就无法在启动时找到安装时提供的默认配置文件，于是使用默认配置启动，这就导致了上述的一系列问题。

同理，如果将项目保存到 macOS 文件系统中的某个目录，Microchip Studio 在构建该项目时会出现问题，进而导致无法输出内存占用信息和断点功能异常。

## 附录1：问题排查过程

1. 排除项目本身的问题：我新建了一个项目并把代码复制粘贴进去，没有解决问题。
2. 排除代码的问题：修改新建的项目的代码为 Microchip Studio 创建项目时的默认代码，没有解决问题。
3. 排除操作系统版本的问题：尝试使用其他 Windows 11 和相同版本的 Microchip Studio 创建相同的配置、编写相同的代码，发现在其他 Windows 11 上没有出现任何问题。
4. 排除虚拟机和软件安装的问题：新建一个空的 Windows 11 虚拟机，重新安装 Microchip Studio，发现界面布局仍然很诡异，问题仍然没有解决。
5. 解决警告框、重置配置：注意到在新的虚拟机上安装的 Microchip Studio 仍然在每次打开时弹出警告框，于是尝试解决这个警告框。在通过重置配置并将配置文件保存到虚拟机的文件系统中后，问题解决。

## 附录2：问题复现步骤

1. 使用 Parallels Desktop 创建一个 Windows 11 虚拟机。
2. 在虚拟机中安装最新版本的 Microchip Studio。
3. 运行 Microchip Studio，在弹出警告框时点击 `OK`。
4. 创建一个汇编语言项目，设备选择 `ATmega2560`。
5. 尝试构建和断点调试该项目。
