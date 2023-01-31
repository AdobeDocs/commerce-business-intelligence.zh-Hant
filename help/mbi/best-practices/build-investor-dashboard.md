---
title: 為投資者建立儀表板
description: 了解如何為投資者建立控制面板。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 建立投資者儀表板

我們的許多客戶都在與投資者合作，需要與他們共用來自平台的資訊，但您為做出日常業務決策而建立的控制面板，可能不是投資者想要的。 在此，我們將介紹一些最佳實務，說明如何建立全面但簡單的控制面板，以便與活躍和潛在投資者共用。

以下是您為投資者控制面板建立報表所需的內容：

## 標量報表

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## 視覺報表

* **[!UICONTROL Revenue by quarter]**
   * 量度 — 收入
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 量度 — 首次訂購收入
   * 篩選 — 使用者的訂單編號等於1
   * 量度2 — 重複訂購收入
      * 篩選器 — 用戶的訂單號大於1
   * 取消選中「多個Y軸」(Multiple Y-Axes)框
   * 變更為堆疊欄圖
* **[!UICONTROL AOV by quarter]**
   * 量度1 — 收入
      * 隱藏此量度
   * 量度2 — 訂購數
      * 隱藏此量度
   * 公式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 量度 — 收入
   * 依客戶分類 `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 量度 — 產品收入
      * 隱藏圖表
      * 依產品名稱分組。 選擇所有產品。
      * 將時間範圍設定為「全時」
      * 將時間間隔設定為「無」
      * 在「顯示頂部/底部」中，僅顯示按產品利潤排序的前10個
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 量度 — 不重複購買者
      * 透視 — 累積
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 工作階段

使用 [!DNL Google Analytics] 整合，您可以包含報表：

* 網站造訪
* 轉換率

使用 [商務資料擴充服務](https://business.adobe.com/products/magento/magento-commerce.html)，您可以包含的報表如下：

* 按州/地區、年齡、性別劃分的獨特客戶。

## 其他秘訣

* 使用簡潔明瞭 [命名約定](../best-practices/naming-elements.md)
* 與投資者使用者共用控制面板
* 或透過 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 僅建立一個控制面板。 這樣可讓內容更易於維護，您將確切了解您的投資者正在查看的內容。

周密地組織報告，並注意細節。 完成後，控制面板會如下所示：

![](../../mbi/assets/investor-dboard-example.png)
