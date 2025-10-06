---
title: 篩選器
description: 瞭解如何使用篩選器。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 篩選器

可新增一或多個篩選器，以限制用於產生報表的資料。 每個篩選器都是一個運算式，其中包含關聯表格中的欄、運運算元和值。 例如，若只要包含回頭客戶，您可以建立僅包含已下多張訂單的客戶的篩選器。 多個篩選器可以與邏輯`AND/OR`運運算元一起使用，以將邏輯新增至報表。

>[!TIP]
>
>報表最多可包含3,500個資料點。 若要減少資料點的數量，請使用篩選器來減少用於產生報表的資料量。

[!DNL Adobe Commerce Intelligence]包含您可以「立即使用(OOTB)」或修改以符合您需求的篩選選項。 您可以建立的篩選器數量沒有限制。

## 若要新增篩選器：

1. 在圖表中，暫留在每個資料點上。

   在此報表中，每個資料點會顯示當月客戶總數。

1. 在左側面板中，按一下「篩選器」 （![篩選器圖示](../../assets/magento-bi-btn-filter.png)）圖示。

   ![新增篩選器](../../assets/magento-bi-report-builder-filter-add.png)

1. 按一下&#x200B;**[!UICONTROL Add Filter]**。

   篩選器依字母順序編號，第一個是`[A]`。 篩選的前兩個部分是下拉式選項，第三個部分是值。

   ![顯示新增篩選器選項的篩選器介面](../../assets/magento-bi-report-builder-filter-add-a.png)

   * 按一下篩選的第一個部分，然後選擇您要用來作為運算式主旨的欄。

     ![選擇篩選條件的第一部分](../../assets/magento-bi-report-builder-filter-part1.png)

   * 按一下篩選的第二個部分，然後選擇運運算元。

     ![選擇運運算元](../../assets/magento-bi-report-builder-filter-part2.png)

   * 在篩選的第三部分中，輸入完成運算式所需的值。

     ![輸入值](../../assets/magento-bi-report-builder-filter-part3.png)

   * 篩選完成時，按一下&#x200B;**[!UICONTROL Apply]**。

     報表現在僅包含回頭客戶，針對報表擷取的客戶記錄數量從33,000筆減少至12,600筆。

     ![已篩選的報告](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. 在側邊欄中，按一下透視（![透檢視示](../../assets/magento-bi-btn-perspective.png)）圖示。

   ![透視](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 在設定清單中，選擇`Cumulative`。 然後，按一下&#x200B;**[!UICONTROL Apply]**。

   ![累積透視](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   `Cumulative`觀點會隨時間分配變更，而不是顯示每個月的鋸齒狀上下變化。

1. 輸入報告的`Title`，然後按一下&#x200B;**[!UICONTROL Save]**&#x200B;將它當成`Chart`加入您的儀表板。

   ![儲存至儀表板](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
