---
title: 識別您最有價值的行銷來源和管道
description: 了解一些可用來揭露最有價值的行銷管道的報表。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# 識別成功的行銷來源

您研究了對象、建立了行銷活動、投資了幾個行銷管道。 一段時間過後，這些管道的表現如何？ 新使用者最多的管道為何？ 哪個來源對您的總收入貢獻最大？

使用 [!DNL MBI]，您可以輕鬆地依反向連結來源劃分收入和使用者，無論其對應至 [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) 或自訂資料欄位。 此區段可讓您找出成效最佳的管道，並更妥善地投資行銷預算。

本文探討一些您可以用來發掘最有價值行銷管道的報表：

* [按來源列出的新用戶](#newusersbysource)
* [按使用者來源列出的平均期限收入](#avglifetimerev)
* [按用戶源的平均訂單值](#avgorderval)
* [按用戶註冊日期和來源列出的收入](#revbyregdateandsource)
* [按用戶源重複訂單](#repeatordersbysource)

## 必要條件 {#prereqs}

若要建置本文中的分析，您需要存取行銷贏取/反向連結來源資料。 如果您尚未追蹤，則需要將 [訂購引用源資料 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL MBI] 才能繼續。 此外，將用戶設備資訊添加到您的分析中使您能夠查看反向連結使用的技術。

## 按來源列出的新用戶 {#newusersbysource}

評估反向連結來源的效能是決定您最有價值管道的關鍵。 此報表會依贏取來源顯示一段時間內新註冊使用者的數量，讓您追蹤反向連結來源在贏取新註冊使用者時的效能。

若要在 [Report Builder](../../tutorials/using-visual-report-builder.md)，新增 **新使用者** 量度（或計算一段時間中新使用者人數的相等量度）。 然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Interval] 到每月。
1. 設定 [!UICONTROL Group By] 若要贏取（或轉介）來源，請選取您要包含的來源。
1. 此範例使用 `stacked columns` [!UICONTROL chart type].

以下是視覺逐步說明：

![按源建立新用戶報告。](../../assets/New_Users_by_source.gif)

## 按使用者來源列出的平均期限收入 {#avglifetimerev}

尋找能吸引新使用者的管道很重要，但這些轉介整體價值有多大？ 此報表顯示特定贏取來源使用者在期限內的平均收入。 換句話說，這可讓您查看從特定來源獲得的使用者在其期限內是否與從不同來源獲得的一組使用者相比花費更多。

若要在Report Builder中建立此報表，請新增 **平均期限收入** 量度。 然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 至您要分析的時段。
1. 設定 [!UICONTROL Interval] 到每月。
   [!UICONTROL Group By] 若要贏取（或轉介）來源，請選取您要包含的來源。
1. 此範例使用 `line chart` 類型。

以下是視覺逐步說明：

![建立依使用者來源的平均期限收入](../../assets/Lifetime_revenue_by_user_source.gif).

此範例只會查看期限收入，但您也可以複製此分析來查看 [!UICONTROL Number of orders] 或 [!UICONTROL Distinct buyers] 由轉介來源。

## 按用戶源的平均訂單值 {#avgorderval}

若要進一步了解使用者從特定贏取來源支出的金額，您可以建立報表，查看其平均訂購值。 這可讓您追蹤從特定來源取得的使用者是否比從其他來源取得的使用者在每次訂單上花費更多。

若要在Report Builder中建立此報表，請新增 **平均訂購值** 量度，然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 設定 [!UICONTROL Group By] 若要贏取（或轉介）來源，請選取您要包含的來源。
1. 此範例使用 **堆疊欄** 圖表類型。

以下是視覺逐步說明：

![建立依使用者來源的「平均訂單值」報表。](../../assets/Average_order_value_by_source.gif)

## 按用戶註冊日期和來源列出的總收入 {#revbyregdateandsource}

先前涵蓋的期限收入分析可讓您查看從不同來源取得的使用者的平均期限收入，但期限收入總計又如何？ 此報告可讓您識別在特定時間和特定來源中註冊的使用者總收入。

若要在Report Builder中建立此報表，請新增 `Revenue by user registration date` 量度。 如果您尚未 [建立此量度](../../data-user/reports/ess-manage-data-metrics.md) 你可以通過複製 `Revenue` 量度和變更 `time stamp` 至使用者的 `creation date`. 新增量度後，請執行下列動作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 設定 [!UICONTROL Group By] 若要贏取（或轉介）來源，請選取您要包含的來源。
1. 此範例使用 `stacked columns` 圖表類型。

以下是視覺逐步說明：

![按用戶註冊日期和來源建立收入合計報表。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 按用戶源重複訂單 {#repeatordersbysource}

「平均訂單值」報表平均顯示從特定來源獲取的用戶在下訂單時的花費。 不過，如果相同的使用者是重複客戶，此報表不會顯示。 但透過「依使用者來源重複訂購」，您可以查看特定來源的使用者是否進行了或多或少的重複購買。

若要在 [Report Builder](../../tutorials/using-visual-report-builder.md)，新增 **訂單數** 量度，然後執行下列動作：

1. 設定 [!UICONTROL Time Period] 到要分析的註冊期。
1. 設定 [!UICONTROL Time Interval] 到每月。
1. 新增 [!UICONTROL filter] 以便僅包含具有重複訂單的使用者：

   用戶的訂單號大於1

1. 設定 [!UICONTROL Group By] 若要贏取（或轉介）來源，請選取您要包含的來源。
1. 此範例使用 `stacked columns` 圖表類型。

以下是視覺逐步說明：

![建立「依使用者來源的重複訂單」報表。](../../assets/Repeat_orders_by_user_source.gif)


## 包裝 {#wrapup}

本文只談了幾項分析，可供您用來分析收購和行銷管道的價值，但這只是冰山一角。

## 相關 {#related}

* [透過追蹤訂單反向連結來源 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [連接 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [建置 [!DNL Google ECommerce] 含訂單和客戶資料的維度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [中的UTM標籤最佳作法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
