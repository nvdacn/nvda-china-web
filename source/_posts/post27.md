---
title: nvwave:音频播放及音频设备控制模块
date: 2016-06-01 15:34
tags:
more: 详细阅读
---
提供一个简单的python界面，通过windows 多媒体 waveOut函数播放音频，也可作为实用的音频工具。
下面介绍这个模块所包含的类和方法：
## WavePlayer：类，同步播放一个音频流 
用法：构建一个实例，并使用 feed 嵌入波形格式音频。
## _winmm_errcheck，初始化错误检测。 
## __init__：初始化。 
参数：
channels：音频声道数量（整数），如1声道为单声道，2声道为立体声等。
samplesPerSec：每秒采样数（整数，单位为HZ）
bitsPerSample: 每秒比特率（整数）
outputDevice: 设备 ID 或所使用的输出设备的名称（整数或字串）
closeWhenIdle: 如果为 True，没有音频输出时关闭音频设备（
wantDucking: 如果为 True，windows8以上的系统的背景音量将会被降低
注释：如果 outputDevice所包含的设备名称不存在，将使用默认设备
触发WindowsError: 如果出现错误则打开音频输出设备
## open:打开音频设备，如果需要，他可被自动调用。 
## feed：提供一块音频数据以供播放之用，通常这会与上一音频块同步，如在没有音频播放的时候调用，它会在上一个音频播放结束之后马上播放所调用的音频块，且会立马返回。通常这可用来无缝的串接音频块的播放 
参数：
data: 构建实力时所指定格式的波形音频（字符串）
触发WindowsError: 播放音频时出错
## sync：与回放同步，直到上一段音频播放完毕之前此方法都处于锁定状态 
它会被L{feed}自动调用，所以，通常情况下用户无需直接调用。
## pause：函数，暂停或取消暂停回放 
参数：
switch： 为 True 时暂停播放，为 False时取消暂停
## idle：显示播放器的空闲状态，极音频播放完毕后的状态。它会先调用 sync 与回放同步。如果 closeWhenIdle 为 True，输出设备将会被关闭。如果与 feed 同时调用将重开音频设备。 
## stop：函数，停止回放。在某些系统下，先暂停或可使得waveOutReset的响应速度变得更快。waveOutReset在某些系统可能会造成随机错误。如果设备被占用，取消上一次缓冲的预处理并关闭播放设备。 
## close，函数，关闭播放设备。 
## _getOutputDevices，获取输出设备，某些情况下，windows所包含的设备不可访问 
## getOutputDeviceNames：获取所有输出设备的名称。返回值是所有输出设备的名称。 
## outputDeviceIDToName：获取给定ID所属设备的名称。 
参数：ID：设备ID（整数）
返回值：设备名称（字符串）
## 、outputDeviceNameToID：获取给定名称所属设备的ID。 
参数：name，设备名称（字符串）
useDefaultIfInvalid： 为 True}时，使用默认设备，为 False时触发exception
返回值：设备ID（整数）
触发LookupError：如果 useDefaultIfInvalid 为 False 且没有所调用的设备则触发