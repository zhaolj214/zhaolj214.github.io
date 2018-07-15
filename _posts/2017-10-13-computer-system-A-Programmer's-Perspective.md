---
layout: post
title:  "深入理解计算机系统"
date:   2017-10-13 15:14:54
categories: operating system 
tags: OS [operating system]
desciption: computer system A Programmer's Perspective[second edition] 
 
---

* content
{:toc}



## 第二章 ##


### 2.1 信息存储 ###
#### 2.1.1 十六进制表示法 ####

当值x可表示为2的非负整数n次幂时，**x=2<sup>n</sup>**，x的二进制表示形式为1后面跟着n个零。当n表示成`n=i+4j(0≤i≤3)`的形式时，
我们可以把x写成开头的十六进制数字为1(i=0)、2(i=1)、4(i=2)、8(i=3)，后面跟随j个零。例如：x=2048=2<sup>11</sup>，其中n=11=3+4×2
，从而得到十六进制数0x800。

<table>
    <tr>
        <th>n</th>
        <th>2<sup>n</sup>十进制</th>
        <th>2<sup>n</sup>十六进制</th>
    </tr>
    <tr>
        <th>9</th>
        <th>512</th>
        <th>0x200</th>
    </tr>
    <tr>
        <th>19</th>
        <th>1048576</th>
        <th>0x80000</th>
    </tr>
    <tr>
        <th>14</th>
        <th>16384</th>
        <th>0x400</th>
    </tr>
    <tr>
        <th>16</th>
        <th>65535</th>
        <th>0x10000</th>
    </tr>
    <tr>
        <th>17</th>
        <th>131072</th>
        <th>0x20000</th>
    </tr>
    <tr>
        <th>5</th>
        <th>32</th>
        <th>0x20</th>
    </tr>
    <tr>
        <th>7</th>
        <th>128</th>
        <th>0x80</th>
    </tr>
</table>

