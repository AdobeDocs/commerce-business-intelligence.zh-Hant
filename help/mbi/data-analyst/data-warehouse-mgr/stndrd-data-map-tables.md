---
title: 使用映射表標準化資料
description: 瞭解如何使用映射表。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# 使用映射表標準化資料

想像你在 `Report Builder` 建造 `Revenue by State` 報告。 一切順利，直到你嘗試添加 `billing state` 將其分組到報表中，您會看到：

![](../../assets/Messy_State_Segments.png)

## 這怎麼可能？

不幸的是，缺乏標準化有時會導致資料混亂，並在構建報告時造成麻煩。 在此示例中，可能沒有下拉菜單或標準化方法讓客戶輸入其開單狀態資訊。 這會帶來各種價值。 `pa`。 `PA`。 `penna`。 `pennsylvania`, `Pennsylvania`  — 全部為同一狀態，導致在 `Report Builder`。

可能有一種技術資源可幫助您清除資料或直接將所需列插入資料庫。 否則，還有另一個解決方案。 **映射表**。 映射表允許您通過將資料映射到單個輸出來快速而輕鬆地清除和標準化任何混亂的資料。

>[!NOTE]
>
>如果沒有Adobe支援團隊的幫助，則無法為統一表建立映射表。

## 如何建立它？ {#how}

**資料格式刷新程式：**

* 確保電子錶格有標題行。
* 避免使用逗號！ 上載檔案時會出現問題。
* 使用標準日期格式 `(YYYY-MM-DD HH:MM:SS)` 日期。
* 百分比必須以小數輸入。
* 確保正確保留任何前導零或尾隨零。

在你潛入之前，Adobe建議你 [導出原始表資料](../../tutorials/export-raw-data.md)。 首先查看原始資料意味著您可以探索需要清理的資料的所有可能組合，從而確保映射表涵蓋所有內容。

要建立映射表，需要建立位於 [檔案上載的格式規則](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)。

在第一列中，輸入儲存在資料庫中的值 **每行只有一個值**。 比如說， `pa` 和 `PA` 不能位於同一行上 — 每個輸入都需要有自己的行。 有關示例，請參見下面。

在第二列中，輸入這些值 **應該**。 如果需要，請繼續使用開單狀態示例 `pa`。 `PA`。 `Pennsylvania`, `pennsylvania` 只是 `PA`，則 `PA` 的下界。

![](../../assets/Mapping_table_examples.jpg)

## 我需要在 [!DNL Commerce Intelligence] 用它？ {#use}

建立完映射表後，必須 [上載檔案](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 入 [!DNL Commerce Intelligence] 和 [建立聯接列](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 將新欄位重新定位到所需表中。 可以在檔案同步到您的Data Warehouse後執行此操作。

此示例移動您在 `mapping_state` 表格`state_input`) `customer_address` 表。 這允許我們按清潔 `state_input` 列 `state` 的雙曲餘切值。

建立 `joined` 列，導航到在Data Warehouse管理器中將欄位重新定位到的表。 在本例中，這是 `customer_address` 的子菜單。

1. 按一下 **[!UICONTROL Create a Column]**。
1. 選擇 `Joined Column` 從 `Definition` 下拉清單。
1. 為列指定一個名稱，將其與 `state` 的子菜單。 命名列 `billing state (mapped)` 這樣，在報表生成器中分段時，您就可以知道要使用哪一列。
1. 連接表所需的路徑不存在，因此需要建立一個路徑。 按一下 **[!UICONTROL Create new path]**  的 `Select a table and column` 下拉清單。

   如果您不確定表關係是什麼或如何正確定義主鍵和外鍵，請簽出 [本教程](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 來幫忙。

   * 在 `Many` 側，選擇要將欄位重新定位到的表(同樣，對於我們來說， `customer_address`)和 `Foreign Key` 列或 `state` 中。
   * 在 `One` 側，選擇 `mapping` 和 `Primary key` 的雙曲餘切值。 在這種情況下，您將選擇 `state_input` 列 `mapping_state` 的子菜單。
   * 下面是路徑的外觀：

      ![](../../assets/State_Mapping_Path.png)

1. 完成後，按一下 **[!UICONTROL Save]** 的子菜單。
1. 保存後，路徑可能不會立即填充 — 如果出現這種情況，請按一下 `Path` 框中，選擇所建立的路徑。
1. 按一下 **[!UICONTROL Save]** 的子菜單。

## 我現在該怎麼辦？ {#wrapup}

更新週期完成後，您將能夠使用新聯接的列正確地對資料進行分段，而不是從資料庫中對混亂的列進行分段。 現在看看你的分組選項 — 不再有壓力混亂：

![](../../assets/Clean_State_Segments.png)

映射表在您希望清除Data Warehouse中某些可能混亂的資料時非常方便。 但是，映射表也可用於其他一些酷用例，如 [複製 [!DNL Google Analytics channels] 在 [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md)。

### 相關

* [瞭解和評估表關係](../data-warehouse-mgr/table-relationships.md)
* [建立/刪除計算列的路徑](../data-warehouse-mgr/create-paths-calc-columns.md)
