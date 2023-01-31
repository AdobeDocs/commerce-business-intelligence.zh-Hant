---
title: 配置複製方法
description: 了解表的組織方式以及表資料的行為方式允許您為表選擇最佳複製方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# 配置複製方法

`Replication` 方法與 [重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md) 用於標識資料庫表中的新資料或更新的資料。 正確設定這些參數對於確保資料正確性和最佳化更新時間至關重要。 在本文中，我們將只關注複製方法。

在Data Warehouse管理器中同步新表時，將自動為表選擇複製方法。 了解各種複製方法、表的組織方式以及表資料的行為方式，將使您能夠為表選擇最佳的複製方法。

## 有哪些復寫方法？

`Replication` 方法分為三組 —  `Incremental`, `Full Table`，和 `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) 意味著 [!DNL MBI] 只會在每次復寫嘗試時復寫新資料或更新資料。 由於這些方法可大幅減少延遲，因此強烈建議您盡可能使用。

[**[!UICONTROL Full Table Replication]**](#fulltable) 意味著 [!DNL MBI] 將在每次複製嘗試時複製表的整個內容。 由於要複製的資料量可能很大，這些方法可能會增加延遲和更新時間。 如果表包含任何時間戳記或日期時間列，建議改用增量方法。

**[!UICONTROL Paused]** 指示表的複製已停止或已暫停。 [!DNL MBI] 在更新週期期間，不會檢查新資料或更新資料；這表示將不會從具有此複製方法的表中複製任何資料。

## 增量複製方法 {#incremental}

### 修改時間（最理想）

此 `Modified At` 複製方法使用datetime列（建立行時填入該列，然後在資料更改時更新）查找要複製的資料。 此方法的設計目的是搭配符合下列准則的表格使用：

* 包含a `datetime` 在建立行時首次填入的列，在修改行時更新；
* the `datetime` 欄從不為null;
* 不會從表格中刪除列

除了這些條件外，我們也強烈建議 **索引** the `datetime` 用於 `Modified At` 復寫，因為這將幫助優化複製速度。

執行更新時，會搜尋在 `datetime` 最近更新後發生的欄。 發現新行後，這些行將複製到您的Data Warehouse。 如果Data Warehouse中已存在任何行，則它們將被當前資料庫值覆蓋。

例如，表格可能有一列稱為 `modified\_at` 表示上次變更資料的時間。 如果最新更新是星期二中午執行，則更新會搜尋所有具有 `modified\_at` 值大於星期二中午。 從星期二中午開始建立或修改的任何探索到的列都將複製到Data Warehouse。

**你知道嗎？**
即使您的資料庫當前無法支援 `Incremental` 複製方法，您可以 [對資料庫進行一些更改](../../best-practices/mod-db-inc-replication.md) 使用 `Modified At` 或 `Single Auto Incrementing PK`.

`Modified At` 不僅是最理想的複製方法，而且速度最快。 此方法不僅會在大型資料集時產生明顯的速度增加，也不需要設定重新檢查選項。 其他方法將需要逐一查看整個表格，以識別變更，即使一小部分資料已變更。 `Modified At` 只會反覆處理這個小子集。

### 單自動增加主鍵

`Auto Incrementing` 是循序將主鍵指派給列的行為。 如果表是 `Auto Incrementing` 而表中最高主鍵當前為1000，則下一個主鍵值將為1001或更高。 不使用的表格 `Auto Incrementing` 行為可能會指派小於1000的主鍵值，或跳到大得多的數字，但這不常使用。

此方法旨在從符合下列准則的表格中複製新資料：

* `single-column primary key`;和
* `primary key` 資料類型 `integer`;和
* `auto incrementing` 主鍵值。

表使用時 `Single Auto Incrementing Primary Key` 復寫時，系統會搜尋主索引鍵值，以探索到高於Data Warehouse中目前最高值的新資料。 例如，如果Data Warehouse中最高主鍵值為500，則下次運行更新時，它將搜索主鍵值為501或更高的行。

### 新增日期

此 `Add Date` 方法函式與 `Single Auto Incrementing Primary Key` 方法。 此方法將使用 `timestamped` 欄來檢查新列。

表使用 `Add Date` 復寫時，會搜尋大於同步至您Data Warehouse之最新日期的時間戳記值，以探索新資料。 例如，如果上次更新是在20/12/2015 09執行:00:00，時間戳記大於此值的任何列都會標示為新資料並複製。

>[!NOTE]
>
>不同於 `Modified At` 方法， `Add Date` 不會檢查現有列以取得更新的資訊，只會看到新列。

## 完整表複製方法 {#fulltable}

### 完整表格

`Full table` 每當檢測到新行時，複製都會刷新整個表。 這是迄今為止最低效的複製方法，因為假設有新列，每次更新期間都必須重新處理所有資料。

在同步進程開始時查詢資料庫並計算行數，可檢測新行。 如果本地資料庫包含的行數超過 [!DNL MBI]，則會重新整理表格。 如果列計數相同，或 [!DNL MBI] 包含 *更多* 行，則跳過表。

這引出了一個重要問題 **`Full Table`復寫時不相容：**

* 在後續更新週期之間，刪除的行數比在本地資料庫表中建立的行數多，或者
* 欄值已變更，但未建立其他列

在上述任一種情況下， `Full Table` 復寫不會偵測到任何變更，且您的資料會過時。 由於此複製方法效率低下，以及上述要求， `Full Table` 僅建議將復製作為最後手段。

### 主鍵批

表使用 `Primary Key Batch` （PK批），通過計算主鍵值範圍或批內的行來發現新資料。 雖然我們通常認為這會與整數搭配使用，但即使是文字值，也能以可讓系統定義常數範圍的方式排序。

例如，假設更新執行，並執行從1到100的鍵值範圍的列計數。 在此更新中，系統會尋找並記錄37列。 在下次更新中，會在1-100範圍內再次執行列計數，並找出41列。 由於列數與上次更新有所差異，因此系統將更詳細地檢查該範圍（或批）。

此方法旨在從符合以下條件的表中複製資料：

* 單列非整數；或
* 複合鍵（包括主鍵的多列） — 請注意，複合主鍵中使用的列永遠不能具有空值；或
* 單欄、整數、非自動遞增主鍵值。

此方法並不理想，因為由於檢查批次和查找更改時必須執行的處理量，處理速度非常慢。 除非無法進行支援其他復寫方法所需的修改，否則不建議使用此方法。 如果必須使用此方法，則更新時間會增加。

## 設定復寫方法

復寫方法是逐表設定。 要為表設定複製方法，您需要 [`Admin`](../../administrator/user-management/user-management.md) 權限，以便您存取Data Warehouse管理員。

1. 進入「Data Warehouse管理器」後，從 `Synced Tables` 清單，以顯示表格的架構。
1. 當前複製方法列在表名下。 若要變更，請按一下連結。
1. 在顯示的快顯視窗中，按一下任一選項旁的選項按鈕 `Incremental` 或 `Full Table` 復寫以選取復寫類型。
1. 下一步，按一下 **[!UICONTROL Replication Method]** 下拉式清單來選取方法，例如 `Paused` 或 `Modified At`.

   >[!NOTE]
   >
   >**某些增量方法要求您設定`Replication Key`**. [!DNL MBI] 將使用此金鑰來決定下一個更新週期的開始位置。
   >
   >例如，如果我們想使用 `modified at` 方法 `orders` 表格，我們要設定 `date column` 作為復寫金鑰。 復寫金鑰的數個選項可能存在，但我們會選取 `created at`，或建立訂單的時間。 如果上次更新週期停止於12/1/2015 00:10:00，下一個週期將開始使用 `created at` 日期大於此。

1. 完成後，按一下 **[!UICONTROL Save]**.

請檢視整個程式：

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 包裝

最後，我們將此表放在一起，比較各種複製方法。 我們發現，在資料倉庫中為表格選取方法時，它非常方便。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 更快 | 慢速 | 否 | 否 | 否 | 是 |
| `Primary Key Batch Monitoring` | 慢速 | 慢速 | 是 | 是 | 是 | 是 |
| `Modified At` | 更快 | 更快 | 是 | 是 | 是 | 否 |

{style=&quot;table-layout:auto&quot;}

## 相關檔案

* [了解資料重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)
* [修改資料庫以支援 ](../../best-practices/mod-db-inc-replication.md)
* [優化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
