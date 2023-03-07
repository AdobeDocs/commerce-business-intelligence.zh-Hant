---
title: 使用映射表標準化資料
description: 了解如何使用對應表格。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 使用映射表標準化資料

想像一下：你在 `Report Builder`，建立 `Revenue by State` 報表。 你在區裡。 一切都順利，直到你 `billing state` 分組後，您會看到：

![](../../assets/Messy_State_Segments.png)

## 這怎麼可能？

不幸的是，缺乏標準化有時會導致資料混亂，並且在建立報表時帶來麻煩。 在此範例中，可能沒有下拉式功能表或標準化方式供客戶輸入其帳單狀態資訊。 這會產生各種值 —  `pa`, `PA`, `penna`, `pennsylvania`，和 `Pennsylvania`  — 全部為相同狀態，導致 `Report Builder`.

有技術資源可協助您清理資料，或直接將您需要的欄插入資料庫。 如果沒有，還有另一個解決方案 —  **映射表**. 對應表格可讓您將資料對應至單一輸出，以快速輕鬆地清除和標準化任何亂糟糟的資料。

>[!NOTE]
>
>如果沒有Adobe支援團隊的幫助，則無法為統一表建立映射表。

## 如何建立它？ {#how}

**資料格式重新整理：**

* 請確定試算表有標題列。
* 請避免使用逗號！ 上傳檔案時會造成問題。
* 使用標準日期格式 `(YYYY-MM-DD HH:MM:SS)` 日期。
* 百分比必須輸入為小數。
* 請確定所有前導或尾隨零皆正確保留。

在您深入之前，Adobe建議您 [匯出原始表格資料](../../tutorials/export-raw-data.md). 首先查看原始資料表示您可以探索所有可能的資料組合，以便清除所需資料，從而確保對應表格涵蓋所有內容。

若要建立對應表格，您需建立遵循的兩欄試算表 [檔案上載的格式規則](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

在第一欄中，輸入儲存在資料庫中的值 **每列只有一個值**. 例如， `pa` 和 `PA` 不能在同一行上 — 每個輸入都需要有自己的行。 如需範例，請參閱下方。

在第二欄中，輸入這些值 **應該是**. 如果您想要，請繼續使用計費狀態範例 `pa`, `PA`, `Pennsylvania`，和 `pennsylvania` 就是 `PA`，您可以輸入 `PA` 在此欄中輸入每個輸入值。

![](../../assets/Mapping_table_examples.jpg)

## 我要做什麼 [!DNL MBI] 用它？ {#use}

建立完對應表格後，您需要 [上傳檔案](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] 和 [建立聯接列](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 將新欄位重新定位至所需表格。 將檔案同步至Data Warehouse後，即可執行此動作。

此範例會移動您在 `mapping_state` 表格(`state_input`) `customer_address` 表格。 這可讓我們依清潔 `state_input` 欄，而非 `state` 欄。

若要建立 `joined` 欄，導覽至「Data Warehouse管理器」中欄位要重新定位到的表。 在此範例中，這會是 `customer_address` 表格。

1. 按一下 **[!UICONTROL Create a Column]**.
1. 選擇 `Joined Column` 從 `Definition` 下拉式清單。
1. 為欄指定可區分它與 `state` 欄。 為欄命名 `billing state (mapped)` 以便您在報告建立工具中劃分區段時知道要使用哪個欄。
1. 連接表所需的路徑不存在，因此需要建立一個路徑。 按一下 **[!UICONTROL Create new path]**  在 `Select a table and column` 下拉式清單。

   如果您不確定表關係是什麼或如何正確定義主鍵和外鍵，請簽出 [教學課程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 來幫忙。

   * 在 `Many` 側邊，選取您要將欄位重新定位至的表格(同樣地，對我們來說是 `customer_address`)和 `Foreign Key` 欄，或 `state` 欄，在範例中。
   * 在 `One` 側，選取 `mapping` 表格和 `Primary key` 欄。 在此情況下，您可以選取 `state_input` 欄 `mapping_state` 表格。
   * 路徑外觀如下：

      ![](../../assets/State_Mapping_Path.png)

1. 完成後，按一下 **[!UICONTROL Save]** 來建立路徑。
1. 儲存後，路徑可能不會立即填入 — 如果發生此情況，請按一下 `Path` 框中，然後選擇您建立的路徑。
1. 按一下 **[!UICONTROL Save]** 來建立欄。

就這樣！

## 我現在該做什麼？ {#wrapup}

更新週期完成後，您將能使用新的聯接列來正確劃分資料，而不是從資料庫中劃分混亂的列。 看看你的分組選項 — 不再有壓力混亂：

![](../../assets/Clean_State_Segments.png)

您隨時都可以使用對應表格來清理Data Warehouse中可能雜亂的資料。 不過，映射表也可用於其他一些酷炫使用案例，例如 [在MBI中複製Google Analytics通道](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 相關

* [了解和評估表關係](../data-warehouse-mgr/table-relationships.md)
* [建立/刪除計算列的路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
