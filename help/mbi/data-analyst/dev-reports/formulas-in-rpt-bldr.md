---
title: Report Builder中的公式
description: 瞭解公式如何在Report Builder中使用。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# `Report Builder`中的公式

在[`Report Builder`](../../tutorials/using-visual-report-builder.md)中，您可以使用帳戶中的[定義量度](../../data-user/reports/ess-manage-data-metrics.md)來建立強大的視覺效果。 在公式中組合這些量度，可讓您從資料中取得其他深入分析。 本主題探討如何在`Report Builder`中使用公式 — 讓您可以跳入！

## 什麼是`formula`？ {#what}

在`Report Builder`中，`formula`只是根據某些數學邏輯的一或多個量度的組合。 典型的範例看起來像這樣：

![](../../assets/formula-example.png)

在此範例中，您使用`Number of orders metric (A)`和`Distinct buyers metric (B)`，目標是回答以下問題：我的買家每個月平均訂購數是多少？ 公式的引數為：

* `Definition`：在這裡，您對輸入量度套用數學。 在此範例中，將訂單數除以不同的買家數，可得出平均訂單數。 因此，定義為(A/B)。

* `Format`：您的公式是否傳回數字、時段或貨幣金額？ 公式定義旁有一個下拉式清單，可用來指定傳回的格式。 在此範例中，它是一個數字。

* `Miscellaneous`：公式的時間戳記、群組、透視和篩選器均由其輸入量度繼承。 這裡沒有任何可執行的動作！

## 如何在我的報告中使用`formulas`？ {#how}

您已涵蓋基本知識，請檢視一些範例。

### 範例：我想瞭解我的收入中有多少百分比可歸屬於首次訂單。

![使用公式來尋找首次訂購的收入百分比](../../assets/first_time_orders.gif)

在此範例中，您使用了`Revenue`和`Revenue (first time orders)`量度。 將`Revenue (first time orders)(B)`量度除以`Revenue metric (A)`，並將傳回格式設定為`Percent`，即可找出可歸因至首次訂購的收入百分比。

### 範例：我想知道在這樣做和不提供`promo code`時，每份訂單的平均收入是多少。

![使用公式來尋找有促銷代碼和無促銷代碼的每份訂單的平均收入](../../assets/promo_code.gif)

在此範例中，您使用了`Revenue`和`Number of orders`量度。 此問題的答案包含兩個步驟 — 將`Revenue (A)`除以`Number of orders (B)`並將傳回格式設定為`Currency`。 接著，您僅允許公式結果(`Avg. Revenue per order`)顯示結果並依`Promo code`分組。

### 範例：我想瞭解新客戶的UTM來源的分佈。

![使用公式來尋找新客戶的UTM來源的分佈](../../assets/distro.gif)

尋找此問題的答案需要幾個步驟：

1. 首先，您已新增`New Customers`量度，然後依`utm_source - all`分組。 這是量度`A`或`New Customers (grouped)`。

1. 接著，您複製`New Customers (grouped)`量度，並將其設定為使用獨立維度。 量度`B` - `New customers (ungrouped)` — 顯示新客戶的總數。

1. 在隱藏兩個量度後，您將公式定義設為`A/B`。 這會將`New customers (grouped)`除以`New Customers (ungrouped)`。

1. 接下來，您將結果格式設定為`Percent`。

在此範例中，您使用`Stacked Columns`觀點來依月份顯示結果。 這可讓我們逐月比較新客戶的分佈情況。

## 正在結束 {#wrapup}

您是否在上述範例中注意到公式的`timestamp`、`groupings`、`perspectives`和`filters`繼承自其輸入量度？ 請記得，公式可以像量度一樣，用來使用`perspectives`和[獨立的時間選項](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"}。

若您有關於在`Report Builder`中使用公式的任何其他問題，[請聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)。
