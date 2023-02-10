---
title: 提高廣告宣傳的投資報酬率
description: 了解評估行銷活動績效的幾種不同方法。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# 廣告宣傳與ROI

MBI讓您輕鬆 [結合廣告成本資料和收入資料](../../data-analyst/importing-data/integrations/google-adwords.md) 從資料庫。 這可協助您識別哪些促銷活動的投資報酬率最高。 在本文中，我們探討評估行銷活動績效的幾種不同方法。

## 必要條件

* 匯入廣告成本資料：
   * [連接您的 [!DNL Google AdWords] to [!DNL MBI]](../importing-data/integrations/google-adwords.md):這會自動同步您的 [!DNL Adwords] 花在 [!DNL MBI]
   * [上傳其他廣告成本資料](../importing-data/connecting-data/import-offline-ad-data.md):若沒有直接連接器，建議使用 [!DNL MBI]
   * 如果您從多個來源匯入成本資料，我們可以 [合併](../../best-practices/consolidating-your-tables.md) 中的資料 [!DNL MBI]. 簡單 [提交支援票證](../../guide-overview.md).
* [追蹤使用者贏取管道資料](../analysis/google-track-user-acq.md)

## 使用者贏取促銷活動

以使用者贏取為目標的促銷活動可從許多角度測量，包括：

1. 已取得促銷活動的新使用者人數
1. 促銷活動從註冊到購買的轉換率
1. 根據平均使用者期限值(LTV)的行銷活動ROI

以上分析(1)和(2)在關於 [識別最上層行銷管道](../analysis/most-value-source-channel.md). 在此，我們將探索分析(3)，以衡量一段時間內的促銷活動ROI。 這將回答從特定促銷活動獲得的使用者是否產生足夠的終身收入，以支付其贏取成本。

>[!NOTE]
>
>我們將假設所有促銷活動成本都專門用於贏取新用戶。 實際上，您的促銷活動成本也會與取得未轉換的造訪、重複購買者等項目共用。 但是，假設所有成本都用於獲取新註冊用戶，則最終的ROI將考慮最壞的情況（每次獲取的成本最高），因此您可以確定實際ROI高於我們的計算。
>
>範例：假設您在促銷活動上花費$20（促銷活動產生了10個新使用者和10個重複購買者），則每位新使用者的實際成本為$1，但根據我們的假設，為了贏取新使用者而花費的所有成本為$2。)

**1. 首先，請建立圖表，依促銷活動劃分廣告成本：**

1. 建立 [!UICONTROL Metric] 你花的時間
1. 前往 [!UICONTROL Data > Metrics]
1. 選擇 `Add New Metric` ，然後選取 [!DNL `Adwords...`] 記錄 [!DNL AdWords] 成本資料。
1. 在量度編輯器中，為量度命名(例如 [!UICONTROL AdWord Cost])
1. 使用下拉式清單，執行 **總和** 在 `adCost` 欄中 [!DNL Adwords...] 表格（變更）依 `date` 欄。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. 我們完蛋了。 按一下 `Back to Metric List` ，然後前往任何控制面板。

1. 建立依促銷活動劃分的區段支出報表
1. 在任何控制面板中，按一下 [!UICONTROL Add Report > Create new report]
1. 選取 [!UICONTROL Adword Cost] 量度
1. 設定 [!UICONTROL Time period] to `All-time`，和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 標籤，新增 `campaign` as [!UICONTROL grouping field]，然後按一下 `Add All` 框中。
1. 此報表會顯示您的 [!DNL AdWords] 行銷活動成本

**2. 接著，我們將建立報表，依促銷活動計算新使用者：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 選取 `New users` 計算一段時間內新註冊使用者人數的量度
1. 設定 [!UICONTROL Time period] to `All-time`，和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 標籤，新增 `campaign` as `grouping field`，然後按一下 **`Add All`** 框中
1. 此報表會依促銷活動顯示您所有已註冊的使用者

**3. 我們也可以建立報表，依促銷活動將平均使用者LTV分段：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 選取 `Average lifetime revenue` 計算平均使用者期限收入的量度
1. 設定 [!UICONTROL Time period] to `All-time`，和 [!UICONTROL Interval] to `None`
1. 在 `Group by` 標籤，新增 `campaign` 或 `utm\_campaign` as [!UICONTROL grouping field]，然後按一下 `Add All` 框中
1. 此報表將依促銷活動顯示您的平均使用者期限收入

**最後，我們將這三個分析整合在一份報表中，借此計算促銷活動的投資報酬率：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 新增作為輸入，我們將使用上述三個量度。 每個都會獲派一個字母(例如，\[`A`\], \[`B`\]和\[`C`\]
1. [!UICONTROL Cost]:新增量度AdWords成本 — 此量度將為變數\[A\]。 這只會讓行銷活動傳回成本。
1. [!UICONTROL Users]:新增量度「新使用者」 — 此量度將為變數\[B\]。 這只會傳回行銷活動的使用者人數。
1. [!UICONTROL LTV]:新增「平均期限收入」量度 — 此量度將為變數\[`C`\]。 這只會通過競選傳回LTV。

1. 按一下「圖表」旁的隱藏表徵圖，以便您能夠聚焦在表格上
1. 現在我們將使用 `Add Formula` 若要結合這些量度，如下所示：
1. [!UICONTROL ROI]:輸入公式 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`，若\[`A`\]代表 `Ad Cost by Campaigns`, \[`B`\]代表 `New users by campaigns`，和\[`C`\] `LTV by campaigns`. 這會傳回（平均使用者LTV — 每次贏取的平均成本）/（每次贏取的平均成本）的比率
1. [!UICONTROL Avg Return per User]:輸入公式 **\[`C`\]-(\[`A`\]/\[`B`\]**. 這會透過計算（平均使用者LTV） — （每次贏取的平均成本），傳回使用者的平均利潤。
1. [!UICONTROL CPA]:輸入公式 **`\[A\]/\[B\]`**. 這會傳回實際促銷活動的每次贏取成本。
1. 其他可能的量度，包括 [!DNL AdWords] 資料包括總和  `Impressions` 和 `adClicks` 從 [!DNL AdWords] 資料)，連同總計 `number of orders` 透過特定行銷活動所製作。
1. 根據LTV 30天和用戶註冊或首次購買後的90天來計算ROI也許也很有趣。

1. 您可以點按並拖曳量度和公式，重新排序報表的欄
1. 為報表命名，並確實儲存為表格。

## 產品行銷活動

您在經營產品特定的廣告嗎？ 若是如此，您可以透過計算特定產品的收入/成本來評估這些促銷活動的投資報酬率。

>[!NOTE]
>
>我們將假設所有促銷活動成本都專門用於產生特定產品的購買。 假設所有成本都花在了產生購買上，則最壞的情況（每次購買的成本最高）將包括所產生的ROI，因此您可以確定實際ROI高於此計算。 範例：假設您在產生10個新使用者和10個購買的促銷活動上花費了$20，則您的每次購買實際成本為$1，但根據我們的假設，購買新使用者的所有成本為$2。)*

開始之前， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 將以下維連接到行項表(`sales\_flat\_order\_item, order\_item`):

* 訂單的來源（如果您只追蹤使用者層級的反向連結來源，則加入使用者的來源）
* 訂購的促銷活動（如果您只追蹤使用者層級的反向連結來源，則加入使用者的促銷活動）
* 訂單的媒體（如果您只追蹤使用者層級的反向連結來源，則加入使用者的媒體）

**1. 現在，請先建立圖表，為特定產品傳回每個促銷活動的收入：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 選取 `Revenue by items` 計算行項目層收入的量度
1. 設定 [!UICONTROL Time period] to `All-time`，和 [!UICONTROL Interval] to `None`
1. 在 `Filter by` 標籤，新增 `product name 'IN'` 產品 `A`，產品 `B`，產品 `C`, ...」 並包含您的促銷活動所定位的所有產品名稱(例如， `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. 在 `Group by` 標籤，新增 `order's campaign` 或 `order's utm\_campaign` as `grouping` 欄位，然後按一下 **[!UICONTROL Add All]** 框中
1. 此報表會依促銷活動顯示特定產品的收入

**2. 若要計算ROI，我們將再次將量度合併成一個報表：**

1. 在任何控制面板中，按一下 **[!UICONTROL Add Report > Create new report]**
1. 新增 `Revenue by items` 量度，依據上方特定產品報表之促銷活動的指示進行篩選並分組，然後按一下 **[!UICONTROL Hide]** 在量度的標量值下
1. 現在新增 [!DNL AdWords Cost] 量度，依篩選器，並依來自 `Ad cost by campaigns` 在 `User acquisition campaigns` 上節；然後按一下 **[!UICONTROL Hide]** 在量度的標量值下
1. 現在，我們已備妥這些量度，並新增公式：
1. [!UICONTROL ROI]:輸入公式 `\[A\]/\[B\]`，如果 `\[A\]` 代表 `Revenue per campaign for specific product(s)` 和 `\[B\]` 代表 `Ad cost by campaigns`. 這會傳回（特定產品的收入）/（促銷活動成本）的比率
1. [!UICONTROL Return]:輸入公式 `\[A\]-\[B\]`. 這會透過計算（平均使用者LTV） — （每次贏取的平均成本），傳回使用者的平均利潤
1. （可選） [!UICONTROL Revenue]:取消隱藏 `Revenue by items` 量度，檢視每個促銷活動之特定產品的收入
1. （可選） [!UICONTROL Cost]:取消隱藏 `AdWords Cost` 可查看促銷活動成本的量度

1. 為報表命名，並確實將其儲存為表格

**3. 對您廣告的每個產品或產品群組重複上述步驟1和2。**

## 相關檔案

* [透過追蹤訂單轉介來源 [!DNL Google Analytics] 電子商務](../importing-data/integrations/google-ecommerce.md)
* [在您的資料庫中追蹤使用者反向連結來源](../analysis/google-track-user-acq.md)
* [在資料庫中追蹤使用者裝置、瀏覽器和作業系統資料](../analysis/track-usr-dev-browser.md)
* [探索您最有價值的贏取來源和管道](../analysis/most-value-source-channel.md)
* [連接您的 [!DNL Google Adwords] 帳戶](../importing-data/integrations/google-adwords.md)
* [如何 [!DNL Google Analytics] UTM歸因功能是否正常？](../analysis/utm-attributes.md)
* [5個UTM標籤最佳實務，位於 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
