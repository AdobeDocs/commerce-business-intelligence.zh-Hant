---
title: 匯入Bing廣告支出資料
description: 瞭解如何將Bing廣告支出資料匯入[!DNL Commerce Intelligence]進行分析。
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%
---
# 匯入[!DNL Bing]資料

若要將[!DNL Bing]廣告支出資料匯入[!DNL Adobe Commerce Intelligence]進行分析，只要以`.csv`格式從[!DNL Bing Ads Editor]匯出資料，然後依照下列步驟將其上傳到[!DNL Commerce Intelligence]即可。

## [!DNL Bing Ads Editor]

若要匯出您的[!DNL Bing Ads]資料，您必須安裝[!DNL Bing Ads Editor]。 您可以找到[[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor)的免費下載。

## [!DNL Bing Ads]資料匯出

1. 在[!DNL Bing Ads Editor]的`Browser`窗格中，用滑鼠右鍵按一下您要匯出的行銷活動或廣告群組，然後按一下&#x200B;**[!UICONTROL Export]**。
1. 在`Export`對話方塊中，按一下&#x200B;**[!UICONTROL Export]**。
1. 在`Save As`對話方塊中，按一下您想要儲存匯出檔案的資料夾。
1. 在`File name`方塊中，選擇檔案匯出的名稱。
1. 按一下&#x200B;**[!UICONTROL Save]**。
1. 下載檔案後，[請連絡支援人員](https://experienceleague.adobe.com/zh-hant/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)代表您執行第一次上傳，並設定必要的後端維度。
