---
title: 建立Google Analytics圖表
description: 瞭解如何從Google Analytics資料建立圖表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 建立 [!DNL Google Analytics] 圖表

（使用規則運算式語法說明）

在您連線至 [[!DNL Google Analytics] 帳戶](../../data-analyst/importing-data/integrations/google-analytics.md)，您可以使用您的 [!DNL Google Analytics] 資料。

## 建立 [!DNL Google Analytics] 圖表

1. 按一下 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 在中選取量度時 `Chart Builder`，捲動至清單底部以尋找包含 [!DNL Google Analytics] 設定檔。 第二個量度下拉式清單隨即顯示。 您可以在此處選擇要分析的量度。

1. 選擇量度後，您可以選取「 」，將此圖表當成任何其他圖表來處理 `time period`， `interval`、和資料 `perspectives` 您希望看到的專案。

1. 這裡的主要差異在於 `√` 使用規則運算式進行篩選。 規則運算式（簡稱regex）是用於描述搜尋模式的特殊文字字串。 請參閱中的規則運算式語法範例 [[!DNL Google] Analytics規則運算式指南](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>唯一需要使用\字元逸出的特殊字元為下列中繼字元：

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
