---
layout: post
title: "Google 拼音输入法 Android 版 MOD v3"
date: 2011-02-03 14:44
comments: true
categories: [Android, Google Pinyin, smali, hacking]
---

前段时间入手 T-Mobile G2 之后把 Google 拼音输入法升级到了在 G1 上跑起来慢吞吞的最新版，结果遇到各种小问题用得很不爽，一怒之下抄起家伙把它狠狠改了一通。虽然还有些小问题，但影响没那么严重就暂时懒得管了。

懒得另外写说明了，直接引用 [GitHub repo](https://github.com/rainux/com.google.android.inputmethod.pinyin) 里的 README 吧。

## 目的 ##

使用 [apktool](http://code.google.com/p/android-apktool/) 对 Google 拼音输入法 Android 版进行反向工程[注1]，在 Dalvik JVM 汇编层级微调修改它，使其更适合日常使用。

注1：实际上不是真正完整的反向工程，后来有大量借助 [Android Open Source Project](http://source.android.com/) 中 Google 拼音输入法 1.0.0 的 Java 源代码理解反汇编得到的 smali 代码。

## 问题修正 ##

* 中文模式下硬件键盘上某些标点符号没有被正确映射为中文（全角）形态，尤其是在 T-Mobile G2 上。
* 中文模式下在软键盘未初始化时使用硬件键盘 Enter 键会导致 Google 拼音崩溃。
* 中文模式下软键盘上的圆括号不是中文（全角）形态。
* 软键盘上的 & 和 < 符号被不正确地转义成了 \&amp; 和 \&lt;。（MOD 版引入的问题。）
* 中文模式下软键盘在空闲状态时 Del 不能删除字符。（MOD 版引入的问题。）

## 细节改进 ##

* 中文模式空闲和联想状态下 Alt + Del 像系统默认行为一样删除当前行。
* 中文模式选字状态下 Alt + Del 删除所有拼音字符并回到空闲状态。
* 中文模式下回到空闲状态以及空闲状态输入字符后重置 Alt 和 Shift 状态，避免使用 Del 修正输入内容时误删当前行。（MOD 版引入的不便。）
* 中文模式下硬件键盘 _ （下划线）映射为—（半个破折号），`（反单引号）映射为·（英文人名分隔符）。

## 如何使用 ##

下载 [Google 拼音输入法 1.3.4 MOD v3](https://github.com/downloads/rainux/com.google.android.inputmethod.pinyin/Google_Pinyin_IME_v1.3.4_MOD_v3.apk)，使用 adb 工具或 Android 的 Package Manager 安装。或者 git clone 此 smali 源代码仓库自己用 apktool 编译生成 .apk 文件。

注意：**安装 MOD 版本之前必须先卸载官方版本，这是因为 MOD 版本签名所使用的证书不可能与官方版本一致。**

## 感谢 ##

* @[pipitu](http://twitter.com/pipitu): 在我头昏眼花犯下低级错误的时候帮我查阅 smali 资料，让我得以“拨云见日醍醐灌顶茅塞顿开遍体舒畅的神一般的展开”。
