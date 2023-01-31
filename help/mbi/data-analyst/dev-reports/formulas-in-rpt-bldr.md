---
title: Report Builder中的公式
description: 了解如何在Report Builder中使用公式。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 中的公式 `Report Builder`

在 [`Report Builder`](../../tutorials/using-visual-report-builder.md)，您可以使用 [定義量度](../../data-user/reports/ess-manage-data-metrics.md) 在您的帳戶中。 將這些量度合併至公式中，可讓您從資料中獲得其他深入分析。 在本文中，我們將深入探討如何在 `Report Builder`  — 讓我們跳進去！

## 什麼是 `formula`? {#what}

在 `Report Builder`, `formula` 只是根據某些數學邏輯的一或多個量度的組合。 典型範例如下所示：

![](../../assets/formula-example.png)

在此範例中，我們使用 `Number of orders metric (A)` 和 `Distinct buyers metric (B)`，我們的目標是回答以下問題：我的買家每月的平均訂單數是多少？ 公式的參數為：

* `Definition`:您可在此對輸入量度套用數學。 在此範例中，將訂單數除以不同購買者數量，即可告訴我們平均訂單數。 因此，定義為(A/B)。

* `Format`:您的公式會傳回數字、時段或貨幣金額嗎？ 公式定義旁邊是下拉式清單，您可以使用該下拉式清單指定傳回的格式。 在此案例中，是數字。

* `Miscellaneous`:公式的時間戳記、群組、透視和篩選器都由其輸入量度繼承。 這裡沒什麼可做的！

## 如何使用 `formulas` 在我的報告裡？ {#how}

現在我們已說明基本概念，讓我們來看一下一些範例。

### 範例：我想了解我的收入中有多少百分比可以歸因於首次訂購。

![使用公式來尋找歸因於首次訂購的收入百分比](../../assets/first_time_orders.gif)

在此範例中，我們使用 `Revenue` 和 `Revenue (first time orders)` 量度。 將 `Revenue (first time orders)(B)` 量度 `Revenue metric (A)` 並將傳回格式設為 `Percent`，我們可以找到可歸因於首次訂購的收入百分比。

### 範例：我想知道每筆訂單的平均收入是什麼，我做並不提供 `promo code`.

![使用公式來尋找含促銷代碼和不含促銷代碼的每筆訂單的平均收入](../../assets/promo_code.gif)

在此範例中，我們使用 `Revenue` 和 `Number of orders` 量度。 這個問題的答案包括兩個步驟 — 劃分 `Revenue (A)` 按 `Number of orders (B)` 並將傳回格式設為 `Currency`. 接下來，我們只允許公式結果(`Avg. Revenue per order`)來顯示結果，並將結果分組為 `Promo code`.

### 範例：我想知道新客戶的UTM源的分佈。

![使用公式查找新客戶的UTM源的分佈](../../assets/distro.gif)

要找到這個問題的答案，需要執行幾個步驟：

1. 首先，我們將 `New Customers` 量度，然後依 `utm_source - all`. 這是量度 `A`，或 `New Customers (grouped)`.

1. 接著，我們複製了 `New Customers (grouped)` 量度，並將其設為使用獨立維度。 量度 `B` - `New customers (ungrouped)`  — 顯示新客戶的總數。

1. 隱藏兩個量度後，我們會將公式定義設為 `A/B`. 這會將 `New customers (grouped)` 按 `New Customers (ungrouped)`.

1. 接下來，我們將結果格式設定為 `Percent`.

在範例中，我們使用 `Stacked Columns` 透視來依月份顯示結果。 這可讓我們逐月比較新客戶的分配情形。

## 包裝 {#wrapup}

您是否注意到上述範例中，公式 `timestamp`, `groupings`, `perspectives`，和 `filters` 是否繼承自其輸入量度？ 請記住，公式可被運用來使用 `perspectives` 和 [獨立時間選項](../../tutorials/time-options-visual-rpt-bldr.md){:target=&quot;_blank&quot;}，就像量度可以一樣。

如果您對於在 `Report Builder`, [聯絡支援](../../guide-overview.md).
