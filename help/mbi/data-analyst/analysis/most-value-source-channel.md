---
title: 確定您最有價值的營銷來源和渠道
description: 瞭解一些報告，這些報告可用於發現您最有價值的市場營銷渠道。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 確定成功的營銷來源

你研究了你的受眾，你創造了你的活動，你投資了幾個營銷渠道。 現在時間已經過去了，這些頻道表現如何？ 哪個渠道吸引了最多的新用戶？ 哪個來源對您的總收入貢獻最大？

與 [!DNL Adobe Commerce Intelligence]，您可以輕鬆地按推薦來源劃分收入和用戶，無論它是否與 [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) 或自定義資料欄位。 這種細分使您能夠找到效能最佳的渠道，並更好地投資營銷預算。

本主題探討一些報告，您可以使用這些報告來發現您最有價值的營銷渠道：

* [按源列出的新用戶](#newusersbysource)
* [按用戶來源列出的平均生存期收入](#avglifetimerev)
* [按用戶源列出的平均訂單值](#avgorderval)
* [按用戶註冊日期和來源列出的收入](#revbyregdateandsource)
* [按用戶來源重複訂單](#repeatordersbysource)

## 先決條件 {#prereqs}

要構建本主題中的分析，您需要訪問市場營銷獲取/推薦源資料。 如果你還沒有跟蹤它，你需要 [訂單引用源資料 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) 入 [!DNL Adobe Commerce Intelligence] 才能繼續。 此外，向分析中添加用戶設備資訊使您能夠查看推薦使用的技術。

## 按源列出的新用戶 {#newusersbysource}

評估推薦來源的效能是確定您最有價值的渠道的關鍵。 此報表按獲取來源顯示一段時間內新註冊用戶的數量，從而允許您跟蹤在獲取新註冊用戶時推薦來源的效能。

在 [Report Builder](../../tutorials/using-visual-report-builder.md)的子菜單。 **新用戶** 度量（或計算一段時間內新用戶數的等效度量）。 然後執行以下操作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Interval] 到每月。
1. 設定 [!UICONTROL Group By] 獲取（或引用）來源，並選擇要包括的來源。
1. 此示例使用 `stacked columns` [!UICONTROL chart type]。

下面是一個視覺漫遊：

![按源建立新用戶報告。](../../assets/New_Users_by_source.gif)

## 按用戶來源列出的平均生存期收入 {#avglifetimerev}

找到能吸引新用戶的渠道非常重要，但這些推薦總體而言有多重要？ 此報表顯示一段時間內來自特定獲取來源的用戶的平均生存期收入。 換句話說，這允許您查看從特定源獲取的用戶在其整個生命週期中是否比從不同源獲取的一組用戶花費更多。

要在Report Builder中建立此報表，請添加 **平均生命週期收入** 度量。 然後執行以下操作：

1. 設定 [!UICONTROL Time Period] 到要分析的時間段。
1. 設定 [!UICONTROL Interval] 到每月。
   [!UICONTROL Group By] 獲取（或引用）來源，並選擇要包括的來源。
1. 此示例使用 `line chart` 的雙曲餘切值。

下面是一個視覺漫遊：

![按用戶源建立平均生存期收入](../../assets/Lifetime_revenue_by_user_source.gif)。

此示例僅查看生命期收入，但您也可以複製此分析以查看 [!UICONTROL Number of orders] 或 [!UICONTROL Distinct buyers] 按推薦來源。

## 按用戶源列出的平均訂單值 {#avgorderval}

為了更好地瞭解用戶從特定收購來源中花費的金錢，您可以構建一個查看其平均訂單值的報告。 這使您能夠跟蹤從特定來源獲取的用戶是否比從其他來源獲取的用戶花費更多的每訂單支出。

要在Report Builder中建立此報表，請添加 **平均訂單值** ，然後執行以下操作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 設定 [!UICONTROL Group By] 獲取（或引用）來源，並選擇要包括的來源。
1. 此示例使用 **堆疊列** 圖表類型。

下面是一個視覺漫遊：

![按用戶來源建立平均訂單值報表。](../../assets/Average_order_value_by_source.gif)

## 按用戶註冊日期和來源列出的總收入 {#revbyregdateandsource}

前面介紹的生命週期收入分析允許您查看從不同來源獲得的用戶的平均生命週期收入，但是，整個生命週期的收入呢？ 此報表允許您確定在特定時間和特定來源中註冊的總收入用戶的生成量。

要在Report Builder中建立此報表，請添加 `Revenue by user registration date` 度量。 如果你沒有 [建立此度量](../../data-user/reports/ess-manage-data-metrics.md) 你可以通過複製 `Revenue` 度量和更改 `time stamp` 到用戶 `creation date`。 添加度量後，執行以下操作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 設定 [!UICONTROL Group By] 獲取（或引用）來源，並選擇要包括的來源。
1. 此示例使用 `stacked columns` 圖表類型。

下面是一個視覺漫遊：

![按用戶註冊日期和來源建立收入合計報表。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 按用戶來源重複訂單 {#repeatordersbysource}

平均訂單值報表平均顯示從特定來源獲取的用戶在下訂單時的花費。 但是，此報告不會顯示這些用戶是否是重複客戶。 但是，使用「按用戶來源重複訂單」，您可以查看特定來源的用戶是否多或少重複購買。

在 [Report Builder](../../tutorials/using-visual-report-builder.md)的子菜單。 **訂單數** ，然後執行以下操作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 添加 [!UICONTROL filter] 只包括重複訂單的用戶：

   用戶的訂單號大於1

1. 設定 [!UICONTROL Group By] 獲取（或引用）來源，並選擇要包括的來源。
1. 此示例使用 `stacked columns` 圖表類型。

下面是一個視覺漫遊：

![按用戶來源建立重複訂單報表。](../../assets/Repeat_orders_by_user_source.gif)


## 包裝 {#wrapup}

本主題僅涉及一些分析，您可以用來分析您的收購和營銷渠道的價值，但這只是冰山一角。

## 相關 {#related}

* [跟蹤訂單推薦來源 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [連接 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [大樓 [!DNL Google ECommerce] 包含訂單和客戶資料的維](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [UTM標籤的最佳做法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
