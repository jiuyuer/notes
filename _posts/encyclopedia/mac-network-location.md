---
title: 如何在 Mac 上使用网络位置
tags:
  - Mac
  - 网络位置
categories:
  - 百科全书
date: 2018-06-17 13:28:08
---

> 借助“网络”偏好设置中的“位置”功能，您可以在不同的网络设置组之间快速切换。

在不同的网络设置组（位置）之间切换的功能在以下情况下非常有用：

- 您在工作场所和家中使用相同类型的网络（如以太网），但在工作场所使用的设置不允许您的 Mac 自动连接到家中所用的相同类型网络。
- 您的 Mac 在工作场所和家中连接到多种类型的网络服务（如 Wi-Fi 和以太网），但是，在工作场所，您希望您的 Mac 先尝试连接到以太网网络，而在家中，则希望先尝试连接到 Wi-Fi 网络。换言之，您希望针对每个位置设置不同的服务顺序。
- 您的 Mac 无法连接到网络，并且您想要快速重设您的网络设置以用于测试，同时不丢失当前的网络设置。

在上述每个示例中，“网络”偏好设置中的“位置”功能均可发挥作用。以下步骤适用于使用 [OS X v10.6 或更高版本的](https://support.apple.com/zh-cn/HT201260) Mac 电脑。

---

## 如何创建新的网络位置

1.  选取苹果菜单 () >“系统偏好设置”，然后点按“网络”。
2.  “位置”弹出式菜单中会显示您当前所选网络设置组的名称。默认位置名称为“自动”。从该菜单中选取“编辑位置”。
    ![](/images/baike/macos-sierra-system-preferences-network-location-edit.png)

3.  此时，将打开一个位置对话框。点按位置列表下方的 “添加”按钮，然后为新位置键入一个名称，如“工作”或“家庭”或“移动”：
    ![](/images/baike/macos-sierra-system-preferences-network-location-edit-2.png)
4.  点按“完成”。“位置”菜单现在应显示新位置的名称。点按“应用”后，您对网络设置所做的全部更改都将存储到该位置。您之前位置中的网络设置在您离开时会保留，因此您可以随时切换回来。
5.  点按“应用”以存储您的设置，并从之前的位置切换到新的位置。您的 Mac 会自动尝试为每种类型的网络确定正确的设置。如果您需要进一步调整设置，请记得再次点按“应用”。如果您的新设置不允许您连接到您的网络，请点按“向导”。

<!-- more -->

---

## 如何在网络位置之间进行切换

如果您有多个位置，您可以使用以下任一方法在这些位置之间进行切换：

- 如上文所述，请使用“网络”偏好设置中的“位置”弹出式菜单。选择位置后请记得点按“应用”。
- 或者从菜单栏中选取苹果菜单 >“位置”，然后从子菜单中选取您的位置。

---

## 如何更改网络服务顺序

如果您正在使用网络位置，而您希望每个位置在连接时首选不同的网络服务（如 Wi-Fi 或以太网），请按照以下步骤更改每个位置中的服务顺序（也称为“端口优先顺序”）。

1.  选取苹果菜单 >“系统偏好设置”，然后点按“网络”。
2.  使用“位置”菜单来选取想要修改的位置。
3.  点按服务列表下方的 “操作”菜单，然后选取“设置服务顺序”。
4.  拖动列表中的服务以更改其顺序。您的 Mac 将先尝试连接列表顶部的服务，然后继续按降序连接，直到连接成功。
    > 虚拟专用网络 (VPN) 连接不能重新排序，因为它们始终优先于其他连接。
    > ![](/images/baike/macos-sierra-system-preferences-network-set-service-order.png)
5.  点按“好”，然后点按“应用”，以激活更新的服务顺序。

---

## 如何阻止使用某个网络服务

默认情况下，名为“自动”的位置可激活所有可用网络（也称为“端口”或“网络接口”），无论它们是否用于连接到网络。您的 Mac 将自动搜索这些服务以进行网络或互联网连接。例如，您可能会在家中使用 Wi-Fi 网络而在工作场所使用以太网网络。您的 Mac 在连接时会自动检测要使用哪个网络服务。

如果您想要确保您的 Mac 不使用某个特定网络服务（如 Wi-Fi），您可以在您的所有网络位置停用该服务：

1.  选取苹果菜单 >“系统偏好设置”，然后点按“网络”。
2.  使用“位置”菜单来选取想要修改的位置。
3.  点按服务列表下方的 <span id="style">![](/images/baike/elcapitan-system-preferences-gear-icon.png)</span>“操作”菜单，然后选取“停用服务”。
4.  点按“应用”。

<style>
#style a{
  cursor: default;
  border-bottom:none;
}
#style img{
  display:inline !important;
  width:22px; height:14px;
  margin: 0;
  padding: 0;
  border: none;
}
</style>
