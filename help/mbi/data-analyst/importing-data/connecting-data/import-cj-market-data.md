---
title: 匯入CJ Affiliate (Commission Junction)行銷資料
description: 瞭解如何將CJ Affiliate (Commission Junction)資料匯入 [!DNL Commerce Intelligence].L Commerce Intelligence。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# 匯入[!DNL CJ Affiliate]資料

若要將[!DNL CJ Affiliate (Commission Junction)]資料匯入[!DNL Adobe Commerce Intelligence]，只要依照下列步驟將結果檔案附加至[支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)即可。 Adobe會設定您帳戶的資料表，並允許您繼續獨立上傳資料。

## 匯出[!DNL CJ Affiliate]資料

1. 在您的[!DNL CJ Affiliate]帳戶中，移至`Reports`標籤。

1. 在`Performance`索引標籤中，選取`Report Options`。

1. 將`Performance By`設定為等於`Program`、`Trend`設定為等於`Daily`，且`Date Range`設定為等於稽核的日期範圍。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選取`Run Report`。

1. 在`File Format`下拉式清單中，選取`CSV`。  按一下&#x200B;**[!UICONTROL Download]**。

   ![匯出cj附屬機構資料](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下載檔案之後，您可以[將檔案](../connecting-data/using-file-uploader.md)上傳至您的[!DNL Commerce Intelligence] Data Warehouse。

   這會在您的[!DNL Commerce Intelligence] Data Warehouse中建立表格，供您繼續定期上傳新資料至。 上傳檔案時，請遵循[使用檔案上傳程式](../connecting-data/using-file-uploader.md)中列出的格式要求。
