---
title: 現成控制面板
description: 了解現成可用的控制面板，以深入了解您的業務。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 0%

---

# 現成控制面板

[!DNL MBI] 包含現成可用的控制面板，可提供您業務的深入分析。 透過控制面板，您可以檢查基本量度的運作狀況，例如使用者期限收入、重複購買次數、指定時段內購買的最暢銷產品等。 這些預先設定的控制面板可協助您做出明智的業務決策。

>[!NOTE]
>
>存取這些控制面板取決於您的帳戶類型和存取層級。 如果您沒有看見這些控制面板，請聯絡 [支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## 報表可用性

若 `Customers` 和 `Executive Summary` 控制面板，則部分報表僅會根據您商店的結帳設定而提供。 具體來說，如果您的商店允許訪客結帳，或不允許訪客結帳。

## 客戶（允許來賓結帳）

「客戶」（允許訪客結帳）控制面板提供有關客戶群的資訊，例如其購買行為。 此控制面板可協助您改善客戶保留率，並決定哪些客戶帶來最高收入。

### 報表

| 名稱 | 說明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去30天內，從未下過訂單的客戶所下的訂單。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去30天內，來自先前已下至少一次訂單的客戶的訂單。 |
| `Total Unique Customers (Past 30 Days)` | 過去30天內下訂單的不重複客戶計數。 |
| `Orders by New vs Existing Customers` | 沒有先前訂單的客戶與至少有一個先前訂單的客戶的訂單數量。 |
| `Subsequent Order Probability (All Time)` | 下過訂單的客戶再下訂單的可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 已下多個訂單的所有客戶的百分比。 |
| `Median Time Between Orders (All Time)` | 每位客戶下單與下單之間所花費的時間中位數。 |
| `Subsequent Order Probability` | 下過訂單的客戶再下一個訂單的可能性，依訂單編號細分（即擁有一個訂單、下一個訂單、下兩個訂單、下第三個訂單的客戶百分比，以此類推）。 |
| `Time Between Orders` | 客戶在兩次訂購之間所花費的平均時間和中位數，按訂單編號細分（即訂單一和二、二和三之間的時間，以此類推）。 |
| `Number of Customers - Lifetime Orders` | 對於在客戶期限內下達的指定數量的訂單，下達該數量的訂單的客戶數量，以及該數量代表的整個客戶群百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 在3至6個月前首次購買且僅購買的客戶。 |
| `Avg LTV by First Order` | 比較不同群組的累積平均客戶期限收入。 同類群組的定義方式為客戶首次購買的月份。 例如， `Jan 2020` 同類群組顯示首次購買是2020年1月的客戶的累積平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比較客戶首次購買後30天與整個期限內的平均收入。 每個泡泡都對應於運輸區域，每個泡泡的大小代表從該區域獲得的客戶數量。 |

## 客戶（不允許客戶結帳）

「客戶」（不允許客戶結帳）控制面板提供有關客戶群的資訊，例如其購買行為，以及從帳戶註冊到訂單版位的轉換。 此控制面板可協助您改善客戶保留率，並決定哪些客戶帶來最高收入。

### 報表

| 名稱 | 說明 |
|---|---|
| 帳戶註冊（過去30天） | 過去30天內在您的商店註冊帳戶的人數。 |
| 已註冊帳戶（過去30天），訂購1個或更多 | 過去30天內在您的商店註冊帳戶的人數，並且至少下了一筆訂單。 |
| 從註冊轉換為首次訂購的百分比（過去30天） | 過去30天中已註冊的已下訂單帳戶的百分比。 |
| 從註冊轉換為首次訂購的百分比 | 已下訂單的已登記帳戶百分比，按登記月份分列。 |
| 按新客戶與現有客戶的訂單數 | 沒有先前訂單的客戶與至少有一個先前訂單的客戶的訂單數量。 |
| 後續順序機率（所有時間） | 下過訂單的客戶再下訂單的可能性。 |
| 具有多個訂單的客戶百分比（所有時間） | 已下多個訂單的所有客戶的百分比。 |
| 訂單之間時間中位數（所有時間） | 每位客戶下單與下單之間所花費的時間中位數。 |
| 後續順序機率 | 下過訂單的客戶再下一個訂單的可能性，依訂單編號細分（即擁有一個訂單、下一個訂單、下兩個訂單、下第三個訂單的客戶百分比，以此類推）。 |
| 訂購間時間 | 客戶在兩次訂購之間所花費的平均時間和中位數，按訂單編號細分（即訂單一和二、二和三之間的時間，以此類推）。 |
| 客戶數量 — 期限訂購 | 對於在客戶期限內下達的指定數量的訂單，下達該數量的訂單的客戶數量，以及該數量代表的整個客戶群百分比。 |
| 3-6個月前購買的一次性客戶 | 在3至6個月前首次購買且僅購買的客戶。 |
| 按一次順序的平均LTV | 比較不同群組的累積平均客戶期限收入。 同類群組的定義方式為客戶首次購買的月份。 例如，2020年1月的同類群組會顯示初次購買是2020年1月的客戶的累積平均LTV。 |
| 客戶的前30天與期限收入 | 比較客戶首次購買後30天與整個期限內的平均收入。 每個泡泡都對應於運輸區域，每個泡泡的大小代表從該區域獲得的客戶數量。 |

## 執行摘要（允許訪客結帳）

「執行摘要」（允許訪客結帳）控制面板提供您訂單和收入情況的簡明圖片。 此儀表板旨在讓執行人員全面了解業務績效，但也能為其他人提供洞察力。

### 報表

| 名稱 | 說明 |
|---|---|
| 收入（當月） | 您的商店本月產生的收入。 在此情況下，收入定義為客戶在訂單上支付的最終價格。 |
| 收入(過去6個月（每天） | 每日總收入，與前七天的平均每日收入重疊。 在此情況下，收入定義為客戶在訂單上支付的最終價格。 |
| 收入變化百分比(MoM MTD) | 當月（到目前為止）與上個月相同部分的收入比較。 |
| 來自新客戶與現有客戶的收入（當月） | 本月（至今）的收入歸屬於新（首次）客戶與現有客戶（下次或更後訂單）。 |
| 平均訂購值（當月） | 當月（至今）下單的每日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| 訂購（當月） | 當月（至今）在您商店下訂單的數量。 |
| 訂單變化百分比(MoM MTD) | 當月（到目前為止）與上個月相同部分的訂單數比較。 |
| 按新客戶列出的訂單（當月） | 從未下過訂單的客戶所訂購的當月訂單。 |
| 按現有客戶列出的訂單（當月） | 當月訂單來自先前已下至少一筆訂單的客戶。 |
| 依新客戶與現有客戶的訂單數（依周列出本年度） | 沒有先前訂單的客戶與至少有一個先前訂單的客戶的訂單數量（目前為止）。 |

## 執行摘要（不允許來賓結帳）

「執行摘要」（不允許客戶結帳）控制面板可讓您清楚了解業務在訂單、收入和帳戶註冊方面的運作方式。 此儀表板旨在讓執行人員全面了解業務績效，但也能為其他人提供洞察力。

### 報表

| 名稱 | 說明 |
|---|---|
| 收入（當月） | 本月由您的商店產生的收入。 在此情況下，收入定義為客戶在訂單上支付的最終價格。 |
| 收入(過去6個月（每天） | 每日總收入，與前七天的平均每日收入重疊。 在此情況下，收入定義為客戶在訂單上支付的最終價格。 |
| 收入變化百分比(MoM MTD) | 本月迄今的收入與上月同期收入的比較。 |
| 來自新客戶與現有客戶的收入（當月） | 本月（至今）的收入歸屬於新（首次）客戶與現有客戶（下次或更後訂單）。 |
| 平均訂購值（當月） | 當月（至今）下單的每日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| 訂購（當月） | 當月（至今）在您商店下訂單的數量。 |
| 訂單變化百分比(MoM MTD) | 當月（到目前為止）與上個月相同部分的訂單數比較。 |
| 帳戶註冊（當月） | 本月新註冊的賬戶數。 |
| 從註冊轉換為首次訂購的百分比（當月） | 本月已註冊的已下訂單帳戶的百分比。 |
| 從註冊轉換為首次訂購的百分比（按周列出當年） | 今年到目前為止，每週註冊的已下單帳戶的百分比。 |

## 訂購

「訂單」控制面板提供交易式訂單數量、其狀態、使用的抵用券代碼、產生的收入以及使用的付款方法的分析。 例如，您可以追蹤完成流程，並確定沒有問題或發生瓶頸。

>[!NOTE]
>
>此控制面板上的報表可用於連線至具有任一組態類型（訪客結帳、無訪客結帳）之存放區的帳戶。

### 報表

| 名稱 | 說明 |
|---|---|
| 訂購（過去30天） | 過去30天內向您的商店下單的數量。 |
| 收入（過去30天） | 過去30天內由您的商店產生的收入。 收入定義為客戶在訂單上支付的最終價格。 |
| 平均訂購值（過去30天） | 過去30天內進行的訂單平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| 訂購 | 每月在您的商店中下的訂單數。 |
| 按付款方式列出的收入 | 您的商店產生的收入，以付款方式分割。 收入定義為客戶在訂單上支付的最終價格。 |
| 新客戶與現有客戶的AOV | 每月在您的商店中下達的訂單平均值，由沒有先前訂單的客戶與至少有一個先前訂單的客戶所下訂單拆分。 訂單值定義為客戶在訂單上支付的最終價格。 |
| 按狀態列出的訂單百分比（過去30天） | 過去30天中，目前處於每個訂單狀態的每天訂單百分比。 |
| 未完成訂單（在1天前建立） | 多天前下達且仍處於未完成狀態（未取消或完成）的所有訂單的清單。 |
| 每小時訂單數（過去7天） | 按小時按日訂購卷。 |
| 收入詳細資料（過去30天） | 將過去30天的每日收入劃分至總收入值的所有元件。 |
| 按抵用券代碼列出的訂單詳細資料（過去30天） | 對於您商店提供的每個抵用券代碼，詳細說明了該抵用券代碼的使用方式，以及在過去30天中帶來的回報。 |
| 具有抵用券的訂單百分比（過去30天） | 過去30天內使用抵用券的訂單與未使用的訂單百分比。 |

## 產品

「產品」儀表板按訂購的產品、其總商品價值(GMV)以及購買和退貨的最暢銷產品顯示一般產品效能。 它可協助您平衡購買與退貨，並決定產品的成功與受歡迎程度。 您的商店必須 [已配置以跟蹤退款](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) 為要填充的圖表。

>[!NOTE]
>
>此控制面板上的報表可用於連線至具有任一組態類型（訪客結帳、無訪客結帳）之存放區的帳戶。

### 報表

| 名稱 | 說明 |
|---|---|
| GMV（過去30天） | 過去30天內銷售的所有產品的商品總值。 GMV定義為訂購數量乘以每種產品的基本價格。 |
| % GMV（過去30天）已退回 | 在過去30天內購買的產品GMV的百分比，這導致了退款。 |
| 訂購產品數量（過去30天） | 過去30天內訂購的物料總數。 |
| %已購產品（過去30天）已退回 | 在過去30天內購買並導致退款的項目百分比。 |
| 商品總值 | 按月列出的所有產品的總商品價值。 GMV定義為訂購數量乘以每種產品的基本價格。 |
| 購買與每項產品的退款率（過去30天） | 對於每件產品，會比較過去30天訂購的總數與退貨率。 每個泡泡的大小代表退款率。 |
| 產品效能詳細資訊（過去30天） | 過去30天內的銷售和後續退款詳細資訊（依產品SKU和產品名稱）。 |
| 按GMV購買的最多產品（過去30天） | 過去30天內銷售的產品帶來最多收入（前10名）。 |
| 按GMV列出的最大退款產品（過去30天） | 過去30天內購買的產品，導致因退款而損失的GMV最多（前10名）。 |
| 按數量列出的最大購買產品（過去30天） | 過去30天內銷售的產品數量最多（前10名）。 |
| 按數量列出的最大退款產品（過去30天） | 在過去30天內購買的產品，可導致最大數量的退款（前10個）。 |