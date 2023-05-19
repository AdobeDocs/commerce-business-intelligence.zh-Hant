---
title: 儀表板
description: 瞭解如何建立和使用儀表板。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 儀表板

[!DNL Adobe Commerce Intelligence] 儀表板可讓您快速查看您商店的效能和銷售活動。 單個儀表板可以與其他用戶共用並組織成邏輯組。 您也可以為其他用戶設定不同級別的權限。

建立報告、將其添加到儀表板以及將資料導出到Excel非常容易。 可以調整圖表和報表的大小，並將其拖放到儀表板上的位置。

![儀表板](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 建立儀表板 {#createdash}

儀表板是可共用的主題時段，用於在Report Builder中建立的分析。 這就是您如何鼓勵您的團隊協作，並在整個組織中維護單一的真相來源。

*如果您是管理員或標準用戶*，可通過按一下 `Dashboard Options` 下拉清單和選擇 `Create New dashboard`。

您建立的儀表板的外觀完全取決於您。 您可以根據需要和工作流在儀表板中排列和調整元素的大小。

![排列調整儀表板元素](../../assets/arrange_resize_dashboard_element.gif)

### 建立儀表板

1. 在菜單上，按一下 **[!UICONTROL Dashboards]**。

1. 預設儀表板的名稱出現在儀表板標題的左上角。 按一下向下箭頭(![](../../assets/magento-bi-btn-down.png))顯示可用選項。

   ![建立儀表板](../../assets/magento-bi-dashboard-create.png)

1. 按一下 **[!UICONTROL Create Dashboard]**。 然後，執行以下操作：

   * 輸入 `Name` 的下界。

   * 建立 `Group` 在儀表板中，輸入組的名稱。

      例如，如果Commerce安裝具有多個儲存視圖，則可以為每個儲存視圖建立一個組。

   * 按一下 **[!UICONTROL Create]**。

   ![儀表板名稱](../../assets/magento-bi-dashboard-create-name.png)

   * 新儀表板的名稱將出現在左上角。 按一下向下箭頭(![](../../assets/magento-bi-btn-down.png))。 如果建立了組，則新儀表板將出現在清單中組的下方。


### 添加報告

1. 要添加報告，請執行以下操作之一：

   * 按一下 **[!UICONTROL Add a report]** 提示。

   * 在儀表板標題中，按一下 **[!UICONTROL Add Report]**。

      ![添加報告](../../assets/magento-bi-dashboard-create-add-report.png)

1. 按一下 **[!UICONTROL Create Report]** 顯示 **[!UICONTROL Report Builder Options]**。

   ![Report Builder選項](../../assets/magento-bi-report-builder.png)

## 在儀表板上排列項目

* 要調整圖表或報表的大小，請將右下角拖動到新大小。

* 要移動圖表或報表，請將滑鼠懸停在標題或標題上，直到游標變為十字。 然後，將其拖到位置。

## 管理儀表板 {#managedash}

在 **[!DNL Manage Data** > **Dashboards]**，您可以管理您擁有的儀表板的用戶權限、刪除不再需要的儀表板以及設定預設儀表板。

### 共用儀表板 {#sharingdash}

真正擴展 [!DNL Commerce Intelligence] Adobe鼓勵您與其他團隊成員共用您建立的控制板，並提供有價值的見解。 *您可以共用自己的儀表板* 按一下 `Share Dashboard` 的上界。

在共用儀表板時，您可以在組織或組織中按個別基準分配權限，這意味著您有權決定誰可以查看和編輯您的報告。

>[!NOTE]
>
>`Read-Only` 用戶只能訪問直接與他們共用的儀表板 — 他們無法自行搜索和添加儀表板。 別忘了讓他們聽進去！

### 訪問共用儀表板 {#accessshared}

*如果您是管理員或標準用戶* 並希望將共用儀表板添加到帳戶，您可以通過按一下 **[!UICONTROL Dashboard Options]** 然後按一下 **[!UICONTROL Find]** 的下界。

![查找儀表板](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### 管理儀表板設定

1. 在菜單上，按一下 **[!DNL Manage Data** > **Dashboards]**。

1. 如果適用，請輸入新 `Dashboard Name`。

1. 將儀表板分配給特定 `Dashboard Group`，從組清單中選擇。

   **`Permissions`**

   要向所有用戶授予對儀表板的相同訪問級別，請執行以下操作：

   1. 下 **`Shared with`**，選擇以下選項之一：

      * `View`
      * `Edit`
      * `None`
   1. 提示確認時，按一下 **[!UICONTROL OK]** 更新每個用戶的權限級別。

   1. 要更改個人的權限級別，請在清單中查找用戶更改權限級別。 更改將自動保存。

   **`Default`**

   1. 要使此儀表板成為您的 [!DNL Commerce Intelligence] 帳戶，按一下 **[!UICONTROL Make Default]**。

   **`Remove`**

   1. 要刪除儀表板，請按一下 **[!UICONTROL Delete Dashboard]**。
