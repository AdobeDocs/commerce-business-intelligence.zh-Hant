---
title: Data Warehouse管理員
description: 瞭解如何管理表格和欄同步設定、深入研究表格的綱要，以及建立要在報告中使用的計算欄。
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Data Warehouse管理員

>[!NOTE]
>
>需要[管理員許可權](../../administrator/user-management/user-management.md)

按一下&#x200B;**[!UICONTROL Manage Data > Data Warehouse]**&#x200B;存取的Data Warehouse管理員是您[!DNL Adobe Commerce Intelligence]Data Warehouse的入口網站。 使用「Data Warehouse管理員」，您可以管理表格和欄同步設定、深入研究表格的綱要，並建立計算欄以用於報表。

本主題涵蓋：

* [瞭解如何因應各種因素](#learning)
* [同步表格和欄](#syncing)
* [建立計算欄](#calculated)
* [正在卸除資料表及移除資料行](#delete)
* [在背景同步新表格](#syncnew)
* [那麼，我何時可以使用新的欄？](#when)

## 瞭解如何因應各種因素 {#learning}

`Data Warehouse Manager`頁面的左側包含表格清單，讓您在表格之間輕鬆切換。 當您從清單中選取表格時，表格管理區域會填入表格的綱要，您可以在其中修改選取的表格。

在表格清單中，表格會依其連線來源分組。 這些來源新增至[!UICONTROL Manage Data > Integrations]之下，可能是資料庫、[API](https://developer.adobe.com/commerce/services/reporting/)或協力廠商聯結器。 在表格清單頂端有一個搜尋方塊，可讓您輕鬆尋找所需的表格。

在搜尋方塊底下，您會看到兩個選項： `All Tables`和`Synced Tables`。 `All Tables`選項會列出您Data Warehouse可用的所有表格，包括同步和未同步的表格。

`Synced Tables`選項會顯示所有已新增至Data Warehouse的資料表，以及從選取的資料行復寫資料。

沒有在`All Tables`清單中看到您在尋找的資料表？ 這種情況有幾個可能的原因：

* 資料來源尚未新增
* 資料來源是資料庫，而您建立的[!DNL Commerce Intelligence]使用者沒有存取權。 在這種情況下，您或您的資料庫管理員必須授予存取權。
* 資料來源或資料表最近已新增，但尚未同步

## 同步表格和欄 {#syncing}

### 同步新資料表與原生資料行

Data Warehouse管理員不僅可讓您輕鬆檢視和管理資料來源，也可讓您自由選取要同步的個別表格和欄。

1. 按一下`All Tables`選項，然後找到您要同步處理的資料表。
1. 按一下表格名稱以預覽架構。 如果表格是新的，則所有欄會顯示為`Unsynced`。
1. 核取您要同步的欄。

   >[!NOTE]
   >
   >資料表的原生資料行在`Location`資料行中有「來自您的資料庫」。

1. 請務必檢查`Primary Key`欄 — 這些欄的欄名稱旁會有索引鍵符號。 需要`Primary Key`才能將資料正確同步到Data Warehouse中。

   如果您正在同步直接從資料庫取得的資料表，則可能無法表示`Primary Keys`。 在此情況下，請連絡您的資料庫管理員，要求將一或多個主索引鍵新增至表格。
1. 完成後，按一下![按鈕](../../assets/button.png)按鈕。

*成功！顯示*&#x200B;訊息，且所選欄的狀態變更為`Pending`。 下次完整更新完成後，新同步的表格和欄將可用於報告中。 您也可以在初始同步之後設定新的[復寫方法](./cfg-replication-methods.md)。

以下快速瞭解整個程式：

![正在將資料行新增至資料倉儲](../../assets/DW_sync.gif)

### 在背景同步新表格 {#syncnew}

第一次同步處理大型表格時，Data Warehouse必須先回溯擷取表格中的所有資料點，才能持續擷取新資料。 如果您的資料表很大，您可能不想讓初始同步處理依序執行您的&#x200B;**更新週期**。 在此情況下，您希望初始同步會在背景中進行，以&#x200B;*平行*&#x200B;與任何目前執行中的更新。

若要確定發生此情況，您應該選取第一次同步處理該資料表的`Save and Sync Data Immediately`選項。

### 檢查新表格和欄 {#forceupdate}

在新增來源、表格或欄時，您的Data Warehouse不會自動偵測這些來源、表格或欄。 同步化程式會在一週中執行以尋找新的加入並使其可用，但如果您要在程式執行之前存取新加入的表格和欄，則可以強制進行結構同步化。

表格清單中搜尋列下方是`Check for new tables and columns`連結。 按一下此連結會強制啟動結構同步程式；新專案通常在10分鐘後提供。 重新整理頁面以檢視新的來源、表格或欄。

## 建立計算欄 {#calculated}

只要能夠檢視和管理您所有來源的資料，就能更輕鬆獲得對業務的深入分析。 但在「Data Warehouse管理員」中，您可以在表格內建立計算欄以更進一步。 `Calculated`欄從您現有的資料衍生出新資訊。

假設您想要將`user's lifetime revenue`新增至您的`users`資料表以尋找高價值使用者。 或者，如果您想要依性別劃分收入，可以新增`customer's gender`至您的`orders`表格。

如需詳細資訊，請參閱此[教學課程](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)。

## 刪除表格與移除欄 {#delete}

就像您可以選取要同步至Data Warehouse的表格和欄一樣，您也可以拖放或移除它們。

>[!NOTE]
>
>刪除表格或移除欄會在您確認刪除後，刪除任何相依的報告、量度、篩選器集和欄。 確定您要執行此動作 — **此動作無法復原。**

如果您不小心按一下&#x200B;**[!UICONTROL Delete]**，請不要擔心。 相依性檢查會在任何專案刪除前執行，因此您有機會在確認前檢閱所有專案。

若要移除欄，請按一下該欄所屬的表格。 核取您要移除的資料行，然後按一下![button\_1.png](../../assets/button_1.png)按鈕。

若要移除同步處理的表格，請選取表格中的所有欄，然後再次按一下![按鈕](../../assets/button_1.png)按鈕。 這會從您的Data Warehouse中移除使用此表格的所有原生和計算欄。

### 確認變更

無論您是要卸除資料表還是移除資料行，刪除程式完成之前都會執行相依性檢查。 相依性是指使用要移除之表格或欄的計算欄、量度、篩選器集和報表。 任何發現的相依性都會顯示 — 此時，您可以取消程式或按一下&#x200B;**[!UICONTROL Confirm Changes]**&#x200B;以卸除表格/移除欄。

雖然已刪除的相依性無法復原，但如果您日後需要重新同步任何原生欄，表格和欄仍可使用。

以下為移除欄的快速檢視：

![正在從您的資料倉儲移除資料行](../../assets/DW_delete.gif)

## 那麼，我何時可以使用新的欄？ {#when}

新的同步欄和新的/更新的計算欄將在下次完整更新完成後準備使用。 如果更新尚未進行，您可以按一下`Data Warehouse`或`Integrations`頁面頂端顯示的&#x200B;**[!UICONTROL Force update]**&#x200B;來強制更新。 您也可以按一下&#x200B;**[!UICONTROL Email me when complete]**，在更新完成時排程電子郵件通知。

當您準備在報告中使用新欄時，[您必須先將它們新增到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。 雖然在更新完成之前無法取得資料，您仍可在報表中使用新欄。 更新完成後，會顯示報表中的資料。

## 正在結束

本文涵蓋許多內容。 到現在為止，您應該已經相當瞭解什麼是資料庫、資料如何組織、表格如何相互關聯，以及您可以使用「Data Warehouse管理員」做什麼。

透過[建立計算資料行](../data-warehouse-mgr/creating-calculated-columns.md)或[製作一些有趣的報告](../../tutorials/using-visual-report-builder.md)來測試您的知識。
