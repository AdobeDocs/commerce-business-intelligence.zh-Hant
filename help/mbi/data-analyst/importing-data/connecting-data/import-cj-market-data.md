---
title: 匯入CJ附屬機構（委託章節）行銷資料
description: 了解如何將CJ附屬機構(Commission Junction)資料匯入 [!DNL MBI].L MBI]。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 匯入 `CJ Affiliate` 資料

匯入 `CJ Affiliate` （委託章克申）資料 [!DNL MBI]，只需依照下列步驟操作，並將產生的檔案附加至支援票證即可。 我們會設定您帳戶的資料表，允許您繼續獨立上傳資料。

## 匯出 `CJ Affiliate` 資料

1. 在 `CJ Affiliate` 帳戶，請前往 `Reports` 標籤。

1. 在 `Performance` 索引標籤，選取 `Report Options`.

1. 設定 `Performance By` 等於 `Program`, `Trend` 等於 `Daily`，和 `Date Range` 等於要稽核的日期範圍。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選擇 `Run Report`.

1. 在 `File Format` 下拉式清單，選取 `CSV`.  按一下 **[!UICONTROL Download]**.

   ![導出cj附屬資料](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. 下載檔案後，您可以 [上傳檔案](../connecting-data/using-file-uploader.md) 至 [!DNL MBI] 資料倉庫。

   這會在您的 [!DNL MBI] 資料倉庫，您可以繼續定期將最新資料上傳至。 上傳檔案時，請務必遵循 [使用檔案上傳程式](../connecting-data/using-file-uploader.md).
