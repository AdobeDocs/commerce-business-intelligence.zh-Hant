---
title: 提高廣告行銷活動的ROI
description: 瞭解評估行銷活動績效的幾種不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Advertising行銷活動與ROI

[!DNL Adobe Commerce Intelligence]可讓您從資料庫輕鬆[結合廣告成本資料和收入資料](../../data-analyst/importing-data/integrations/google-adwords.md)。 這可幫助您識別哪些行銷活動具有最高的投資報酬率(ROI)。 本主題會探索幾種評估行銷活動績效的不同方法。

## 先決條件

* 匯入您的廣告成本資料：
   * [將您的 [!DNL Google AdWords] 連線至 [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md)：這會同步處理您的[!DNL Adwords]在[!DNL Commerce Intelligence]中的支出
   * [上傳其他廣告成本資料](../importing-data/connecting-data/import-offline-ad-data.md)：建議將此用於沒有直接聯結器的頻道[!DNL Commerce Intelligence]
   * 如果您從多個來源匯入成本資料，您可以[合併](../../best-practices/consolidating-your-tables.md)在[!DNL Commerce Intelligence]中的資料。 只需[提交支援票證](../../guide-overview.md#Submitting-a-Support-Ticket)即可。
* [追蹤使用者贏取管道資料](../analysis/google-track-user-acq.md)

## 使用者贏取行銷活動

鎖定目標為贏取使用者的行銷活動可從多個角度進行測量，包括：

1. 從行銷活動取得的新使用者數
1. 從註冊到購買行銷活動的轉換率
1. 根據平均使用者期限值(LTV)的促銷活動ROI

在有關[識別您的主要行銷管道](../analysis/most-value-source-channel.md)的獨立教學課程中，將探索上述分析(1)和(2)。 在這裡，您可以探索分析(3)以測量一段時間內的行銷活動ROI。 此量度可回答從特定行銷活動取得的使用者是否產生足夠的期限收入以涵蓋取得成本。

>[!NOTE]
>
>此範例假設所有行銷活動成本僅用於取得新使用者。 實際上，您的促銷活動成本也會與獲得未轉換的造訪、重複購買者等共用。 假設所有成本都用於取得新的註冊使用者，則產生的ROI會考慮最壞的情況（每次取得的最高成本）。 您可以確定您的實際ROI高於您的計算。
>
>範例：假設您在產生10個新使用者和10個重複購買者的行銷活動上花費$20，則您每個新使用者的實際成本為$1。 但是，假設所有成本都花在獲取新使用者上，則每次獲取的成本為2美元。

**1. 首先，請建立圖表，依行銷活動劃分您的廣告成本：**

1. 建立一段時間內總支出的[!UICONTROL Metric]
1. 前往[!UICONTROL Data > Metrics]
1. 選取`Add New Metric`並選取正在記錄您的[!DNL `Adwords...`]成本資料的[!DNL AdWords]資料表。
1. 在量度編輯器中，為您的量度命名（例如，[!UICONTROL AdWord Cost]）
1. 使用下拉式清單，對依&#x200B;**欄排序的**&#x200B;資料表（變更）中的`adCost`欄執行[!DNL Adwords...]總和`date`。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 按一下頂端的「`Back to Metric List`」並前往任何儀表板。

1. 建立依行銷活動劃分割槽段支出的報表
1. 在任何儀表板中，按一下[!UICONTROL Add Report > Create report]
1. 選取您剛建立的[!UICONTROL Adword Cost]量度
1. 將[!UICONTROL Time period]設為`All-time`，並將[!UICONTROL Interval]設為`None`
1. 在`Group by`標籤下，新增`campaign`為[!UICONTROL grouping field]，然後按一下方塊中的`Add All`。
1. 此報表依行銷活動顯示您的全部[!DNL AdWords]成本

**2。 建立依行銷活動計數新使用者的報告：**

1. 在任何儀表板中，按一下&#x200B;**[!UICONTROL Add Report > Create report]**
1. 選取計算一段時間內新註冊使用者人數的`New users`量度
1. 將[!UICONTROL Time period]設為`All-time`，並將[!UICONTROL Interval]設為`None`
1. 在`Group by`標籤下，新增`campaign`為`grouping field`，然後按一下方塊中的&#x200B;**`Add All`**
1. 此報表依行銷活動顯示您所有時間的註冊使用者

**3。 建立依促銷活動劃分平均使用者LTV的報告：**

1. 在任何儀表板中，按一下&#x200B;**[!UICONTROL Add Report > Create report]**
1. 選取計算平均使用者期限收入的`Average lifetime revenue`量度
1. 將[!UICONTROL Time period]設為`All-time`，並將[!UICONTROL Interval]設為`None`
1. 在`Group by`標籤下，新增`campaign`或`utm\_campaign`作為[!UICONTROL grouping field]，然後按一下方塊中的`Add All`
1. 此報表顯示依行銷活動的平均使用者期限收入

**最後，將這三種分析整合在一個報告中，以計算行銷活動ROI：**

1. 在任何儀表板中，按一下&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 新增作為輸入，使用上述三個量度。 每個檔案都會指派一個字母（例如\[`A`\]、\[`B`\]和\[`C`\]）
1. [!UICONTROL Cost]：新增量度AdWords成本 — 此為變數\[A\]。 這會依行銷活動傳回成本。
1. [!UICONTROL Users]：新增量度新使用者 — 這是變數\[B\]。 這會傳回行銷活動的使用者人數。
1. [!UICONTROL LTV]：新增量度平均期限收入 — 此為變數\[`C`\]。 這會依行銷活動傳回LTV。

1. 按一下「圖表」一字旁邊的隱藏圖示，即可將焦點放在表格上
1. 現在使用`Add Formula`來合併這些量度，如下所示：
1. [!UICONTROL ROI]：輸入公式`(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，如果\[`A`\]代表`Ad Cost by Campaigns`，\[`B`\]代表`New users by campaigns`，且\[`C`\] `LTV by campaigns`。 這會傳回（平均使用者LTV — 每次收購的平均成本） / （每次收購的平均成本）的比率
1. [!UICONTROL Avg Return per User]：輸入公式&#x200B;**\[`C`\]-(\[`A`\]/\[`B`\])**。 透過計算（平均使用者LTV） — （每次收購的平均成本），這會傳回使用者的平均利潤。
1. [!UICONTROL CPA]：輸入公式&#x200B;**`\[A\]/\[B\]`**。 這會傳回實際促銷活動的每次贏取成本。
1. 要從[!DNL AdWords]資料包含的其他潛在量度包括`Impressions`和`adClicks`的總和（來自[!DNL AdWords]資料），以及通過特定行銷活動建立的總計`number of orders`。
1. 根據使用者註冊或首次購買後的30天和90天計算LTV的ROI可能也很有趣。

1. 您可以按一下並拖曳量度和公式，重新排序報表中的欄
1. 為報表命名，並請務必儲存為表格。

## 產品行銷活動

您是否執行產品特定廣告？ 若是如此，您可以計算特定產品的收入/成本，以評估這些促銷活動的ROI。

>[!NOTE]
>
>此範例假設所有行銷活動成本都專門用於產生特定產品的購買。 假設所有成本都花在產生購買上，則產生的ROI會考慮最壞的情況（最高每次購買成本）。 您可以確定您的實際ROI高於此計算。 範例：假設您在產生10名新使用者和10次購買的行銷活動上花費$20，則您的每次購買實際成本為$1。 假設所有成本都是為了取得新使用者，則每次購買的成本為$2。

開始之前，[送出支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)以將下列維度聯結到您的行專案表格(`sales\_flat\_order\_item, order\_item`)：

* 訂單的來源（如果您只追蹤使用者層級的轉介來源，則加入使用者的來源）
* 訂單的行銷活動（如果您只追蹤使用者層級的轉介來源，則加入使用者的行銷活動）
* 訂單媒體（如果您只追蹤使用者層級的轉介來源，則加入使用者的媒體）

**1. 現在先建立圖表，傳回特定產品的每個行銷活動的收入：**

1. 在任何儀表板中，按一下&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 選取在行專案層級計算收入的`Revenue by items`量度
1. 將[!UICONTROL Time period]設為`All-time`，並將[!UICONTROL Interval]設為`None`
1. 在「`Filter by`」標籤下方，新增`product name 'IN'`產品`A`、產品`B`、產品`C`， ...」，並包含以逗號分隔的行銷活動鎖定的所有產品名稱（例如，`product name 'IN' yellow t-shirt`、`red t-shirt, blue t-shirt`）
1. 在`Group by`標籤下，新增`order's campaign`或`order's utm\_campaign`作為`grouping`欄位，然後按一下方塊中的&#x200B;**[!UICONTROL Add All]**
1. 此報表依行銷活動顯示特定產品的收入

**2。 若要計算ROI，請再次將度量合併到一個報表中：**

1. 在任何儀表板中，按一下&#x200B;**[!UICONTROL Add Report > Create new report]**
1. 新增`Revenue by items`量度，依照上方特定產品報表之行銷活動的篩選器和說明分組，然後按一下量度純量值下方的&#x200B;**[!UICONTROL Hide]**
1. 現在依照您在上述[!DNL AdWords Cost]區段中探索的`Ad cost by campaigns`報告中的篩選器和群組方式方向，新增`User acquisition campaigns`量度；然後按一下量度純量值下方的&#x200B;**[!UICONTROL Hide]**
1. 設定好這些量度後，即可新增公式：
1. [!UICONTROL ROI]：輸入公式`\[A\]/\[B\]`，如果`\[A\]`代表`Revenue per campaign for specific product(s)`，`\[B\]`代表`Ad cost by campaigns`。 這會傳回（特定產品的收入） / （行銷活動成本）的比率
1. [!UICONTROL Return]：輸入公式`\[A\]-\[B\]`。 這會透過計算（平均使用者LTV）傳回使用者的平均利潤 — （每次收購的平均成本）
1. （選用） [!UICONTROL Revenue]：取消隱藏`Revenue by items`量度以檢視每個行銷活動的特定產品收入
1. （選用） [!UICONTROL Cost]：取消隱藏`AdWords Cost`量度以檢視行銷活動的成本

1. 為報表命名，並確實儲存為表格

**3。 對每個已公告的產品或產品群組重複上述步驟1和2。**

## 相關檔案

* [透過 [!DNL Google Analytics] E-Commerce追蹤訂單轉介來源](../importing-data/integrations/google-ecommerce.md)
* [追蹤資料庫中的使用者反向連結來源](../analysis/google-track-user-acq.md)
* [追蹤資料庫中的使用者裝置、瀏覽器和作業系統資料](../analysis/track-usr-dev-browser.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連線您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [ [!DNL Google Analytics] UTM歸因如何運作？](../analysis/utm-attributes.md)
* [在 [!DNL Google Analytics]中進行UTM標籤的五個最佳實務](../../best-practices/utm-tagging-google.md)
