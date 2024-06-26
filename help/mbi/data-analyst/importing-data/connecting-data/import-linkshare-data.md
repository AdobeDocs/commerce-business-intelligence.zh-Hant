---
title: 匯入Linkshare資料
description: 瞭解如何將Linkshare資料匯入 [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# 匯入 [!DNL Linkshare] 資料

將您的 [!DNL Linkshare] 資料到 [!DNL Adobe Commerce Intelligence]，您必須執行下列兩件事：

1. [匯出Linkshare資料於 ](#export)
1. [上傳試算表至 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## 從Linkshare匯出資料 {#export}

1. 在您的 [!DNL Linkshare] 帳戶，前往 **[!UICONTROL Reports** > **Run Reports].**

1. 在 `Report` 下拉式清單，選取 **[!UICONTROL Sales & Activity Report]**.

1. 將所有其他下拉式清單選項保留為預設選項。

1. 在 `Date Range` 下拉式清單，選取任一選項(`Sun - Sat`， `Mon - Sun`)符合您的 `Start of Week` 中的設定 [!DNL Commerce Intelligence].

1. 清除 `Compare Year-Over-Year Data` 核取方塊。

1. 在 `Data Type`，選取 `Transaction Date`.

   ![匯入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 按一下 **[!UICONTROL View Report]**.

1. 按一下 **[!UICONTROL Download]**.

   此時， `.csv` 檔案和已下載。

下載檔案後，您可以將其上傳到 [!DNL Commerce Intelligence] 使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md).
