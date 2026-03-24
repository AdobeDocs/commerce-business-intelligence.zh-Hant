---
title: 匯入Linkshare資料
description: 瞭解如何將Linkshare資料匯入 [!DNL Commerce Intelligence]。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
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
source-wordcount: 94
ht-degree: 0%

---

# 匯入[!DNL Linkshare]資料

若要將您的[!DNL Linkshare]資料帶入[!DNL Adobe Commerce Intelligence]，您必須執行下列兩件事：

1. [匯出Linkshare資料於 &#x200B;](#export)
1. [將試算表上傳至 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## 從Linkshare匯出資料 {#export}

1. 在您的[!DNL Linkshare]帳戶中，移至&#x200B;**[!UICONTROL Reports** > **Run Reports].**

1. 在`Report`下拉式清單中，選取&#x200B;**[!UICONTROL Sales & Activity Report]**。

1. 將所有其他下拉式清單選項保留為預設選項。

1. 在`Date Range`下拉式清單中，選取與您在`Sun - Sat`中的`Mon - Sun`設定相符的任何選項(`Start of Week`、[!DNL Commerce Intelligence])。

1. 清除`Compare Year-Over-Year Data`核取方塊。

1. 在`Data Type`下，選取`Transaction Date`。

   ![匯入\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 按一下&#x200B;**[!UICONTROL View Report]**。

1. 按一下&#x200B;**[!UICONTROL Download]**。

   此時，已下載一個`.csv`檔案。

下載檔案後，您可以使用[!DNL Commerce Intelligence]功能[`File Upload`將其上傳至](../connecting-data/using-file-uploader.md)。
