---
title: 篩選器
description: 瞭解如何使用篩選器。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# 篩選器

可以添加一個或多個篩選器以限制用於生成報告的資料。 每個篩選器都是包含關聯表的列、運算子和值的表達式。 例如，要僅包括重複客戶，您可以建立一個篩選器，該篩選器僅包括已下達多個訂單的客戶。 多個篩選器可與邏輯 `AND/OR` 運算子，以將邏輯添加到報表。

>[!TIP]
>
>一個報告最多可以有3,500個資料點。 要減少資料點數，請使用篩選器來減少用於生成報告的資料量。

[!DNL Adobe Commerce Intelligence] 包括一些篩選器，您可以使用「出廠設定(OOTB)」或根據需要進行修改。 您可以建立的篩選器數量沒有限制。

## 要添加篩選器：

1. 在圖表中，將滑鼠懸停在每個資料點上。

   在此報表中，每個資料點都顯示當月的客戶總數。

1. 在左面板中，按一下「篩選器」(![](../../assets/magento-bi-btn-filter.png))。

   ![添加篩選器](../../assets/magento-bi-report-builder-filter-add.png)

1. 按一下 **[!UICONTROL Add Filter]**。

   篩選器按字母順序編號，第一個 `[A]`。 過濾器的前兩部分是下拉選項，第三部分是值。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 按一下篩選器的第一部分，然後選擇要用作表達式主題的列。

      ![選擇篩選器的第一部分](../../assets/magento-bi-report-builder-filter-part1.png)

   * 按一下濾鏡的第二部分，然後選擇運算子。

      ![選擇運算子](../../assets/magento-bi-report-builder-filter-part2.png)

   * 在篩選器的第三部分，輸入完成表達式所需的值。

      ![輸入值](../../assets/magento-bi-report-builder-filter-part3.png)

   * 過濾器完成後，按一下 **[!UICONTROL Apply]**。

      此報告現在僅包括重複的客戶，並且檢索到的用於該報告的客戶記錄數已從33,000減少到12,600。

      ![篩選的報告](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 在提要欄中，按一下透視( ![](../../assets/magento-bi-btn-perspective.png))。

   ![透視](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 在設定清單中，選擇 `Cumulative`。 然後，按一下 **[!UICONTROL Apply]**。

   ![累積透視](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   的 `Cumulative` 透視會隨時間而分佈變化，而不是每個月顯示鋸齒和鋸齒。

1. 輸入 `Title` ，然後按一下 **[!UICONTROL Save]** 它 `Chart` 到儀表板。

   ![保存到儀表板](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
