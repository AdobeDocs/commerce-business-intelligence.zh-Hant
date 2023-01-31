---
title: 建立Google Analytics圖
description: 了解如何從Google Analytics資料建立圖表。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 建立 [!DNL Google Analytics] 圖表

（透過regex語法說明）

在您連接了 [[!DNL Google Analytics] 帳戶](../../data-analyst/importing-data/integrations/google-analytics.md)，您可以從 [!DNL Google Analytics] 資料。

## 建立 [!DNL Google Analytics] 圖表

1. 按一下 **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 在 `Chart Builder`，捲動至清單底部以尋找包含 [!DNL Google Analytics] 設定檔。 第二個量度下拉式清單隨即出現。 您可以在此選取要分析的量度。

1. 選取量度後，您可以選取 `time period`, `interval`，和資料 `perspectives` 你想看的。

1. 其中一個主要區別是 `√` 對篩選器使用規則運算式。 規則運算式（簡稱為「規則運算式」）是描述搜尋模式的特殊文字字串。 請參閱 [[!DNL Google] Analytics規則運算式指南](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>只有下列超字元才需使用\字元來逸出：

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
