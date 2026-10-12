---
title: 建立Google Analytics圖表
description: 瞭解如何從Google Analytics資料建立圖表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: 'https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o'
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
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
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
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%
---
# 建立[!DNL Google Analytics]個圖表

（使用規則運算式語法說明）

連線[[!DNL Google Analytics] 帳戶](../../data-analyst/importing-data/integrations/google-analytics.md)之後，您就可以使用[!DNL Google Analytics]資料建立圖表。

## 建立[!DNL Google Analytics]個圖表

1. 按一下&#x200B;**[!UICONTROL Add Chart** > **Create New Chart]**。

1. 在`Chart Builder`中選取量度時，捲動至清單底部以尋找包含您的[!DNL Google Analytics]設定檔的區段。 第二個量度下拉式清單隨即顯示。 您可以在此處選擇要分析的量度。

1. 選擇量度後，您可以選取想要檢視的`time period`、`interval`和資料`perspectives`，繼續使用此圖表，就像任何其他圖表一樣。

1. 這裡的主要差異在於`√`使用規則運算式進行篩選。 規則運算式（簡稱regex）是用於描述搜尋模式的特殊文字字串。 請參閱Analytics規則運算式[&#128279;](https://support.google.com/analytics/answer/1034324?hl=en)的[!DNL Google] 指南中的規則運算式語法範例。

>[!NOTE]
>
>唯一需要使用\字元逸出的特殊字元為下列中繼字元：

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
