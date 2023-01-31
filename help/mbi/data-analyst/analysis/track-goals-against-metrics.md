---
title: 根據量度追蹤目標
description: 了解如何設定控制面板，協助您根據實際資料（包括收入、新註冊使用者和訂單）追蹤業務目標。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 根據績效量度追蹤目標

我們的大部分客戶通常都想追蹤他們的 **業務目標**，但不會意識到這在 [!DNL MBI]. 在本文中，我們示範如何設定控制面板，協助您根據實際資料（包括收入、新註冊使用者和訂單）追蹤業務目標。 我們也會示範如何比較逐年績效，所有這些都在控制面板中，如下所示：

![](../../assets/Goals-_dashboard_2.png)

開始之前，請熟悉 [檔案上傳程式](../importing-data/connecting-data/using-file-uploader.md) 並確保已定義指定時段的業務目標。

## 快速入門

您必須先上傳包含貴公司特定每日/每月/每季目標的檔案。

您可以使用 [檔案上傳程式](../importing-data/connecting-data/using-file-uploader.md) 和下面的影像，以設定檔案格式。 我們客戶追蹤的最常見目標 [!DNL MBI] 包括訂購、收入和新註冊帳戶。

![](../../assets/Goals-_Excel.png)

## 量度

您必須為每個目標建立一個新量度。 例如，如果您上傳每月收入和訂單目標，則需要建立兩個新量度：

* **每月收入目標**
* 在 **`Monthly goals`** 表格
* 此量度會執行 **總和**
* 在 **`Revenue target`** 欄
* 由 **`Month`** timestamp

* **每月訂單目標**
* 在 **`Monthly goals`** 表格
* 此量度會執行 **總和**
* 在 **`Orders target`** 欄
* 由 **`Month`** timestamp

* **每月新註冊帳戶目標**
* 在 **`Monthly goals`** 表格
* 此量度會執行 **總和**
* 在 **`New registered accounts target`** 欄
* 由 **`Month`** timestamp

## 報表

一如既往，在分析目標時，混合使用靜態值和視覺化圖表會很有幫助。 以下是三個範例報表，可協助您開始追蹤收入績效。

* **剩餘收入用於實現目標**
* 量度 `A`: `Revenue`
* 

   [!UICONTROL量度]: `Revenue`

* 量度 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL公式]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]:（您想要的任何相關時段）
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **收入目標**
* 量度 `A`: `Revenue`
* 

   [!UICONTROL量度]: `Revenue`

* 量度 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 量度 `C`: `Revenue (amount change since previous year)` （隱藏）
* 
   [!UICONTROL量度]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]:（去年這個月）
* 
   [!UICONTROL公式]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* 關閉 `Multiple Y-Axes`
* [!UICONTROL Time period]:（不管您想要什麼相關時段）*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

完成上述收入目標報表後，您就可以針對訂單、註冊帳戶或目標檔案上傳中包含的任何其他值，建立相同的目標報表。

編譯所有報表後，您可以視需要在控制面板上組織報表。 最終結果看起來可能像此頁面頂端的影像。
