---
title: 導入MailChimp資料
description: 學習將MailChimp資料導入 [!DNL Commerce Intelligence]。
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 導入 [!DNL Mailchimp] 資料

要全面瞭解您的競選活動，您可以導入 [!DNL Mailchimp] 電子郵件市場活動資料 [!DNL Commerce Intelligence]。 要完成導入，您需要對每個 [!DNL Mailchimp] 您擁有的市場活動：

## 導出開啟資料 {#opens}

1. 登錄後 [!DNL Mailchimp]，轉到 `Campaigns` 頁籤。

   ![導入mailchim 1](../../../assets/import-mailchimp-1.png)

1. 按一下 **[!UICONTROL View Report]**，在活動名稱旁邊。

   ![導入mailchim 2](../../../assets/import-mailchimp-2.png)

1. 按一下 **[!UICONTROL Opened]** 數。

   ![導入mailchim3](../../../assets/import-mailchimp-3.png)

1. 按一下 **[!UICONTROL Export]** 並保存 `.csv` 的子菜單。

   必須添加 `primary key`。 `date (mm/dd/yyyy)`, `campaign name` 列。 確保 `primary keys` 對每行都是唯一的。

   ![導入mailchim 4](../../../assets/import-mailchimp-4.png)

## 導出按一下資料 {#clicks}

1. 導航到 `View Report` 螢幕。

1. 按一下 `Clicked`。

   ![導入郵件連結5](../../../assets/import-mailchimp-5.png)

1. 按一下 `Total Clicks` 或 `Unique Clicks` 的雙曲餘切值。

   ![導入郵件連結6](../../../assets/import-mailchimp-6.png)

1. 按一下 **[!UICONTROL Export]** 並保存 `.csv` 的子菜單。

   必須添加 `Primary Key`。 `date (mm/dd/yyyy)`。 `campaign name`, `URL` 列。 您不需要添加完整的URL，只是添加一些讓您知道點擊了什麼的內容。

   ![導入郵件連結7](../../../assets/import-mailchimp-7.png)

1. 對電子郵件中按一下的每個URL重複步驟3和4，將所有資料合併到同一個 `.csv` 的子菜單。

## 導出發送的資料 {#sent}

1. 進入 `Campaigns` 頁籤 [!DNL Mailchimp]。

1. 按一下 **[!UICONTROL View Report]** 選項。

1. 按一下旁邊的數字 `Recipients`。

   ![導入mailchim8](../../../assets/import-mailchimp-8.png)

1. 按一下 **[!UICONTROL Export]** 並保存 `.csv` 的子菜單。

   必須添加 `Primary Key`。 `date (mm/dd/yyyy)`, `campaign name` 列。

   ![導入郵件連結9](../../../assets/import-mailchimp-9.png)

## 準備檔案以上載到 [!DNL Commerce Intelligence] {#upload}

每個檔案 —  `Opens`。 `Clicks`, `Sent`  — 應上載到 [!DNL Commerce Intelligence] 檔案。 Adobe建議使用此命名約定命名檔案： `MailChimp\_ACTION\_DATE`。 替換 `ACTION` 與 `Open`。 `Click`或 `Sent`，替換 `DATE` 和導出日期。

準備好上載檔案時，請使用 [`File Upload` 特徵](../connecting-data/using-file-uploader.md) 將資料帶入Data Warehouse。
