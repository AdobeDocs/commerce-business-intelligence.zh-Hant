---
title: 分段和篩選的建議資料Dimension
description: 瞭解細分和篩選的最佳實務。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# 細分和篩選

良好的細分可將表面統計轉變為推動決策的商務量度。

想知道您最有價值的客戶是誰？ 您最有價值的行銷管道為何？ 您的哪些產品移動得更快？為什麼？ 若要取得上述任何答案，您必須先將資料分段。

本主題涵蓋經常向客戶建議的關鍵區段。 此外，也會詳細說明這些區段可協助您回答的問題。 技術上，區段是資料庫中的資料欄。 在[!DNL Adobe Commerce Intelligence]中，這些維度稱為維度。

![](../../mbi/assets/mbi-critical-segments.png)


## 使用者區段

使用者區段可協助您瞭解使用者的身分和行為方式。

* **年齡/出生年**：您的使用者年齡為何？ 您最活躍的使用者年齡為何？ 通常將值分組到範圍中以進行更有效的分析是有意義的。
* **性別**：不同的性別與您的網站互動方式是否不同？
* **位址**：您的使用者來自何處？ 您應該將行銷工作聚焦於特定地區嗎？ 您最近的廣告行銷活動是否在目標區域如預期般執行？
* **客戶贏取來源**\：您知道使用者來自哪個行銷管道嗎？ 他們是否點按廣告或透過搜尋找到您？ [依使用者贏取來源將資料分段](../data-analyst/analysis/google-track-user-acq.md)是最佳化新客戶贏取的第一步。 第二步是花更多錢在有效果上，並扼殺無效果實。
* **註冊裝置**：使用者是否透過您的行動應用程式或網站註冊？ iOS或Android™？ 您的行動使用者基礎是否夠大，可以配置更多資源來開發您的行動產品？ 如果您尚未追蹤此專案，請參閱此主題[關於追蹤使用者裝置](../data-analyst/analysis/track-usr-dev-browser.md)。
* **由**&#x200B;推薦：誰是您最有影響力的人？ 有多少位使用者被其他人直接參照？
* **產業**：如果您是B2B企業，您的使用者在哪些產業工作？ 哪些貿易組織值得加入？
* **調查回應**：如果您執行客戶調查，請將回應當成區段，以更深入的分析層級。 您可以提出問題，以補充您已瞭解的使用者情況，或確認您的猜測。
* **第一筆訂單金額與產品類別**：使用者的第一筆訂單與未來的購買模式之間是否有關聯？

## 訂單/事件區段

訂單和事件區段可協助分析一段時間內的使用者行為和參與度。

* **[!UICONTROL Billing / Shipping Address]**：您大部分的訂單來自何處？ 帳單和運送地址之間是否有差異？
* **[!UICONTROL Status]**：您有多少訂單無法完成？ 過去七天擱置訂單的比率是多少？
* **[!UICONTROL Customer acquisition source]**：除了在使用者層級追蹤使用者贏取資料之外，您還可以在訂單或事件層級[追蹤資料。 ](../data-analyst/analysis/google-track-user-acq.md)透過一個來源註冊的使用者完全可以繼續透過其他來源存取您的網站。
* **[!UICONTROL Device]**：行動訂單的數量是否增加？ 您的收入中有多少是透過行動裝置購買產生的？ (如果您尚未追蹤此專案，請參閱此主題[關於追蹤順序裝置資料](../data-analyst/analysis/track-usr-dev-browser.md)。
* **[!UICONTROL Fulfillment Center]**：您的哪個履行中心產生最多收入？ 如果您正在分析訂單時間與出貨時間之間的差異，哪一個履行中心的回應速度最快？
* **[!UICONTROL Delivery Carrier]**：哪一個是最受歡迎的電信業者？ 哪個電信業者傳回的專案數最少？
* **[!UICONTROL Discount / Coupon Codes]**：您的促銷活動是否確實帶來額外的業務？ 除了待售專案外，您的客戶還購買了多少額外專案？ 優惠券如何影響平均訂購值？ 折扣與非折扣專案的平均利潤是多少？
* **[!UICONTROL Satisfaction / Rating]**：您的客戶對其訂單的滿意度為何？ 您的客戶可能會將業務轉介給您嗎？

## 產品區段

產品區段可協助您進行銷售決策。

* **[!UICONTROL Merchant / Brand]**：某個特定品牌的銷售速度是否比其他品牌快？ 哪些品牌表現不佳？
* **[!UICONTROL Type / Category]**：不同的使用者區段是否享有不同型別的產品？ 哪些產品類別產生的重複業務最多？
* **[!UICONTROL Discount / Coupon Codes]**：促銷是否會影響非折扣產品的銷售？ 優惠券如何影響產品的感知價值？
* **[!UICONTROL Social Activity]**：社群媒體產生的熱門話題與產品的銷售量之間是否有關聯？
* **[!UICONTROL Size / Variant]**：您需要每個變體的詳細目錄比率是多少？ 哪些變體可以折扣率出售？

如果您對銷售感興趣，請檢視[如何使用產品區段來推動重複業務](../data-analyst/analysis/most-value-source-channel.md)。

## 建立客戶設定檔

細分專家可能想要超越一維切片，並開始建立真正的客戶個人檔案。 例如，年齡介於13到24歲之間且透過行動裝置註冊的人，會加入一個名為「Young &amp; Mobile」的群組。 此群組的行為與您其他使用者群相比如何？

這類分析就是《財富》1000強公司的行銷人員一整天都在做的事。 在[!DNL Commerce Intelligence]等雲端型商業智慧平台出現之前，我們其他人基本上無法企及。 幸運的是，現在情況已完全不同。

## 追蹤新區段

依照上述維度來劃分量度的第一個步驟，就是確定您正在資料庫中追蹤此資料。 如果未受到追蹤，請和您的技術團隊會面，並找到開始追蹤此資料的方法。

確認資料庫已追蹤資料後，[請連絡支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hant)，將維度推送至[!DNL Commerce Intelligence]量度和圖表。 您也可以使用&#x200B;*欄位管理*&#x200B;工具來追蹤[!DNL Commerce Intelligence]中的這些欄位。

## 相關

* [最佳化資料庫以進行分析](../best-practices/opt-db-analysis.md)
