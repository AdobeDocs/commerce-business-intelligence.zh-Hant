---
title: 根據指標跟蹤目標
description: 瞭解如何設定儀表板，幫助您根據實際資料跟蹤業務目標 — 包括收入、新註冊用戶和隨時間推移的訂單。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 根據效能指標跟蹤目標

大多數客戶都想跟蹤 **業務目標**&#x200B;但是沒意識到這在 [!DNL Adobe Commerce Intelligence]。 本主題演示了如何設定儀表板，以幫助您根據實際資料跟蹤業務目標 — 包括收入、新註冊用戶和隨時間推移的訂單。 您還將學習如何將年與年的績效進行比較，所有這些都位於這樣的儀表板中：

![](../../assets/Goals-_dashboard_2.png)

在開始之前，您應查看 [檔案上載程式](../importing-data/connecting-data/using-file-uploader.md) 並確保您已定義了給定時間段的業務目標。

## 入門

您需要首先上載包含特定業務的每日/每月/季度目標的檔案。

您可以使用 [檔案上載程式](../importing-data/connecting-data/using-file-uploader.md) 和下面的影像來格式化檔案。 客戶端跟蹤的最常見目標 [!DNL Commerce Intelligence] 包括訂單、收入和新註冊帳戶。

![](../../assets/Goals-_Excel.png)

## 度量

為每個目標建立一個新度量。 例如，如果您載入每月收入和訂單目標，則需要建立兩個新指標：

* **月收入目標**
* 在 **`Monthly goals`** 表
* 此度量執行 **和**
* 在 **`Revenue target`** 列
* 按 **`Month`** 時間戳

* **每月訂單目標**
* 在 **`Monthly goals`** 表
* 此度量執行 **和**
* 在 **`Orders target`** 列
* 按 **`Month`** 時間戳

* **每月新註冊帳戶目標**
* 在 **`Monthly goals`** 表
* 此度量執行 **和**
* 在 **`New registered accounts target`** 列
* 按 **`Month`** 時間戳

## 報告

分析目標時，將靜態值和可視圖表混合在一起是很有幫助的。 下面是三個示例報告，幫助您開始跟蹤收入表現。

* **剩餘收入實現目標**
* 度量 `A`: `Revenue`
* 

   [!UICONTROL度量]: `Revenue`

* 度量 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL公式]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]:（不管您想要什麼時間段）
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL圖表類型]: `Scalar`

* **收入目標**
* 度量 `A`: `Revenue`
* 

   [!UICONTROL度量]: `Revenue`

* 度量 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 度量 `C`: `Revenue (amount change since previous year)` （隱藏）
* 
   [!UICONTROL度量]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]:（去年本月）
* 
   [!UICONTROL公式]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* 關閉 `Multiple Y-Axes`
* [!UICONTROL Time period]:（不管您需要什麼相關時間段）*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

完成上述收入目標報表後，您可以建立與訂單、註冊帳戶或目標檔案上載中包含的任何其它值相關的目標相同的報表。

編譯完所有報告後，可以根據需要在儀表板上組織這些報告。 結果可能與此頁頂部的影像類似。
