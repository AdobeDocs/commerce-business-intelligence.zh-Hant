---
title: 為投資者構建儀表板
description: 瞭解如何為投資者構建儀表板。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 構建投資者儀表板

許多客戶與投資者合作，需要從平台中共用資訊，但您為做出日常業務決策而建立的控制板，可能不是投資者想要的。 下面介紹了一些最佳做法，說明如何建立一個全面但簡單、非常適合與活躍和潛在投資者共用的儀表板。

以下是您為投資者儀表板建立報告所需的內容：

## 標量報表

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## 可視報告

* **[!UICONTROL Revenue by quarter]**
   * 指標 — 收入
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 指標 — 首次訂單收入
   * 篩選器 — 用戶的訂單編號等於1
   * 指標2 — 重複訂單收入
      * 篩選器 — 用戶的訂單號大於1
   * 取消選中「多Y軸」(Multiple Y-Axes)框
   * 更改為堆積柱形圖
* **[!UICONTROL AOV by quarter]**
   * 指標1 — 收入
      * 隱藏此度量
   * 指標2 — 訂單數
      * 隱藏此度量
   * 公式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 指標 — 收入
   * 按客戶分組 `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 指標 — 產品收入
      * 隱藏圖表
      * 按產品名稱分組。 選擇所有產品。
      * 將時間範圍設定為「全時」
      * 將時間間隔設定為「無」
      * 在「顯示頂部/底部」中，僅顯示按產品利潤排序的前10個
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 指標 — 不同的買家
      * 透視 — 累計
* **[!UICONTROL Site visits - New vs. repeat by month]**
* 會話

使用 [!DNL Google Analytics] 整合，您可以包括以下報告：

* 現場訪問
* 轉換率

使用 [Commerce Data Exchrity服務](https://business.adobe.com/products/magento/magento-commerce.html)，您可以包括以下報表：

* 按州/地區、年齡、性別分列的獨特客戶。

## 其他提示

* 使用清晰、簡潔的 [命名約定](../best-practices/naming-elements.md)
* 與投資者用戶共用儀表板
* 或通過 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 僅建立一個儀表板。 這使內容更易於維護，而且您完全知道您的投資者在看什麼。

精心組織報告，注重細節。 完成後，儀表板如下所示：

![](../../mbi/assets/investor-dboard-example.png)
