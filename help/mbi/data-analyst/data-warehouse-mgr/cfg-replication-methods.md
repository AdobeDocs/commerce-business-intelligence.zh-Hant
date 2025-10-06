---
title: 設定復寫方法
description: 瞭解表格的組織方式，以及表格資料的行為方式，讓您為表格選擇最佳的複製方法。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1442'
ht-degree: 0%

---

# 設定復寫方法

使用`Replication`方法和[重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)來識別資料庫表格中的新資料或更新資料。 正確設定這些變數對於確保資料正確性和最佳化更新時間至關重要。 本主題著重於復寫方法。

在[Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)中同步新資料表時，會自動為該資料表選擇復寫方法。 瞭解各種複製方法、表格的組織方式，以及表格資料的行為方式，讓您為表格選擇最佳的複製方法。

## 什麼是復寫方法？

`Replication`方法分為三個群組 — `Incremental`、`Full Table`和`Paused`。

[**[!UICONTROL Incremental Replication]**](#incremental)表示[!DNL Commerce Intelligence]只會在每次復寫嘗試時復寫新資料或更新資料。 由於這些方法可大幅減少延遲，Adobe建議儘可能使用。

[**[!UICONTROL Full Table Replication]**](#fulltable)表示[!DNL Commerce Intelligence]會在每次復寫嘗試時復寫表格的全部內容。 由於要複製的資料量可能很大，這些方法可能會增加延遲和更新時間。 如果表格包含任何時間戳記或日期時間欄，Adobe建議改用增量方法。

**[!UICONTROL Paused]**&#x200B;表示資料表的復寫已停止或暫停。 [!DNL Commerce Intelligence]不會在更新週期期間檢查是否有新的或更新資料；這表示不會從以此為復寫方法的資料表中復寫任何資料。

## 增量複製方法 {#incremental}

### 修改時間（最理想）

`Modified At`復寫方法使用datetime欄（在建立資料列時填入，然後在資料變更時更新）來尋找要復寫的資料。 此方法的設計目的是處理符合下列條件的表格：

* 包含`datetime`欄，此欄最初是在建立資料列時填入，並會在資料列修改時更新；
* `datetime`資料行絕不為Null；
* 不會從表格中刪除列

除了這些條件外，Adobe還建議為用於&#x200B;**復寫的**&#x200B;資料行`datetime`編制索引`Modified At`，因為這有助於最佳化復寫速度。

當更新執行時，透過搜尋在最近更新之後發生的`datetime`欄中有值的列，可識別新資料或已變更的資料。 探索到新列時，會將它們復寫到您的Data Warehouse。 如果[Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)中有任何資料列存在，則會以目前的資料庫值覆寫。

例如，資料表可能有一個名為`modified\_at`的資料行，指出上次變更資料的時間。 如果最新的更新在星期二中午執行，則更新會搜尋所有具有大於星期二中午的`modified\_at`值的列。 自星期二中午以來建立或修改的任何發現列都會複製到Data Warehouse。

**您知道嗎？**
即使您的資料庫目前無法支援`Incremental`復寫方法，您也可以[對資料庫進行變更](../../best-practices/mod-db-inc-replication.md)，以啟用`Modified At`或`Single Auto Incrementing PK`的使用。

`Modified At`不僅是最理想的復寫方法，也是最快的復寫方法。 此方法不僅會在大型資料集中產生顯著的速度，而且不需要設定重新檢查選項。 其他方法需要逐一檢視整個表格以識別變更，即使一小部分資料已變更。 `Modified At`只會反複處理這個小子集。

### 單一自動遞增主索引鍵

`Auto Incrementing`是循序將主索引鍵指派給資料列的行為。 如果資料表為`Auto Incrementing`，而資料表中最高主索引鍵為1,000，則下一個主值是1,001或更高。 不使用`Auto Incrementing`行為的資料表可指派小於1,000的主索引鍵值或跳至大得多的數字，但並不常用。

此方法旨在從符合下列條件的表格中複製新資料：

* `single-column primary key`；和
* `primary key`資料型別是`integer`；以及
* `auto incrementing`個主索引鍵值。

當資料表使用`Single Auto Incrementing Primary Key`復寫時，搜尋大於Data Warehouse中目前最高值的主索引鍵值，即可探索新資料。 例如，如果Data Warehouse中的最高主鍵值為500，則下次更新執行時，將會搜尋主鍵值為501或更高的列。

### 新增日期

`Add Date`方法的功能與`Single Auto Incrementing Primary Key`方法類似。 這個方法不是使用整數以取得資料表的主索引鍵，而是使用`timestamped`資料行來檢查新資料列。

當資料表使用`Add Date`復寫時，透過搜尋晚於同步至您Data Warehouse的最新日期的時間戳記值來探索新資料。 例如，如果更新上次執行時間為20/12/2015 09:00:00，則時間戳記大於此的任何列都將標示為新資料並複製。

>[!NOTE]
>
>與`Modified At`方法不同，`Add Date`不會檢查現有資料列是否有更新的資訊，而只會尋找新的資料列。

## 完整表格複製方法 {#fulltable}

### 完整表格

在偵測到新資料列時，`Full table`復寫會重新整理整個資料表。 這是目前為止最不有效率的複製方法，因為所有資料在每次更新期間都必須重新處理（假設有新列）。

在同步化程式開始時查詢資料庫並計算資料列數目，即可偵測新資料列。 如果您的本機資料庫包含超過[!DNL Commerce Intelligence]的資料列，則會重新整理資料表。 如果資料列計數相同，或[!DNL Commerce Intelligence]包含比本機資料庫多&#x200B;*個*&#x200B;資料列，則會略過資料表。

這引出&#x200B;**`Full Table`復寫在**&#x200B;時不相相容的重要點

* 在後續更新週期之間，刪除的資料列多於在本機資料庫表格中建立的資料列，或者
* 欄值已變更，但未建立其他列

在上述任一情況中，`Full Table`復寫不會偵測到任何變更，且您的資料會過時。 由於此復寫方法效率不高，加上上述需求，最後才建議使用`Full Table`復寫。

### 主索引鍵批次

當資料表使用`Primary Key Batch` （PK批次）時，透過計算主索引鍵值範圍或批次中的資料列來探索新資料。 雖然您通常認為這會與整數搭配使用，但即使是文字值，排序方式也可以讓系統定義常數範圍。

例如，假設更新執行並執行索引鍵1至100範圍的列計數。 在此更新中，系統會尋找並記錄37列。 在下次更新中，會在1-100範圍上再次執行列計數，並找到41列。 由於與上次更新相比列數不同，因此系統會更詳細地檢查該範圍（或批次）。

此方法旨在從符合下列條件的表格複製資料：

* 單欄非整數；或
* 複合索引鍵（包含主索引鍵的多個欄） — 請注意，複合主索引鍵中使用的欄永遠不能有null值；或
* 單欄、整數、不自動增加主索引鍵值。

此方法並不理想，因為為了檢查批次和尋找變更而必須執行的處理量太大，所以速度非常慢。 Adobe建議您不要使用此方法，除非無法進行必要的修改以支援其他複製方法。 如果必須使用這個方法，預期更新時間會增加。

## 設定復寫方法

複製方法是以表格為基礎設定的。 若要設定資料表的復寫方法，您需要[`Admin`](../../administrator/user-management/user-management.md)許可權，才能存取Data Warehouse Manager。

1. 進入Data Warehouse Manager後，從`Synced Tables`清單中選取表格以顯示表格的結構描述。
1. 目前的複製方法列在表格名稱下方。 若要變更，請按一下連結。
1. 在顯示的快顯視窗中，按一下`Incremental`或`Full Table`復寫旁的選項按鈕以選取復寫型別。
1. 接著，按一下&#x200B;**[!UICONTROL Replication Method]**&#x200B;下拉式清單以選取方法。 例如，`Paused`或`Modified At`。

   >[!NOTE]
   >
   >**有些增量方法需要您設定`Replication Key`**。 [!DNL Commerce Intelligence]將使用此索引鍵來決定下一個更新週期應該從何處開始。
   >
   >例如，如果您想要對`modified at`資料表使用`orders`方法，您必須將`date column`設定為復寫金鑰。 復寫金鑰可能有數個選項，但您選取`created at`或建立訂單的時間。 如果上次更新週期在12/1/2015 00:10:00停止，則下一個週期會開始複製日期大於此日期的`created at`資料。

1. 完成時，按一下&#x200B;**[!UICONTROL Save]**。

檢視整個程式：

![設定資料庫資料表復寫方法的動畫示範](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## 正在結束

為了完成，您已經將這個表格放在一起，比較各種複製方法。 為Data Warehouse中的表格選取方法非常方便。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 更快 | 慢速 | 否 | 否 | 否 | 是 |
| `Primary Key Batch Monitoring` | 慢速 | 慢速 | 是 | 是 | 是 | 是 |
| `Modified At` | 更快 | 更快 | 是 | 是 | 是 | 否 |

{style="table-layout:auto"}

## 相關檔案

* [瞭解資料重新檢查](../data-warehouse-mgr/cfg-data-rechecks.md)
* [修改資料庫以支援 &#x200B;](../../best-practices/mod-db-inc-replication.md)
* [最佳化資料庫以進行分析](../../best-practices/opt-db-analysis.md)
* [縮短更新時間](../../best-practices/reduce-update-cycle-time.md)
