---
title: Data Warehouse管理器
description: 瞭解如何管理表和列同步設定、深入到表的架構並建立要在報告中使用的計算列。
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
source-git-commit: c4094e780f83255846520d18f4d0806b1dd9a9ef
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Data Warehouse管理器

>[!NOTE]
>
>需要 [管理權限](../../administrator/user-management/user-management.md)

Data Warehouse管理器，通過按一下 **[!UICONTROL Manage Data > Data Warehouse]**，是您的門戶 [!DNL Adobe Commerce Intelligence] Data Warehouse。 使用Data Warehouse管理器，可以管理表和列同步設定，深入到表的架構中，並建立要在報告中使用的計算列。

本主題包括：

* [學習如何](#learning)
* [同步表和列](#syncing)
* [建立計算列](#calculated)
* [刪除表並刪除列](#delete)
* [正在後台同步新表](#syncnew)
* [那麼，我什麼時候才能使用新欄目？](#when)

## 學習如何 {#learning}

左側 `Data Warehouse Manager` 的子菜單。 從清單中選擇表時，表管理區域將使用表的模式填充，在該模式中可以修改選定的表。

在表清單中，表按其連接源分組。 這些源在 [!UICONTROL Manage Data > Integrations] 可能是資料庫， [API](https://developer.adobe.com/commerce/services/reporting/)或第三方連接器。 在表清單的頂部，有一個搜索框，使您能夠輕鬆查找所需的表。

在搜索框下，您會看到兩個選項： `All Tables` 和 `Synced Tables`。 的 `All Tables` 選項列出您已為Data Warehouse提供的所有表，其中包括已同步和未同步的表。

的 `Synced Tables` 選項顯示已添加到Data Warehouse中並且已從選定列複製資料的所有表。

不在中查看您要查找的表 `All Tables` 清單？ 原因有幾：

* 尚未添加資料源
* 資料源是資料庫， [!DNL Commerce Intelligence] 您建立的用戶沒有訪問權限。 在這種情況下，您或資料庫管理員必須授予訪問權限。
* 最近添加了資料源或表，但尚未同步

## 同步表和列 {#syncing}

### 同步新表和本機列

Data Warehouse管理器不僅讓您能夠輕鬆查看和管理資料源，而且您還可以自由選擇要同步的各個表和列。

1. 按一下 `All Tables` 選項並找到要同步的表。
1. 按一下表的名稱以預覽架構。 如果表是新表，則所有列均顯示為 `Unsynced`。
1. 檢查要同步的列。

   >[!NOTE]
   >
   >表的本機列在 `Location` 的雙曲餘切值。

1. 確保檢查 `Primary Key` 列 — 這些列在列名旁邊有一個鍵符號。 A `Primary Key` 正確將資料同步到Data Warehouse。

   如果正在同步直接來自資料庫的表，則可能 `Primary Keys` 可能不表示。 在這種情況下，請與資料庫管理員聯繫，請求將主鍵或鍵添加到表中。
1. 完成後，按一下 ![按鈕](../../assets/button.png) 按鈕

A *成功！* 消息顯示，狀態更改為 `Pending` 的子菜單。 下次完全更新後，新同步的表和列將可用於報表。 也可以設定新 [複製方法](./cfg-replication-methods.md) 在初始同步後。

以下是整個過程的簡要介紹：

![向資料倉庫添加列](../../assets/DW_sync.gif)

### 正在後台同步新表 {#syncnew}

首次同步大表時，Data Warehouse需要追溯捕獲表中的所有資料點，然後才能持續捕獲新資料。 如果表很大，您可能不希望該初始同步與 **更新週期**。 在這種情況下，您希望在後台進行初始同步， *並行* 當前運行的任何更新。

要確保發生這種情況，應選擇 `Save and Sync Data Immediately` 選項首次同步該表。

### 檢查新表和列 {#forceupdate}

Data Warehouse在添加新源、表或列時不會自動檢測它們。 一個同步進程將在一週內運行，以查找新添加項並使其可用，但是，如果要在進程運行之前訪問新添加的表和列，則可以強制執行結構同步。

在表清單中的搜索欄下面 `Check for new tables and columns` 的子菜單。 按一下此連結將強制啟動結構同步過程；通常在10分鐘後提供新的添加。 刷新頁面以查看新源、表或列。

## 建立計算列 {#calculated}

只要能夠查看和管理來自所有來源的資料，就能更輕鬆地洞察您的業務。 但在Data Warehouse管理器中，可以通過在表內建立計算列來更進一步。 `Calculated` 列從現有資料中派生新資訊。

如果要添加 `user's lifetime revenue` 到 `users` 表以查找高價值用戶。 或者，如果您想按性別劃分收入，可以添加 `customer's gender` 到 `orders` 的子菜單。

有關詳細資訊，請查看此 [教程](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)。

## 刪除表和刪除列 {#delete}

正如可以選擇要同步到Data Warehouse的表和列一樣，您也可以刪除或刪除它們。

>[!NOTE]
>
>刪除表或刪除列將在確認刪除後刪除任何相關報表、度量、篩選器集和列。 確定你想這麼做。 **此操作無法撤消。**

按一下時不要擔心 **[!UICONTROL Delete]** 意外。 在刪除任何內容之前運行依賴關係檢查，因此您有機會在確認之前查看所有內容。

要刪除列，請按一下列所屬的表。 檢查要刪除的列，然後按一下 ![按鈕\1.png](../../assets/button_1.png) 按鈕

要刪除同步表，請選擇表中的所有列，然後再次按一下 ![按鈕](../../assets/button_1.png) 按鈕 這將從Data Warehouse中刪除使用此表的所有本機列和計算列。

### 確認更改

無論您是刪除表還是刪除列，刪除過程完成前都會運行依賴關係檢查。 相關性是使用要刪除的表或列的計算列、度量、篩選器集和報表。 所有發現的依賴關係都會顯示 — 此時，您可以取消進程或按一下 **[!UICONTROL Confirm Changes]** 刪除表/列。

雖然無法恢復已刪除的依賴項，但如果以後需要重新同步任何本機列，表和列仍將可用。

下面是刪除列的快速查看：

![從資料倉庫中刪除列](../../assets/DW_delete.gif)

## 那麼，我什麼時候才能使用新欄目？ {#when}

新同步的列和新的/已更新的計算列將在下次完全更新完成後可供使用。 如果更新尚未進行，可通過按一下 **[!UICONTROL Force update]** 顯示在 `Data Warehouse` 或 `Integrations` 的子菜單。 您還可以通過按一下在更新完成後安排電子郵件通知 **[!UICONTROL Email me when complete]**。

當您準備在報告中使用新列時， [您需要先將它們添加到度量](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。 雖然在更新完成之前資料不可用，但您仍然可以在報告中使用新列。 完成更新後，報表中的資料將顯示。

## 收尾

這篇文章涉及很多材料。 現在，您應該對資料庫是什麼、資料的組織方式、表之間的關係以及您可以對Data Warehouse管理器執行什麼操作有了深入的瞭解。

test您的知識 [建立計算列](../data-warehouse-mgr/creating-calculated-columns.md) 或 [作了一些有趣的報告](../../tutorials/using-visual-report-builder.md)。
