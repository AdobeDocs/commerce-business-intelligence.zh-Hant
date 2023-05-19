---
title: 分析網站活動和客戶折換率
description: 瞭解如何設定儀表板來跟蹤您的網站活動（包括頁面視圖、會話和用戶）以及客戶隨時間的轉換率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 分析網站活動

[!DNL Adobe Commerce Intelligence] 允許您輕鬆將廣告成本資料與其餘資料整合。 這不僅使您能夠瞭解您的網站活動，還使您能夠得出您網站上成為註冊用戶或進行購買的訪問者的百分比。

本主題演示了如何設定儀表板來跟蹤您的網站活動（包括頁面視圖、會話和用戶）以及客戶隨時間的轉換率。

## 先決條件

**導入廣告成本資料**  — 連接 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) 至 [!DNL Adobe Commerce Intelligence]  — 這會自動同步 [!DNL AdWords] 花在商業情報上。

**跟蹤用戶獲取通道資料**  — 系上 [!DNL Google AdWords] 資料到資料庫中的特定訂單， [跟蹤用戶獲取](../analysis/google-track-user-acq.md) 通過 [!DNL Google Analytics E-commerce]。 這允許您將每個訂單與utm源和介質連接。

## 用戶購買活動

此報告集合使用以下方法構建：

* 連接時自動生成的度量 [!DNL Google AdWords] 資料
* 您的帳戶上應已提供的基本度量，例如 `Number of orders` 和 `New users`
* Dimension在加入 [!DNL Google Analytics Ecommerce] 資料到資料庫，如訂單的utm源和訂單的utm介質。 如果帳戶中當前沒有這些欄位，請與支援團隊聯繫

## 生成報告

**首先建立一個報告，其中顯示一段時間內的頁面視圖、會話和用戶數：**

1. 建立報告。
1. 按一下 **[!UICONTROL Add Metric]**，然後將滑鼠移到 [!DNL Google Analytics] 下拉框底部的部分，然後選擇 `Page Views`。
1. 添加另一個度量，再次將滑鼠移過 [!DNL Google Analytics] 節，此時選擇 `Sessions`。
1. 添加第三個度量，再次將滑鼠移過 [!DNL Google Analytics] 節，此時選擇 `Users`。
1. 現在，將您的時間段更改為移動範圍，從31天前更改為1天前，並將時間間隔調整為 `by day`。
1. 給您的報表命名(例如， `Page views, sessions and users by day`)，然後按一下 **[!UICONTROL Save]**。

**第二份報告將查看過去一年的頁面視圖數：**

1. 建立報告。
1. 按一下 **[!UICONTROL Add Metric]**，滑鼠懸停在 [!DNL Google Analytics] 下拉框底部的部分，然後選擇 _頁面視圖_。
1. 將時間段更改為移動範圍（從13個月前更改為1個月前），並將時間間隔調整為 `by month`。
1. 給你的報告取個名字，比如 `Page views by month,` 按一下 **[!UICONTROL Save]**。

**第三張圖表是對過去一年的反彈率：**

1. 建立報告。
1. 按一下 **[!UICONTROL Add Metric]**，滑鼠懸停在 [!DNL Google Analytics] 下拉框底部的部分，然後選擇 _彈跳率_。
1. 將時間段更改為移動範圍（從13個月前更改為1個月前），並將時間間隔調整為 `by month`。
1. 給你的報告取個名字，比如 `Bounce rate by month`，然後按一下 **[!UICONTROL Save]**。

**現在，看看新訪客與回訪訪客相比的平均會話時間：**

1. 建立報告。
1. 按一下 **UICONTROL添加度量**，滑鼠懸停在 [!DNL Google Analytics] 下拉框底部的部分，然後選擇 `Average Session Length`。
1. 將時間段更改為移動範圍（從13個月前更改為1個月前），並將時間間隔調整為 `by month`?
1. 添加 `Group by` 選擇 `New or returning visitor`。  檢查 `Show All` 框；按一下 **[!UICONTROL Apply]**。
1. 給你的報告取個名字，比如 `Average session length`，然後按一下 **[!UICONTROL Save]**。

**接下來，查看過去30天中您的頂級引用域：**

1. 建立報告。
1. 按一下 **[!UICONTROL Add Metric]**，滑鼠懸停在 [!DNL Google Analytics] 下拉框底部的部分，然後選擇 `Sessions`。
1. 將時間段更改為移動範圍（從31天前更改為1天前），並將時間間隔調整為 `none`。
1. 添加 `Group by` 選擇 `ga:source`。  檢查 _全部顯示_ 框；按一下 **[!UICONTROL Apply]**。
1. 添加其他 `group by` 選擇 `ga:medium`。 再次，檢查 `Show All` 框；按一下 **[!UICONTROL Apply]**。
1. 給你的報告取個名字，比如 `Top 20 Referring Domains, 30 Days`，然後按一下 **[!UICONTROL Save]**。

**最後，看一下轉換：**

1. 建立報告。
1. 添加以下度量：

* `New users`
   * 按一下 **[!UICONTROL Hide]** 在度量名稱下

* `Number of orders`
   * 添加篩選器 `Customer's order number` = 1，按一下 **[!UICONTROL Apply]**
   * 通過按一下度量名稱並調用該度量來更名該度量 `Number of first orders`，然後按一下 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 度量

* `Users`
   * **[!UICONTROL Hide]** 度量
   * 將時間段更改為 `24 months ago to now`，將時間間隔調整為 `by month`。
   * 通過按一下 **[!UICONTROL Formula]**。
   * A/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `Registration conversion`
   * B/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `First order conversion`
   * C/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `Any order conversion`

* 給你的報告取個名字，比如 `Conversion by month`，然後按一下 **[!UICONTROL Save]**。

## 後續步驟

現在，您可以訪問Web流量和轉換率上的資料，您可以開始挖掘這些資料來推動業務決策，例如哪些站點最擅長將流量傳送到您的站點？ 或者，您的哪些活動在獲得具有高生命週期價值的客戶方面最有效？

在調整廣告支出和營銷策略時，您可以繼續跟蹤 [!DNL Commerce Intelligence]，在此控制板上迭代以滿足您公司不斷變化的優先順序。
