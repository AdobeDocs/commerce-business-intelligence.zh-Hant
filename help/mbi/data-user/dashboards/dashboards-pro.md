---
title: 現成儀表板
description: 瞭解現成儀表板，以深入瞭解您的業務。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# 現成儀表板

[!DNL Adobe Commerce Intelligence] 包括現成儀表板，可讓您深入瞭解您的業務。 使用儀表板，您可以檢查基本指標的運行狀況，如用戶壽命收入、重複購買次數、在指定時間期內購買的頂級產品等。 建立這些預先配置的儀表板是為了幫助您做出明智的業務決策。

>[!NOTE]
>
>訪問這些儀表板取決於您的帳戶類型和訪問級別。 如果您看不到這些儀表板，請與 [支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 報告可用性

對於 `Customers` 和 `Executive Summary` 儀表板，某些報表僅根據您的商店的簽出配置可用。 具體來說，如果您的商店允許來賓結帳或不允許來賓結帳。

## 客戶（允許來賓結帳）

「客戶」（允許客戶結帳）控制板提供有關客戶群的資訊，如他們的購買行為。 此控制板可以幫助您提高客戶保留率並確定哪些客戶能夠帶來最高收入。

### 報告

| 名稱 | 說明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去30天內從以前從未下過訂單的客戶訂購。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去30天內來自先前已下單至少一份客戶的訂單。 |
| `Total Unique Customers (Past 30 Days)` | 過去30天內下訂單的獨特客戶數。 |
| `Orders by New vs Existing Customers` | 沒有先前訂單的客戶與至少有一個先前訂單的客戶的訂單數量。 |
| `Subsequent Order Probability (All Time)` | 已下訂單的客戶可能會再下一個訂單。 |
| `% of Customers with Multiple Orders (All Time)` | 已下達多個訂單的所有客戶的百分比。 |
| `Median Time Between Orders (All Time)` | 每個客戶在下一訂單和下一訂單之間所花費的時間的中值。 |
| `Subsequent Order Probability` | 已下訂單的客戶可能會按訂單編號再次下單。 也就是說，一份訂單的客戶中，有一份訂單的客戶佔百分比，有兩份訂單的客戶佔三分之一，依此類推。 |
| `Time Between Orders` | 客戶在訂單之間平均和中值的時間，按訂單編號細分（即訂單一和二、二和三之間的時間，等等）。 |
| `Number of Customers - Lifetime Orders` | 對於客戶生存期內的給定數量的訂單，已下達該數量訂單的客戶數量以及該數量代表的整個客戶基數的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 在3至6個月前首次購買且僅購買的客戶。 |
| `Avg LTV by First Order` | 比較各組之間累積的平均客戶生存期收入。 Cohort是按客戶首次購買的月份定義的。 例如， `Jan 2020` coort顯示首次購買是2020年1月的客戶的累計平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比較客戶首次購買後30天與整個生命週期的平均收入。 每個氣泡對應於一個運輸區域，每個氣泡的大小代表從該區域獲得的客戶數量。 |

## 客戶（不允許客戶結帳）

「客戶」（不允許客戶結帳）控制面板提供有關客戶群的資訊，如其購買行為和從帳戶登記到訂單放置的轉換。 此控制板可以幫助您提高客戶保留率並確定哪些客戶能夠帶來最高收入。

### 報告

| 名稱 | 說明 |
|---|---|
| `Account Registration (Past 30 Days)` | 過去30天內在您的商店註冊帳戶的人員數。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 過去30天內在您的商店註冊帳戶並且還下了至少一個訂單的人數。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 在過去30天中登記的已下訂單帳戶的百分比。 |
| `% Conversion from Registration to First Order` | 按登記月份登記的已訂購帳戶百分比。 |
| `Orders by New vs Existing Customers` | 沒有先前訂單的客戶與至少有一個先前訂單的客戶的訂單數量。 |
| `Subsequent Order Probability (All Time)` | 已下訂單的客戶可能會再下一個訂單。 |
| `% of Customers with Multiple Orders (All Time)` | 已下達多個訂單的所有客戶的百分比。 |
| `Median Time Between Orders (All Time)` | 每個客戶在下一訂單和下一訂單之間所花費的時間的中值。 |
| `Subsequent Order Probability` | 客戶下訂單的可能性會按訂單編號分出另一個訂單。 也就是說，有一份訂單的客戶中，有一份訂單的客戶佔百分比，有兩份訂單的客戶佔三分之一，依此類推。 |
| `Time Between Orders` | 客戶在訂單之間平均和中值的時間，按訂單編號細分（即訂單一和二、二和三之間的時間，等等）。 |
| `Number of Customers - Lifetime Orders` | 對於客戶生存期內的給定數量的訂單，已下達該數量訂單的客戶數量以及該數量代表的整個客戶基數的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 在3至6個月前首次購買且僅購買的客戶。 |
| `Avg LTV by First Order` | 比較各組之間累積的平均客戶生存期收入。 Cohort是按客戶首次購買的月份定義的。 例如，2020年1月的一組學生顯示首次購買是在2020年1月的客戶的累計平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比較客戶首次購買後30天與整個生命週期的平均收入。 每個氣泡對應於一個運輸區域，每個氣泡的大小代表從該區域獲得的客戶數量。 |

## 執行摘要（允許來賓簽出）

「執行摘要」（允許客戶結帳）控制板為您提供了業務在訂單和收入方面如何運作的簡要說明。 此儀表板旨在讓執行官全面瞭解業務表現，但對其他人也有深刻見解。

### 報告

| 名稱 | 說明 |
|---|---|
| `Revenue (Current Month)` | 您的商店在當月產生的收入。 在這種情況下，收入定義為客戶在訂單上支付的最終價格。 |
| `Revenue (Past 6 Months by Day)` | 每日收入總額，與前七天的日均收入重疊。 在這種情況下，收入定義為客戶在訂單上支付的最終價格。 |
| `% Change in Revenue (MoM MTD)` | 當月（到目前為止）收入與上個月相同部分的比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 本月（迄今）來自新（首次）客戶與現有客戶（下訂第二份或更晚訂單）之收益。 |
| `Average Order Value (Current Month)` | 當月（迄今）下單的日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders (Current Month)` | 當月（到目前為止）在您的商店中下達的訂單數。 |
| `% Change in Orders (MoM MTD)` | 當月（迄今）訂單數與上月相同部分的比較。 |
| `Orders by New Customers (Current Month)` | 從以前從未下過訂單的客戶訂購的當月訂單。 |
| `Orders by Existing Customers (Current Month)` | 當月來自以前至少下了一個訂單的客戶的訂單。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 當前年度（到目前為止）每週沒有前一訂單的客戶的訂單數，與至少有一個前一訂單的客戶的訂單數。 |

## 執行摘要（不允許來賓簽出）

「執行摘要」（不允許客戶結帳）控制板為您提供了業務在訂單、收入和帳戶註冊方面如何運作的簡潔圖片。 此儀表板旨在讓執行官全面瞭解業務表現，但對其他人也有深刻見解。

### 報告

| 名稱 | 說明 |
|---|---|
| `Revenue (Current Month)` | 您的商店本月產生的收入。 在這種情況下，收入定義為客戶在訂單上支付的最終價格。 |
| `Revenue (Past 6 Months by Day)` | 每日收入總額，與前七天的日均收入重疊。 在這種情況下，收入定義為客戶在訂單上支付的最終價格。 |
| `% Change in Revenue (MoM MTD)` | 與上月同期相比，本月迄今為止的營收水準。 |
| `Revenue from New vs Existing Customers (Current Month)` | 本月（迄今）來自新（首次）客戶與現有客戶（下訂第二份或更晚訂單）之收益。 |
| `Average Order Value (Current Month)` | 當月（迄今）下單的日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders (Current Month)` | 當月（到目前為止）在您的商店中下達的訂單數。 |
| `% Change in Orders (MoM MTD)` | 當月（迄今）訂單數與上月相同部分的比較。 |
| `Account Registrations (Current Month)` | 本月迄今新註冊的賬戶數。 |
| `% Conversion from Registration to First Order (Current Month)` | 本月至今已登記的已下單帳戶的百分比。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 今年到目前為止已下訂單的每週登記帳戶的百分比。 |

## 訂單

「訂單」控制面板提供有關訂單事務處理量、其狀態、使用的優惠券代碼、生成的收入以及使用的付款方法的見解。 例如，您可以跟蹤完成流程並確保不存在問題或瓶頸發生。

>[!NOTE]
>
>此儀表板上的報告可用於連接到具有任何配置類型（來賓簽出，無來賓簽出）的儲存的帳戶。

### 報告

| 名稱 | 說明 |
|---|---|
| `Orders (Past 30 Days)` | 過去30天內向您的商店下單的數量。 |
| `Revenue (Past 30 Days)` | 過去30天內由您的商店產生的收入。 收入定義為客戶在訂單上支付的最終價格。 |
| `Average Order Value (Past 30 Days)` | 過去30天內發出的訂單的平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders` | 每月在您的商店中下達的訂單數。 |
| `Revenue by Payment Method` | 由您的商店產生的收入，按付款方法分攤。 收入定義為客戶在訂單上支付的最終價格。 |
| `AOV by New vs Existing Customers` | 在您的商店中下達的訂單的月平均值，按沒有先前訂單的客戶和至少有一個先前訂單的客戶所下達的訂單進行分解。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `% Orders by Status (Past 30 Days)` | 過去30天中每天當前處於每個訂單狀態的訂單的百分比。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 多天前下達的仍處於未完成狀態（未取消或完成）的所有訂單的清單。 |
| `Orders Per Hour (Past 7 Days)` | 按小時按天訂購卷。 |
| `Revenue Details (Past 30 Days)` | 過去30天的每日收入細分為總收入值的所有組成部分。 |
| `Order Details by Coupon Code (Past 30 Days)` | 對於您商店提供的每個優惠券代碼，詳細瞭解如何使用該優惠券代碼以及在過去30天中帶來的回報。 |
| `% Orders with Coupon (Past 30 Days)` | 過去30天內使用優惠券的訂單與未使用優惠券的訂單的百分比。 |

## 產品

「產品」控制面板顯示按訂購產品、其總商品價值(GMV)和已購買和退還的頂級產品計算的一般產品效能。 它可以幫助您平衡購買和退貨，並決定產品的成功和受歡迎程度。 您的商店必須 [配置跟蹤退款](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) 要填充的圖表。

>[!NOTE]
>
>此儀表板上的報告可用於連接到具有任何配置類型（來賓簽出，無來賓簽出）的儲存的帳戶。

### 報告

| 名稱 | 說明 |
|---|---|
| `GMV (Past 30 Days)` | 過去30天內所有已售產品的商品總值。 GMV定義為訂購數量乘以每個產品的基本價格。 |
| `% GMV (Past 30 Days) Refunded` | 在過去30天內購買的導致退款的產品的GMV百分比。 |
| `Product Quantity Ordered (Past 30 Days)` | 過去30天內訂購的物料總數。 |
| `% Purchased Products (Past 30 Days) Refunded` | 在過去30天內採購的導致退款的物料百分比。 |
| `Gross Merchandise Value` | 所有已售產品按月的商品總值。 GMV定義為訂購數量乘以每個產品的基本價格。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 對於每種產品，比較過去30天訂購的總數量與退還產品的比率。 每個氣泡的大小代表退款率。 |
| `Product Performance Details (Past 30 Days)` | 過去30天內按產品sku和產品名稱列出的銷售和後續退款的詳細資訊。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 過去30天內銷售的產品帶來的收入最多（前10位）。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 過去30天內購買的產品導致因退款而損失的GMV最多（前十）。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 過去30天內銷售的產品數量最多（前10個）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 過去30天內所購產品已獲退回數量最多（前10天）。 |
