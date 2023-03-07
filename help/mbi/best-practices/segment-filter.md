---
title: 分段和篩選的建議資料Dimension
description: 了解分段和篩選的最佳實務。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# 細分與篩選

良好的細分將膚淺的統計資料轉化為推動決策的業務量度。

想知道您最有價值的客戶是誰嗎？ 您最有價值的行銷管道是什麼？ 您的哪些產品進展得更快，原因為何？ 若要取得這些答案，您必須從劃分資料開始。

本文涵蓋經常建議給客戶的重要區段。 也會詳細說明這些區段可協助您回答的問題。 技術上，區段是資料庫中的資料欄。 在 [!DNL MBI]，即稱為維度。

![](../../mbi/assets/mbi-critical-segments.png)


## 使用者區段

使用者區段可協助您了解使用者的身分及其行為。

* **年齡/出生年**:您的使用者幾歲？ 您最活躍的使用者的年齡為何？ 將值分段至範圍以進行更有效的分析通常可行。
* **性別**:不同性別的人與您的網站互動是否不同？
* **地址**:您的使用者來自何處？ 您是否應將行銷重點放在特定地區？ 您最近的廣告促銷活動在目標地區是否如預期般執行？
* **客戶贏取來源**\:您知道您的使用者來自哪些行銷管道嗎？ 他們是按一下廣告，還是透過搜尋找到您？ [依使用者贏取來源分段資料](../data-analyst/analysis/google-track-user-acq.md) 是最佳化新客戶贏取的第一步。 第二步是投入更多資金，去殺掉那些沒有用的東西。
* **註冊裝置**:使用者是否透過您的行動應用程式或網站註冊？ iOS還是Android™? 您的行動使用者群是否足夠大，足以配置更多資源來開發您的行動產品？ (如果您尚未追蹤此內容，請參閱本主題 [關於追蹤使用者裝置](../data-analyst/analysis/track-usr-dev-browser.md).
* **引用者**:誰是你最有影響力的人？ 其他人直接轉介了多少個使用者？
* **產業**:如果您是B2B企業，您的使用者會在哪些行業工作？ 哪些貿易組織值得加入？
* **調查回應**:如果您執行客戶調查，請將回應作為區段，以便進行更深入的分析。 您可以提出與已知使用者相關的問題，或確認您的猜測。
* **首次訂購金額和產品類別**:使用者的首次訂購與未來購買模式之間是否有關聯？

## 訂購/事件區段

順序和事件區段有助於分析使用者行為和隨時間變化的參與度。

* **[!UICONTROL Billing / Shipping Address]**:你的大部分訂單都來自哪裡？ 帳單地址和發運地址之間是否有差異？
* **[!UICONTROL Status]**:您的訂單中有多少未能完成？ 過去七天的待定訂單比例是多少？
* **[!UICONTROL Customer acquisition source]**:除了在使用者層級追蹤使用者贏取資料，您也可以 [在訂單或事件層級上追蹤](../data-analyst/analysis/google-track-user-acq.md). 透過一個來源註冊的使用者很可能會繼續透過其他來源存取您的網站。
* **[!UICONTROL Device]**:行動訂單數量是否在增加？ 您的收入中有多少是透過行動購買產生的？ (如果您尚未追蹤此內容，請參閱本主題 [關於追蹤訂購設備資料](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**:您的哪個履行中心產生的收入最多？ 如果您正在分析訂單時間和發運時間之間的差異，那麼哪個履行中心響應最快？
* **[!UICONTROL Delivery Carrier]**:哪家航空公司最受歡迎？ 哪個承運人返回的項目數最少？
* **[!UICONTROL Discount / Coupon Codes]**:您的促銷活動是否實際上會產生額外業務？ 除了銷售的商品外，您的客戶還購買了多少額外的商品？ 抵用券如何影響平均訂購值？ 折扣項目與非折扣項目的平均利潤是多少？
* **[!UICONTROL Satisfaction / Rating]**:您的客戶對其訂單的滿意度如何？ 您的客戶是否可能將業務推薦給您？

## 產品區段

產品區段可協助您做出銷售決策。

* **[!UICONTROL Merchant / Brand]**:某個特定品牌的銷售速度是否高於其他品牌？ 哪些品牌表現欠佳？
* **[!UICONTROL Type / Category]**:不同的使用者區段是否享有不同的產品類型？ 哪些產品類別產生的重複率最高？
* **[!UICONTROL Discount / Coupon Codes]**:促銷是否會影響非折扣產品的銷售？ 抵用券如何影響產品的感知價值？
* **[!UICONTROL Social Activity]**:社交媒體上產生的熱門話題與產品的銷售量是否有關聯？
* **[!UICONTROL Size / Variant]**:每個變體需要的庫存比率是多少？ 哪些變體可以以貼現率出售？

如果您對商品銷售感興趣，請查看 [如何使用產品區段來促進重複業務](../data-analyst/analysis/most-value-source-channel.md).

## 建立客戶設定檔

區段專家可能想要超越一維片段，開始建立真正的客戶設定檔。 例如，13至24歲之間，透過行動裝置註冊的人放入「Young &amp; Mobile」群組。 此群組的行為與您其他使用者群有何不同？

這類分析是《財富1000強》公司的行銷人員整天都在做的。 在雲基商業智慧平台出現之前，例如 [!DNL MBI]而我們其他人則無法承受。 幸運的是，情況已經不是這樣了。

## 追蹤新區段

依上述維度劃分量度的第一步，是確定您要在資料庫中追蹤此資料。 如果未追蹤，請洽詢您的技術團隊，並尋找開始追蹤此資料的方式。

在您確認資料庫中已追蹤資料後， [聯絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 將維度推送至 [!DNL MBI] 度量和圖表。 您也可以使用 *欄位管理* 工具來追蹤 [!DNL MBI].

## 相關

* [優化資料庫以進行分析](../best-practices/opt-db-analysis.md)
