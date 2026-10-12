---
title: 匯出原始資料
description: 瞭解如何從您的[!DNL Commerce Intelligence] Data Warehouse匯出記錄，以進一步瞭解為您的儀表板提供動力的原因。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Developer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
TQID: 'https://experienceleague.adobe.com/8n0DUwkiI1BVF5612vCd4jFWx7jwWlfOHg2K3hgWkco'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%
---
# 匯出原始資料

使用原始資料匯出，您可以從Data Warehouse匯出記錄，以更密切地瞭解為您的儀表板提供動力的內容。 此外，原始資料匯出可協助您[精確找出資料差異](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies)。

原始資料匯出可讓您存取透過取消標準化及預先彙總相關量度而產生的其他欄和維度。 例如，`User's first order date`是可為[!DNL Commerce Intelligence]中的每個使用者匯出的維度，但資料庫中可能無法使用。

本教學課程涵蓋下列內容：

* [選取要匯出的資料](#select)
* [正在下載匯出（`.csv`檔案）](#download)
* [存取歷史匯出](#historical)

## 步驟1：選取要匯出的資料 {#select}

有兩種方式可以在[!DNL Commerce Intelligence]中匯出原始資料：

1. 在圖表層級
1. 在表格層級

### 在[!UICONTROL Manage Data]索引標籤的表格層級匯出

若要從[!UICONTROL Manage Data]索引標籤匯出資料表，您需要[管理員](../administrator/user-management/user-management.md)許可權。

1. 按一下「**[!UICONTROL Manage Data** > **&#x200B;匯出資料&#x200B;**> **原始資料匯出]**」。
1. 您會看到`Export List`最近建立的資料匯出（如果有的話）。 按一下&#x200B;**[!UICONTROL Add Export]**&#x200B;以建立匯出。
1. `New Raw Data Export`對話方塊隨即顯示。 在這裡，您可以透過選取或取消選取欄和篩選器來自訂匯出：

   * `Table` - `Table`欄位會選取資料匯出的來源。 依預設，這會顯示您導覽至的表格。
   * `Export Name` — 在此欄位中，輸入匯出的名稱。 例如： `Philadelphia - Daily Revenue`。
   * `Available Columns` — 此欄位列出資料庫中可包含在匯出中的欄（維度）。 若要新增欄，請按一下其名稱。
   * `Selected Columns` — 此欄位列出目前包含在匯出中的欄（維度）。 若要移除欄，請按一下其名稱。
   * `Filter` — 此區段列出目前套用至匯出的篩選器。 這些篩選器可以變更；也可以新增篩選器以匯出特定資料集。
   * 完成時，按一下&#x200B;**[!UICONTROL Export Data]**。

### 從控制面板在圖表層級匯出

1. 按一下任何圖表右上角的齒輪圖示。

1. 從下拉式清單中選取`Raw Export`以顯示`Raw Export`對話方塊。

1. 選擇要包含或排除的`table`、`columns`和`filters`來自訂匯出。 請參閱上一節，以取得此模組欄位的詳細資訊。

   >[!NOTE]
   >
   >依預設，`Table`欄位中顯示的表格是提供圖表支援的表格。

1. 完成時，按一下&#x200B;**[!UICONTROL Export Data]**。

在圖表層級檢視整個程式。

![從圖表匯出原始資料的動畫示範](../assets/Chart-level_export.gif)

## 步驟2：下載匯出 {#download}

完成您在`Raw Data Export`對話方塊中的選取後，匯出將立即開始處理。 由於部分匯出內容可能較大，因此限製為1,000萬列，且可能需要一些時間才能執行。

若要檢查您的匯出是否已就緒，請按一下畫面右上角的&#x200B;**[!UICONTROL Raw Data Exports]**。 按一下&#x200B;**[!UICONTROL Download]**&#x200B;下載您匯出的壓縮`.csv`檔案。

![下載匯出CSV檔案的動畫示範](../assets/Downloading_export.gif)

## 步驟3：存取歷史匯出 {#historical}

若要檢視您過去的匯出專案，請按一下畫面右上角的&#x200B;**[!UICONTROL Raw Data Export]**。 待定和已完成的報表最長可存取7天。
