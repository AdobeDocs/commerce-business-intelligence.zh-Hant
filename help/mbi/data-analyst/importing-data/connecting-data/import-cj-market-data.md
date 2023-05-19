---
title: 導入CJ關聯(Commission Junction)營銷資料
description: 學習將CJ關聯(Commission Junction)資料導入 [!DNL Commerce Intelligence].L Commerce Intelligence]。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 導入 [!DNL CJ Affiliate] 資料

導入 [!DNL CJ Affiliate (Commission Junction)] 資料 [!DNL Adobe Commerce Intelligence]，只需按照以下步驟操作，並將生成的檔案附加到 [支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。 Adobe將設定您的帳戶的資料表，並允許您繼續獨立上載資料。

## 導出 [!DNL CJ Affiliate] 資料

1. 在 [!DNL CJ Affiliate] 帳戶，轉到 `Reports` 頁籤。

1. 在 `Performance` 頁籤 `Report Options`。

1. 設定 `Performance By` 等於 `Program`。 `Trend` 等於 `Daily`, `Date Range` 等於正在審計的日期範圍。

   ![導出 — cj關聯資料](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選擇 `Run Report`。

1. 在 `File Format` 下拉清單，選擇 `CSV`。  按一下 **[!UICONTROL Download]**。

   ![導出cj關聯資料](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下載完檔案後，您可以 [上載檔案](../connecting-data/using-file-uploader.md) 到 [!DNL Commerce Intelligence] Data Warehouse。

   這將在 [!DNL Commerce Intelligence] Data Warehouse，您可以繼續定期將新資料上載到。 上載檔案時，請遵循中列出的格式要求 [使用檔案上載程式](../connecting-data/using-file-uploader.md)。
