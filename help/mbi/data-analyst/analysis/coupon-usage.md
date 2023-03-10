---
title: 分析抵用券使用情況
description: 了解如何分析贏取和保留客戶的抵用券使用情形。
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 2%

---

# 抵用券使用量

您是否曾懷疑提供優惠券對您的業務有何影響？ 想知道哪些抵用券對績效有幫助或有損？ 本文探討透過回答以下問題來提供客戶優惠券使用情形的分析：

* 有多少客戶使用抵用券？
* 使用了多少抵用券？
* 您在套用抵用券之前和之後的收入為何？
* 套用抵用券之前和之後的平均訂購值為何？
* 你用優惠券吸引哪些顧客？

讓我們開始吧！

## 建議量度 {#metrics}

分析抵用券使用情形時，請考慮使用([或建築](../../data-user/reports/ess-manage-data-metrics.md))這些量度：

### 訂單數

此量度會顯示一段時間內具有和沒有抵用券的訂單數量。 這會顯示客戶是否和多久使用您的抵用券，以及這會隨著時間而改變。

### 總收入

此量度會顯示您從包含特定抵用券的訂單所獲得的總收入。 總收入乃於應用任何折扣前計算已售項目之全價。 這有助於判斷哪些抵用券與最高和最低的總收入相關。

### 優惠券折扣

此量度可顯示從抵用券套用的總折扣金額。 請務必注意，若沒有抵用券，這些訂單可能不會發生。

### 淨收入

此量度會顯示您從包含特定抵用券的訂單所獲得的淨收入。 淨收入為應用所有折扣後所售項目的價格計算。 這有助於判斷哪些抵用券與最高和最低的淨收入相關。

### 折扣百分比

這顯示按折扣抵銷的總收入份額。 對於優惠券，此值已知（例如優惠10%）。 儘管如此，此測量仍提供固定美元折扣的抵用券分析和比較方法。

### 平均淨訂單值

此測量會顯示套用抵用券時的平均訂單值。 您可以分析具有抵用券的訂單，其訂單值是否一直低於沒有抵用券的訂單。

### 平均訂單折扣

這會顯示套用優惠券之每筆訂單的平均折扣金額。 這會顯示平均淨訂單值與平均總訂單值之間的差異。

### 不同的購買者

此量度會顯示使用特定抵用券的不同購買者數量。

### 平均期限收入

此量度可協助評估使用特定抵用券之客戶產生的忠誠度和平均收入。 在評估使用抵用券的客戶是否價值高於其他客戶時，請務必說明每個類別中不同的購買者數量，以確保您的樣本大小相當大。

## 範例 {#example}

現在您知道要查看哪些量度了，看一個包含三種不同抵用券的範例 — 優惠10%、優惠100美元或更多、優惠10美元。

| **抵用券** | **訂單數** | **總收入** | **優惠券總折扣** | **淨收入** | **折扣百分比** |
|-----|-----|-----|-----|-----|-----|
| **優惠10%** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **優惠20美元，優惠100多美元** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **優惠10美元** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style="table-layout:auto"}


| **抵用券** | **平均 淨訂單值** | **平均 訂購折扣** | **不同的購買者** | **平均 期限收入** |
|-----|-----|-----|-----|-----|
| **優惠10%** | $225.08 | $25.01 | 79 | $361.50 |
| **優惠20美元，優惠100多美元** | $117.91 | $20.00 | 95 | $218.76 |
| **優惠10美元** | $62.35 | $10.00 | 199 | $84.27 |

{style="table-layout:auto"}

## 你能從中吸取什麼？

大約80份訂單是以「優惠10%」的抵用券下單，100份訂單是以「優惠100美元或以上」的抵用券下單，200份訂單是以「優惠10美元」的抵用券下單。 此 **訂購數** 與每個抵用券相關聯的因素可能會有所不同，包括：

* 優惠券的發行時間。
* 提供抵用券的日/周/月/年時間。
* 優惠券的發行季，視業務而定。 例如：
* 夏季的月份，該公司提供了「10%的優惠券」，但該公司銷售冬裝。

* 優惠券的限制。 例如：
* 「優惠10美元」的抵用券只提供給新客戶。
* 「優惠10%」的抵用券僅提供給在同一訂單中購買冬季大衣的客戶。

* 一般客戶的購買行為。

若 **折扣** 對於所有三張抵用券，（約2,000美元）的訂單數都不同。 按每筆訂單分析折扣有助於解釋這些不同數字的原因。 「優惠10%」的抵用券的訂單數量最少，但 **平均訂購折扣** 大約25美元。 儘管此優惠券的訂單數量很少，但其高平均折扣值使其總折扣額接近2,000美元。

**總收入及淨收入** 提供與每個抵用券相關聯之訂單的完整值的整體概念。 不過，這張整體圖片並未提供對每個抵用券相關不同行為的了解。 一旦您查看每筆訂單，您就會發現「優惠10%」的抵用券高 **平均淨訂單** 值，這反過來又導致其高 **淨收入**.

另一方面，「10%優惠」的票面價值很高（25.01美元），但最低 **折扣率**. 如果將其平均淨訂購值$225.08計算在內，這就很合理。「10%折扣」的抵用券具有較大平均淨訂購值的小折扣，因此平均訂購折扣是大額。

查看 **不同買家** 和 **平均期限收入** 每張抵用券。 「優惠10%」的抵用券與不同買家的訂單數量相同。 這可能是每個客戶限制為一張抵用券的結果。 另一方面，「優惠$100或以上$20」和「優惠$10」的抵用券中，不同的購買者少於訂單數量，這意味著某些客戶多次使用這些抵用券。

對於平均期限收入，您會看到每個抵用券的平均期限收入大於個別 **平均淨訂單** 值。 這表示客戶重複購買，且/或其訂單值遠高於平均淨訂單值。

## 我還可以分析什麼？ {#otheranalyses}

本文中提到的分析可讓您深入了解客戶如何使用您的抵用券，但有許多其他分析可讓您更進一步了解。

**您可以從抵用券分析客戶的贏取。**

哪些優惠券能鼓勵客戶下訂單？ 這些抵用券是否能吸引一次性購買者，還是能鼓勵客戶忠誠度（換句話說，是重複購買的客戶）?

**您可以分析客戶使用優惠券所花的時間。**

您的抵用券是否在抵用券發行當天使用，或是在大部分客戶使用抵用券之前一兩週？

**您可以找出可提高客戶忠誠度和整體價值的最佳折扣金額。**

折扣額鼓勵了重複購買者、更高的平均訂購值和更高的終身收入？

回答這些問題可讓您深入了解客戶、其行為，以及為您的企業提供最大價值的優惠券。
