---
title: 匯入MailChimp資料
description: 瞭解如何將MailChimp資料匯入 [!DNL Commerce Intelligence]。
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# 匯入[!DNL Mailchimp]資料

若要全面瞭解您的行銷活動，您可以將[!DNL Mailchimp]電子郵件行銷活動資料匯入[!DNL Commerce Intelligence]。 若要完成匯入，您必須針對每個[!DNL Mailchimp]行銷活動執行下列動作：

## 匯出開啟的資料 {#opens}

1. 登入[!DNL Mailchimp]後，移至`Campaigns`標籤。

   ![匯入mailchimp 1](../../../assets/import-mailchimp-1.png)

1. 按一下行銷活動名稱旁的&#x200B;**[!UICONTROL View Report]**。

   ![匯入mailchimp 2](../../../assets/import-mailchimp-2.png)

1. 按一下&#x200B;**[!UICONTROL Opened]**&#x200B;數字。

   ![匯入mailchimp 3](../../../assets/import-mailchimp-3.png)

1. 按一下&#x200B;**[!UICONTROL Export]**&#x200B;並儲存`.csv`檔案。

   您必須新增`primary key`、`date (mm/dd/yyyy)`和`campaign name`欄至此檔案。 請確定每一列的`primary keys`都是唯一的。

   ![匯入mailchimp 4](../../../assets/import-mailchimp-4.png)

## 匯出點按資料 {#clicks}

1. 導覽回促銷活動的`View Report`畫面。

1. 按一下`Clicked`的數字。

   ![匯入mailchimp 5](../../../assets/import-mailchimp-5.png)

1. 按一下`Total Clicks`或`Unique Clicks`資料行下的數字。

   ![匯入mailchimp 6](../../../assets/import-mailchimp-6.png)

1. 按一下&#x200B;**[!UICONTROL Export]**&#x200B;並儲存`.csv`檔案。

   您必須新增`Primary Key`、`date (mm/dd/yyyy)`、`campaign name`和`URL`欄至此檔案。 您不需要新增完整URL，只要讓您知道已點按哪些內容即可。

   ![匯入mailchimp 7](../../../assets/import-mailchimp-7.png)

1. 對電子郵件中按下的每個URL重複步驟3和4，完成後，將所有資料合併到相同的`.csv`檔案中。

## 匯出已傳送的資料 {#sent}

1. 進入`Campaigns`的[!DNL Mailchimp]標籤。

1. 按一下行銷活動名稱旁的&#x200B;**[!UICONTROL View Report]**。

1. 按一下`Recipients`旁邊的數字。

   ![匯入mailchimp 8](../../../assets/import-mailchimp-8.png)

1. 按一下&#x200B;**[!UICONTROL Export]**&#x200B;並儲存`.csv`檔案。

   您必須新增`Primary Key`、`date (mm/dd/yyyy)`和`campaign name`欄至此檔案。

   ![匯入mailchimp 9](../../../assets/import-mailchimp-9.png)

## 準備檔案以上載至[!DNL Commerce Intelligence] {#upload}

每個檔案 — `Opens`、`Clicks`和`Sent` — 都應該以個別檔案的形式上傳到[!DNL Commerce Intelligence]。 Adobe建議您使用此命名慣例來命名檔案： `MailChimp\_ACTION\_DATE`。 以`ACTION`、`Open`或`Click`取代`Sent`，並以匯出日期取代`DATE`。

當您準備好上傳檔案時，請使用[`File Upload`功能](../connecting-data/using-file-uploader.md)將資料帶入您的Data Warehouse。
