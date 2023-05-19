---
title: 導入Linkshare資料
description: 學習將Linkshare資料導入 [!DNL Commerce Intelligence]。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 導入 [!DNL Linkshare] 資料

要將 [!DNL Linkshare] 資料 [!DNL Adobe Commerce Intelligence]你需要做兩件事：

1. [導出中的Linkshare資料 ](#export)
1. [將電子錶格上載到 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## 從Linkshare導出資料 {#export}

1. 在 [!DNL Linkshare] 帳戶，轉到 **[!UICONTROL Reports** > **Run Reports]。**

1. 在 `Report` 下拉清單，選擇 **[!UICONTROL Sales & Activity Report]**。

1. 將所有其它下拉選項保留為預設選擇。

1. 在 `Date Range` 下拉選項(`Sun - Sat`。 `Mon - Sun`與 `Start of Week` 設定 [!DNL Commerce Intelligence]。

1. 清除 `Compare Year-Over-Year Data` 複選框。

1. 下 `Data Type`選中 `Transaction Date`。

   ![導入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 按一下 **[!UICONTROL View Report]**。

1. 按一下 **[!UICONTROL Download]**。

   此時， `.csv` 檔案並下載。

下載檔案後，您可以將其上載到 [!DNL Commerce Intelligence] 使用 [`File Upload` 特徵](../connecting-data/using-file-uploader.md)。
