---
title: 格式化及匯入財務資料
description: 瞭解如何格式化和匯入財務資料。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# 格式化和匯入財務資料

此主題討論匯入財務資料以在[!DNL Adobe Commerce Intelligence]中分析的最佳方式。

二維交叉表資料表格通常是財務資料所使用的格式。 使用欄和列中的標籤分類值，這種型別的版面配置可能很容易以人類的眼睛和試算表工具檢視，但對資料庫不友好。

![以樞紐分析表配置顯示資料的交叉分析表格式](../../mbi/assets/crosstab.png)

若要在[!DNL Commerce Intelligence]中匯入和分析此資料，必須將資料表平面化為一維清單。 平面化時，每個資料值會依全都在單一列中的多個標籤進行分類，其中每一列都是唯一的，或會有唯一的識別碼，例如主鍵欄。

![以欄位版面配置顯示資料的平面化格式](../../mbi/assets/flattened.png)

## 格式化要匯入的Excel檔案

若要使用[!DNL Excel]樞紐分析表平面化二維資料表：

1. 使用二維資料表開啟檔案。
1. 開啟樞紐分析表精靈。 在[!DNL Windows]中，捷徑為`Alt-D`。 在[!DNL Mac OS]中，輸入`Command-Option-P`。
1. 選取&#x200B;**[!UICONTROL Multiple consolidated ranges]**&#x200B;並按一下&#x200B;**[!UICONTROL Next]**。
1. 選取&#x200B;**[!UICONTROL I will create the page fields]**&#x200B;並按一下&#x200B;**[!UICONTROL Next]**。
1. 在二維表格中選取整個資料集，包括標籤。 確定已針對所需的頁面欄位數選取`0`，然後按一下&#x200B;**[!UICONTROL Next]**。
1. 在新工作表中建立樞紐分析表，然後按一下&#x200B;**[!UICONTROL Finish]**。
1. 從欄位清單中取消選取欄和列的欄位。
1. 連按兩下產生的數值，在新頁面中顯示展平的來源資料。
   ![Excel樞紐分析表欄位清單顯示按兩下以展開](../../mbi/assets/pivot-table-double-click.png)
1. 儲存為`CSV`檔案。

## 正在結束

資料表已轉換為清單格式，保留其所有原始資訊，現在可以[匯入 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md)進行分析。
