---
title: Report Builder中的公式
description: 瞭解公式在Report Builder中的使用方式。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 中的公式 `Report Builder`

在 [`Report Builder`](../../tutorials/using-visual-report-builder.md)，您可使用以下專案建立強大的視覺效果： [已定義的量度](../../data-user/reports/ess-manage-data-metrics.md) 在您的帳戶中。 在公式中組合這些量度，可讓您從資料中取得其他深入分析。 本主題探討公式如何用於 `Report Builder`  — 讓我們跳入！

## 什麼是 `formula`？ {#what}

在 `Report Builder`， a `formula` 只是以某些數學邏輯為基礎的一或多個量度的組合。 典型的範例看起來像這樣：

![](../../assets/formula-example.png)

在此範例中，您使用 `Number of orders metric (A)` 和 `Distinct buyers metric (B)`，而目標是要回答以下問題：我的買家每個月的平均訂購次數是多少？ 公式的引數為：

* `Definition`：您可以在此處對輸入量度套用數學。 在此範例中，將訂單數除以不同的買家數，可得出平均訂單數。 因此，定義為(A/B)。

* `Format`：您的公式是否傳回數字、時段或貨幣金額？ 公式定義旁有一個下拉式清單，可用來指定傳回的格式。 在此範例中，它是一個數字。

* `Miscellaneous`：公式的時間戳記、群組、透視和篩選器都是由其輸入量度繼承。 這裡沒有任何可執行的動作！

## 如何使用 `formulas` 我的報表中？ {#how}

您已涵蓋基本知識，請檢視一些範例。

### 範例：我想瞭解我的收入中有多少百分比可歸屬於首次訂單。

![使用公式來尋找首次訂單的收入百分比](../../assets/first_time_orders.gif)

在此範例中，您使用 `Revenue` 和 `Revenue (first time orders)` 量度。 劃分 `Revenue (first time orders)(B)` 量度依據 `Revenue metric (A)` 並將傳回格式設為 `Percent`，您可以找到可歸屬於首次訂單的收入百分比。

### 範例：我想知道在提供和不提供時，每份訂單的平均收入是多少 `promo code`.

![使用公式來尋找有促銷代碼和無促銷代碼的每份訂單平均收入](../../assets/promo_code.gif)

在此範例中，您使用 `Revenue` 和 `Number of orders` 量度。 此問題的答案包括兩個步驟 — 除法 `Revenue (A)` 依據 `Number of orders (B)` 並將傳回格式設為 `Currency`. 接下來，您僅允許公式結果(`Avg. Revenue per order`)來顯示結果，並將結果分組 `Promo code`.

### 範例：我想瞭解新客戶的UTM來源的分佈。

![使用公式來尋找新客戶的UTM來源分配](../../assets/distro.gif)

尋找此問題的答案需要幾個步驟：

1. 首先，您已新增 `New Customers` 量度，然後分組依據 `utm_source - all`. 這是量度 `A`，或 `New Customers (grouped)`.

1. 接下來，您已複製 `New Customers (grouped)` 量度，並將其設定為使用獨立維度。 量度 `B` - `New customers (ungrouped)`  — 顯示新客戶的總數。

1. 隱藏兩個量度後，您可將公式定義設為 `A/B`. 這會除以 `New customers (grouped)` 依據 `New Customers (ungrouped)`.

1. 接下來，將結果格式設定為 `Percent`.

在此範例中，您使用 `Stacked Columns` 透檢視，可按月顯示結果。 這可讓我們逐月比較新客戶的分佈情況。

## 正在結束 {#wrapup}

您是否注意到上述範例中 `timestamp`， `groupings`， `perspectives`、和 `filters` 是從其輸入量度繼承而來的？ 請記住，公式可供使用 `perspectives` 和 [獨立時間選項](../../tutorials/time-options-visual-rpt-bldr.md){： target=&quot;_blank&quot;}，就像量度一樣。

如果您對使用公式有任何疑問，請 `Report Builder`， [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
