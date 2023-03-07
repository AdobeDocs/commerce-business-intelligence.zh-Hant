---
title: 導入MailChimp資料
description: 了解如何將MailChimp資料匯入 [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 匯入 `MailChimp` 資料

若要全面了解您的宣傳活動成果，您可以匯入 `MailChimp` 將行銷活動資料傳送至 [!DNL MBI]. 若要完成匯入，您必須對每個 `MailChimp` 您擁有的行銷活動：

## 匯出開啟的資料 {#opens}

1. 登入後 `MailChimp`，前往 `Campaigns` 標籤。

   ![導入mailchimp 1](../../../assets/import-mailchimp-1.png)

1. 按一下 **[!UICONTROL View Report]**，位於促銷活動名稱旁。

   ![導入mailchimp 2](../../../assets/import-mailchimp-2.png)

1. 按一下 **[!UICONTROL Opened]** 數字。

   ![導入mailchimp 3](../../../assets/import-mailchimp-3.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `primary key`, `date (mm/dd/yyyy)`，和 `campaign name` 欄。 請確定 `primary keys` 對每一列都是唯一的。

   ![導入mailchimp 4](../../../assets/import-mailchimp-4.png)

## 匯出點按次數資料 {#clicks}

1. 導覽回 `View Report` 螢幕。

1. 按一下 `Clicked`.

   ![導入mailchimp 5](../../../assets/import-mailchimp-5.png)

1. 按一下 `Total Clicks` 或 `Unique Clicks` 欄。

   ![導入mailchimp 6](../../../assets/import-mailchimp-6.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`，和 `URL` 欄。 您不需要新增完整的URL，只是可讓您知道已點按的內容。

   ![導入mailchim 7](../../../assets/import-mailchimp-7.png)

1. 對於在電子郵件中點按的每個URL，重複步驟3和4，將所有資料合併成相同的 `.csv` 檔案時填入。

## 匯出已傳送的資料 {#sent}

1. 進入 `Campaigns` 頁簽。

1. 按一下 **[!UICONTROL View Report]** 行銷活動名稱旁邊。

1. 按一下旁邊的數字 `Recipients`.

   ![導入mailchimp 8](../../../assets/import-mailchimp-8.png)

1. 按一下 **[!UICONTROL Export]** 並儲存 `.csv` 檔案。

   您必須新增 `Primary Key`, `date (mm/dd/yyyy)`，和 `campaign name` 欄。

   ![導入mailchim 9](../../../assets/import-mailchimp-9.png)

## 準備要上傳至的檔案 [!DNL MBI] {#upload}

每個檔案 —  `Opens`, `Clicks`，和 `Sent`  — 應上傳至 [!DNL MBI] 檔案。 Adobe建議您使用此命名慣例為檔案命名： `MailChimp\_ACTION\_DATE`. 取代 `ACTION` with `Open`, `Click`，或 `Sent`，取代 `DATE` 和出口日期。

準備好上傳檔案時，請使用 [`File Upload` 功能](../connecting-data/using-file-uploader.md) 將資料帶入您的Data Warehouse。
