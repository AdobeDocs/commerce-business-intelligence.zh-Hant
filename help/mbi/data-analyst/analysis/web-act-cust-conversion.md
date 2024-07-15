---
title: 分析網站活動和客戶轉換率
description: 瞭解如何設定控制面板，追蹤網站活動（包括頁面檢視次數、工作階段和使用者），以及客戶在一段時間內的轉換率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# 分析網站活動

[!DNL Adobe Commerce Intelligence]可讓您輕鬆將您的廣告成本資料與您其餘的資料整合。 這不僅可讓您瞭解您的網站活動，也可讓您匯出網站上成為註冊使用者或進行購買的訪客百分比。

此主題示範如何設定控制面板來追蹤網站活動（包括頁面檢視次數、工作階段和使用者），以及客戶在一段時間內的轉換率。

## 必要條件

**匯入您的廣告成本資料** — 將[!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md)連線至[!DNL Adobe Commerce Intelligence] — 這會自動同步您[!DNL AdWords]在Commerce Intelligence中的支出。

**追蹤使用者贏取管道資料** — 若要將您的[!DNL Google AdWords]資料繫結至資料庫中的特定訂單，您必須[透過[!DNL Google Analytics E-commerce]追蹤使用者贏取](../analysis/google-track-user-acq.md)。 這可讓您以utm來源和中型來連線每個訂單。

## 使用者贏取行銷活動

這份報表的集合是以下列專案建立：

* 連線[!DNL Google AdWords]資料時自動產生的量度
* 基本量度應該已在您的帳戶中可用，例如`Number of orders`和`New users`
* 將[!DNL Google Analytics Ecommerce]資料加入資料庫時建立的Dimension，例如訂單的utm來源和訂單的utm媒體。 如果您的帳戶目前沒有這些欄位，請聯絡支援團隊

## 建立報告

**首先，建立顯示一段時間內頁面檢視、工作階段和使用者數量的報告：**

1. 建立報表。
1. 按一下&#x200B;**[!UICONTROL Add Metric]**，然後將滑鼠移至下拉式清單底部的[!DNL Google Analytics]區段，並選取`Page Views`。
1. 新增另一個量度，再次擱置[!DNL Google Analytics]區段，這次選取`Sessions`。
1. 新增第三個量度，再次繫結在[!DNL Google Analytics]區段中，這次選取`Users`。
1. 現在將您的時段變更為移動範圍，從31天前變更為1天前，並將時間間隔調整為`by day`。
1. 為您的報表命名（例如，`Page views, sessions and users by day`），然後按一下&#x200B;**[!UICONTROL Save]**。

**第二個報表會檢視過去一年中的頁面檢視次數：**

1. 建立報表。
1. 按一下&#x200B;**[!UICONTROL Add Metric]**，將滑鼠移至下拉式清單底部的[!DNL Google Analytics]區段，並選取&#x200B;_頁面檢視_。
1. 將您的時段變更為移動範圍，從13個月前變更為1個月前，並將時間間隔調整為`by month`。
1. 提供您的報表名稱，例如`Page views by month,`，然後按一下&#x200B;**[!UICONTROL Save]**。

**第三個圖表會檢視過去一年的反彈率：**

1. 建立報表。
1. 按一下&#x200B;**[!UICONTROL Add Metric]**，將滑鼠移至下拉式清單底部的[!DNL Google Analytics]區段，並選取&#x200B;_跳出率_。
1. 將您的時段變更為移動範圍，從13個月前變更為1個月前，並將時間間隔調整為`by month`。
1. 提供您的報表名稱，例如`Bounce rate by month`，然後按一下&#x200B;**[!UICONTROL Save]**。

**現在，檢視新訪客與回訪訪客相較之下的平均工作階段長度：**

1. 建立報表。
1. 按一下&#x200B;**UICONTROL新增量度**，將滑鼠移至下拉式清單底部的[!DNL Google Analytics]區段，然後選取`Average Session Length`。
1. 將您的時段變更為移動範圍（從13個月前變更為1個月前），並將時間間隔調整為`by month`？
1. 新增`Group by`並選取`New or returning visitor`。  核取`Show All`方塊；然後按一下&#x200B;**[!UICONTROL Apply]**。
1. 提供您的報表名稱，例如`Average session length`，然後按一下&#x200B;**[!UICONTROL Save]**。

**接下來，檢視您最近30天排名最前的反向連結網域：**

1. 建立報表。
1. 按一下&#x200B;**[!UICONTROL Add Metric]**，將滑鼠移至下拉式清單底部的[!DNL Google Analytics]區段，然後選取`Sessions`。
1. 將您的時段變更為移動範圍，從31天前變更為1天前，並將時間間隔調整為`none`。
1. 新增`Group by`並選取`ga:source`。  勾選「_全部顯示_」方塊；然後按一下「**[!UICONTROL Apply]**」。
1. 新增其他`group by`並選取`ga:medium`。 再次勾選`Show All`方塊；然後按一下&#x200B;**[!UICONTROL Apply]**。
1. 提供您的報表名稱，例如`Top 20 Referring Domains, 30 Days`，然後按一下&#x200B;**[!UICONTROL Save]**。

**最後，檢視轉換：**

1. 建立報表。
1. 新增下列量度：

* `New users`
   * 按一下量度名稱下方的&#x200B;**[!UICONTROL Hide]**

* `Number of orders`
   * 新增`Customer's order number` = 1的篩選器，然後按一下&#x200B;**[!UICONTROL Apply]**
   * 若要重新命名量度，請按一下該量度名稱，呼叫它`Number of first orders`，然後按一下&#x200B;**[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]**&#x200B;量度

* `Users`
   * **[!UICONTROL Hide]**&#x200B;量度
   * 將時段變更為`24 months ago to now`，並將時間間隔調整為`by month`。
   * 按一下&#x200B;**[!UICONTROL Formula]**&#x200B;以新增下列公式。
   * A/D，然後按一下&#x200B;**[!UICONTROL Apply]**
   * 重新命名公式`Registration conversion`
   * B/D，然後按一下&#x200B;**[!UICONTROL Apply]**
   * 重新命名公式`First order conversion`
   * C/D，然後按一下&#x200B;**[!UICONTROL Apply]**
   * 重新命名公式`Any order conversion`

* 現在為您的報告命名，例如`Conversion by month`，然後按一下&#x200B;**[!UICONTROL Save]**。

## 後續步驟

現在您可以存取有關網站流量和轉換率的資料，您可以開始發掘這些資料以推動業務決策，例如哪些網站最能帶來您網站的流量？ 或您的哪些行銷活動最能有效吸引終身價值高的客戶？

當您調整廣告支出和行銷策略時，您可以繼續追蹤[!DNL Commerce Intelligence]中的結果，在此控制面板上反複追蹤，以符合貴公司不斷變化的優先順序。
