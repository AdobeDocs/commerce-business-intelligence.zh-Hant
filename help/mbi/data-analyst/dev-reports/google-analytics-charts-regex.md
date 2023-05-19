---
title: 建立Google Analytics圖表
description: 瞭解如何從您的Google Analytics資料建立圖表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 建立 [!DNL Google Analytics] 圖表

（使用regex語法幫助）

連接後 [[!DNL Google Analytics] 帳戶](../../data-analyst/importing-data/integrations/google-analytics.md)，可以使用 [!DNL Google Analytics] 資料。

## 建立 [!DNL Google Analytics] 圖表

1. 按一下 **[!UICONTROL Add Chart** > **Create New Chart]**。

1. 在 `Chart Builder`，滾動到清單底部以查找包括 [!DNL Google Analytics] 配置檔案。 出現第二個度量下拉清單。 您可以在此處選擇要分析的度量。

1. 選擇度量後，可以繼續使用此圖表，如同它是任何其他圖表一樣，方法是選擇 `time period`。 `interval`，以及資料 `perspectives` 你想看的。

1. 這裡的一個主要區別是 `√` 對篩選器使用規則運算式。 規則運算式（regex表示短）是用於描述搜索模式的特殊文本字串。 請參見中的regex語法示例 [[!DNL Google] 分析規則運算式指南](https://support.google.com/analytics/answer/1034324?hl=en)。

>[!NOTE]
>
>使用\字元轉義的唯一特殊字元是以下元字元：

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
