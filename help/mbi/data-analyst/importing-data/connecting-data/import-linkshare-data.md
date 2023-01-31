---
title: 匯入Linkshare資料
description: 了解如何將Linkshare資料匯入 [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 匯入 `Linkshare` 資料

將 `Linkshare` 資料 [!DNL MBI]，您需要執行兩項動作：

1. [將Linkshare資料匯出至 ](#export)
1. [將試算表上傳至 [!DNL MBI]](../connecting-data/using-file-uploader.md)

## 從Linkshare匯出資料 {#export}

1. 在 `Linkshare` 帳戶，轉到 **[!UICONTROL Reports** > **Run Reports].**

1. 在 `Report` 下拉式清單，選取 **[!UICONTROL Sales & Activity Report]**.

1. 將所有其他下拉式清單選項保留為預設選項。

1. 在 `Date Range` 下拉式清單，選取任何選項(`Sun - Sat`, `Mon - Sun`)符合您的 `Start of Week` 設定 [!DNL MBI].

1. 清除 `Compare Year-Over-Year Data` 核取方塊。

1. 在 `Data Type`，選取 `Transaction Date`.

   ![匯入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 按一下 **[!UICONTROL View Report]**.

1. 按一下 **[!UICONTROL Download]**.

   此時，a `.csv` 檔案即會建立及下載。

下載檔案後，您可將其上傳至 [!DNL MBI] 使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md).
