---
title: 分析網站活動和客戶轉換率
description: 了解如何設定控制面板來追蹤您的網站活動（包括頁面檢視、工作階段和使用者），以及一段時間內的客戶轉換率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# 分析網站活動

[!DNL MBI] 可讓您輕鬆整合廣告成本資料與其餘資料。 這不僅可讓您了解您的網站活動，還可讓您衍生出您網站上成為註冊使用者或進行購買的訪客百分比。

在本文中，我們示範如何設定控制面板來追蹤您的網站活動（包括頁面檢視、工作階段和使用者），以及一段時間內的客戶轉換率。

## 必要條件

**匯入廣告成本資料**  — 連接 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) to [!DNL MBI]  — 這會自動同步 [!DNL AdWords] 花在BI上。

**追蹤使用者贏取管道資料**  — 系結您的 [!DNL Google AdWords] 資料到資料庫中的特定訂單，我們需要 [追蹤使用者贏取](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]，可讓我們使用utm來源和媒體連線每個訂單。

## 使用者贏取促銷活動

此報告集合是使用下列項目建立：

* 在您連線時自動產生的量度 [!DNL Google AdWords] 資料
* 您帳戶上應已可用的基本量度，例如 `Number of orders` 和 `New users`
* Dimension在加入 [!DNL Google Analytics Ecommerce] 資料到資料庫，如訂單的utm源和訂單的utm介質。 如果您的帳戶中目前沒有這些欄位，請聯絡我們的支援團隊

## 建立報表

**首先，建立一份報表，顯示一段時間內的頁面檢視、工作階段和使用者數量：**

1. 建立新報表。
1. 按一下 **[!UICONTROL Add Metric]**，將滑鼠移至 [!DNL Google Analytics] 區段，然後選取 `Page Views`.
1. 新增其他量度，將滑鼠移到 [!DNL Google Analytics] 部分，此時選擇 `Sessions`.
1. 新增第三個量度，將滑鼠游標移到 [!DNL Google Analytics] 部分，此時選擇 `Users`.
1. 現在，將您的時段變更為移動範圍（從31天前變更為1天前），並將時間間隔調整為 `by day`.
1. 為報表命名(例如 `Page views, sessions and users by day`)，然後按一下 **[!UICONTROL Save]**.

**我們的第二份報告將審視過去一年的頁面檢視次數：**

1. 建立新報表。
1. 按一下 **[!UICONTROL Add Metric]**，將滑鼠移至 [!DNL Google Analytics] 區段，然後選取 _頁面檢視_.
1. 將時段變更為移動範圍（從13個月前變更為1個月前），並將時間間隔調整為 `by month`.
1. 為報表命名，例如 `Page views by month,` 和按一下 **[!UICONTROL Save]**.

**第三張圖表將顯示過去一年的反彈率：**

1. 建立新報表。
1. 按一下 **[!UICONTROL Add Metric]**，將滑鼠移至 [!DNL Google Analytics] 區段，然後選取 _反彈率_.
1. 將時段變更為移動範圍（從13個月前變更為1個月前），並將時間間隔調整為 `by month`.
1. 為報表命名，例如 `Bounce rate by month`，然後按一下 **[!UICONTROL Save]**.

**現在，請查看新訪客與再度訪問的訪客的平均工作階段長度：**

1. 建立新報表。
1. 按一下 **UICONTROL新增量度**，將滑鼠移至 [!DNL Google Analytics] 區段，然後選取 `Average Session Length`.
1. 將時段變更為移動範圍（從13個月前變更為1個月前），並將時間間隔調整為 `by month`?
1. 新增 `Group by` 選取 `New or returning visitor`.  檢查 `Show All` 框；然後按一下 **[!UICONTROL Apply]**.
1. 為報表命名，例如 `Average session length`，然後按一下 **[!UICONTROL Save]**.

**接下來，請查看您過去30天內排名最前的反向連結網域：**

1. 建立新報表。
1. 按一下 **[!UICONTROL Add Metric]**，將滑鼠移至 [!DNL Google Analytics] 區段，然後選取 `Sessions`.
1. 將時段變更為移動範圍（從31天前變更為1天前），並將時間間隔調整為 `none`.
1. 新增 `Group by` 選取 `ga:source`.  檢查 _全部顯示_ 框；然後按一下 **[!UICONTROL Apply]**.
1. 添加其他 `group by` 選取 `ga:medium`. 再次檢查 `Show All` 框；然後按一下 **[!UICONTROL Apply]**.
1. 為報表命名，例如 `Top 20 Referring Domains, 30 Days`，然後按一下 **[!UICONTROL Save]**.

**最後，請檢視轉換：**

1. 建立新報表。
1. 新增下列量度：

* `New users`
   * 按一下 **[!UICONTROL Hide]** 在量度名稱下方

* `Number of orders`
   * 新增篩選器 `Customer's order number` = 1，點按 **[!UICONTROL Apply]**
   * 按一下量度名稱並呼叫，以重新命名量度 `Number of first orders`，然後按一下 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 量度

* `Users`
   * **[!UICONTROL Hide]** 量度
   * 將時段變更為 `24 months ago to now`，將時間間隔調整為 `by month`.
   * 按一下，新增下列公式 **[!UICONTROL Formula]**.
   * A/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `Registration conversion`
   * B/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `First order conversion`
   * C/D，然後按一下 **[!UICONTROL Apply]**
   * 更名公式 `Any order conversion`

* 請為您的報表命名，例如 `Conversion by month`，然後按一下 **[!UICONTROL Save]**.

## 後續步驟

現在，您可以存取網路流量和轉換率上的資料，就可以開始挖掘這些資料以推動業務決策。 哪些網站最能促進網站流量？  哪些促銷活動最能有效吸引具有高存留價值的客戶？

當您調整廣告支出和行銷策略時，可以繼續追蹤 [!DNL MBI]，在此控制面板上重複執行，以符合貴公司不斷演變的優先順序。
