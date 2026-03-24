---
title: 為投資者建立儀表板
description: 瞭解如何為投資者建立儀表板。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Developer, User
feature: Dashboards, Data Integration
TQID: https://experienceleague.adobe.com/0G3u84SK-CvA7Pvb5bI-uEkUkbi9oiYvWwJHRwd-568
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 289
ht-degree: 0%

---

# 建立投資者儀表板

許多客戶都與投資者合作，並且需要從平台分享資訊，但您為進行日常業務決策而建立的儀表板可能不是投資者所尋求的。 以下說明如何建立完整但簡單的儀表板的一些最佳實務，最適合與活躍和潛在投資者分享。

以下是為投資者儀表板建立報告所需的內容：

## 純量報表

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## 視覺化報表

* **[!UICONTROL Revenue by quarter]**
   * 量度 — 收入
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 量度 — 首次訂購收入
      * 篩選器 — 使用者的訂單編號等於1
   * 量度2 — 重複訂購收入
      * 篩選器 — 使用者的訂單編號大於1
   * 取消勾選多個Y軸的方塊
   * 變更為棧疊式柱狀圖
* **[!UICONTROL AOV by quarter]**
   * 量度1 — 收入
      * 隱藏此量度
   * 量度2 — 訂單數
      * 隱藏此量度
   * 公式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 量度 — 收入
   * 依客戶的`utm_source`分組
* **[!UICONTROL Revenue from top 10 products]**
   * 量度 — 產品收入
      * 隱藏圖表
      * 依產品名稱分組。 選取所有產品。
      * 將時間範圍設定為「所有時間」
      * 將時間間隔設定為「無」
      * 在「顯示排名前/最後」中，僅顯示依產品利潤排列的排名前10位
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 量度 — 不同的購買者
      * 透視 — 累積
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 工作階段

透過[!DNL Google Analytics]整合，您可以包含下列報表：

* 網站造訪
* 轉換率

透過[Commerce資料擴充服務](https://business.adobe.com/tw/products/magento/magento-commerce.html)，您可以包含下列報表：

* 依州/地區、年齡、性別區分的不重複客戶。

## 其他秘訣

* 使用簡潔明瞭的[命名慣例](../best-practices/naming-elements.md)
* 與投資者使用者共用控制面板
* 或透過&#x200B;**[!UICONTROL Automated email summary]**&#x200B;傳送(../data-user/export-data/email-summaries.md)
* 僅建立一個儀表板。 這樣可讓內容更容易維護，而且您清楚知道投資者在看什麼。

周詳地組織報告，並注意詳細資訊。 完成後，控制面板看起來類似以下畫面：

![建立投資者儀表板](../../mbi/assets/investor-dboard-example.png)
