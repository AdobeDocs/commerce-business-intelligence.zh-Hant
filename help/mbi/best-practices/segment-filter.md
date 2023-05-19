---
title: 推薦的資料Dimension用於分段和過濾
description: 瞭解細分和篩選的最佳做法。
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# 分段和過濾

好的細分是將一個膚淺的統計資料轉化為一個商業指標來推動決策。

想知道您最有價值的客戶是誰嗎？ 您最有價值的營銷渠道是什麼？ 您的哪些產品移動得更快，原因何在？ 要找到這些答案，你必須從分割資料開始。

本主題涵蓋通常推薦給客戶的關鍵領域。 它還詳細介紹了這些部分可以幫助您回答哪些問題。 技術上，段是資料庫中的資料列。 在 [!DNL Adobe Commerce Intelligence]，它們稱為尺寸。

![](../../mbi/assets/mbi-critical-segments.png)


## 用戶段

用戶段可幫助您瞭解用戶的身份和用戶的行為。

* **年齡/出生年**:您的用戶有多大？ 您最活躍的用戶的年齡是多少？ 通常，將這些值儲存到範圍中以便更有效地分析是有意義的。
* **性別**:不同性別的人與你的網站有不同的互動嗎？
* **地址**:您的用戶來自何處？ 您是否應將營銷工作重點放在特定地區？ 您最近的廣告活動是否按預期在目標地區進行？
* **客戶採購來源**\:您知道您的用戶來自哪個營銷渠道嗎？ 他們是點擊廣告還是通過搜索找到你？ [按用戶獲取源分段資料](../data-analyst/analysis/google-track-user-acq.md) 是優化新客戶收購的第一步。 第二步是，在有效的產品上多花些錢，而在無效產品上多殺。
* **註冊裝置**:用戶是否通過您的移動應用或網站註冊？ iOS還是安卓？ 您的移動用戶群是否足夠大，能夠分配更多資源來開發您的移動產品？ 如果尚未跟蹤此內容，請參閱此主題 [關於跟蹤用戶設備](../data-analyst/analysis/track-usr-dev-browser.md)。
* **引用者**:誰是你最有影響力的人？ 有多少用戶被其他用戶直接引用？
* **工業**:如果你是B2B企業，你的用戶在哪些行業工作？ 哪些貿易組織值得加入？
* **調查響應**:如果執行客戶調查，請將響應用作更深入的分析級別的段。 您可以提出與您已經瞭解的用戶資訊相輔相成的問題，或確認您的猜測。
* **第一訂單金額和產品類別**:用戶的第一訂單模式與未來採購模式之間是否存在關聯？

## 訂單/事件段

訂單和事件段有助於分析用戶隨時間推移的行為和約定。

* **[!UICONTROL Billing / Shipping Address]**:你的大部分訂單都從哪來的？ 開單地址和發運地址之間是否存在差異？
* **[!UICONTROL Status]**:您有多少訂單未能完成？ 過去七天的待定訂單比率是多少？
* **[!UICONTROL Customer acquisition source]**:除了在用戶級別跟蹤用戶獲取資料外，您還可以 [在訂單或事件層跟蹤它](../data-analyst/analysis/google-track-user-acq.md)。 通過一個源註冊的用戶很可能會繼續通過其他源訪問您的站點。
* **[!UICONTROL Device]**:移動訂單數量是否在增加？ 您通過移動購買獲得了多少收入？ (如果您尚未跟蹤此內容，請參閱此主題 [關於跟蹤訂單設備資料](../data-analyst/analysis/track-usr-dev-browser.md)。
* **[!UICONTROL Fulfillment Center]**:您的哪個履行中心能夠產生最多的收入？ 如果您正在分析訂單時間與發運時間之間的差異，那麼哪個履行中心最能響應？
* **[!UICONTROL Delivery Carrier]**:哪家最受歡迎？ 哪個承運人的退貨數量最少？
* **[!UICONTROL Discount / Coupon Codes]**:您的促銷活動是否確實帶來了額外的業務？ 除了銷售的產品外，您的客戶還購買了多少額外的產品？ 優惠券如何影響平均訂單價值？ 折扣項目與非折扣項目的平均利潤是多少？
* **[!UICONTROL Satisfaction / Rating]**:您的客戶對他們的訂單有多滿意？ 您的客戶是否可能向您推薦業務？

## 產品段

產品分類可幫助您做出促銷決策。

* **[!UICONTROL Merchant / Brand]**:某個特定品牌的銷售速度是否快於其他品牌？ 哪些品牌表現不佳？
* **[!UICONTROL Type / Category]**:不同的用戶群是否享受不同類型的產品？ 哪些產品類別會產生最多的重複業務？
* **[!UICONTROL Discount / Coupon Codes]**:促銷是否影響了非折扣產品的銷售？ 優惠券如何影響您產品的感知價值？
* **[!UICONTROL Social Activity]**:社交媒體上產生的熱議與產品的銷量之間是否存在關聯？
* **[!UICONTROL Size / Variant]**:每種變型需要的庫存比率是多少？ 哪些變型可以按折扣率銷售？

如果你對商品銷售感興趣，請 [如何利用產品分類推動重複業務](../data-analyst/analysis/most-value-source-channel.md)。

## 建立客戶配置檔案

細分專家可能希望超越一維切片並開始建立真正的客戶配置檔案。 例如，13至24歲通過移動設備註冊的人將一個「Young &amp; Mobile」組放入了一個組。 與您的其他用戶群相比，此組的行為如何？

這類分析是《財富1000強》公司的營銷人員整天都在做的。 在基於雲的業務智慧平台出現之前， [!DNL Commerce Intelligence]對我們其他人來說，這幾乎是遙不可及的。 幸運的是，情況已經不是這樣了。

## 跟蹤新段

按上述維分段度量的第一步是確保跟蹤資料庫中的此資料。 如果未跟蹤，請與您的技術團隊會面，並找到開始跟蹤此資料的方法。

確認資料在資料庫中被跟蹤後， [與支援團隊聯繫](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 將尺寸推到 [!DNL Commerce Intelligence] 度量和圖表。 您還可以使用 *欄位管理* 用於跟蹤這些欄位的工具 [!DNL Commerce Intelligence]。

## 相關

* [優化資料庫以進行分析](../best-practices/opt-db-analysis.md)
