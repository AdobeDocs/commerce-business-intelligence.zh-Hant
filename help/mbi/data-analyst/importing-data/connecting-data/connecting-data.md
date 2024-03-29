---
title: 連線您的資料
description: 瞭解如何在Data Warehouse管理員中瀏覽可用於同步的表格。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 連線您的資料

在 [!DNL Adobe Commerce Intelligence]，資料來源稱為 `integrations`. 之後 `integration` 已成功連線，您將能夠在「Data Warehouse管理員」中瀏覽可供同步的表格。

整合可透過新增和管理 `Connections` 頁面，按一下即可存取 **[!UICONTROL Manage Data** > **Connections]**. 在這裡，您會看到：

* 與您帳戶連線的所有整合專案清單

* 整合型別

* 狀態([!DNL Google Analytics] 和 [!DNL Data Import API] 連線的狀態列位為空白)

* 上次連線測試的時間(`Last Connection Started` （欄）已執行

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 整合型別

有四種方式可將您的資料匯入 [!DNL Commerce Intelligence]：連線資料庫、連線SaaS整合、上傳 `.csv` 或使用AdobeAPI。

## 資料庫整合

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] 支援SQL和NoSQL資料庫，例如 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md)， [MICROSOFT SQL](../integrations/microsoft-sql-server.md)， [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)、和 [PostgreSQL](../integrations/postgresql.md).

雖然您可以直接將資料庫連線到 [!DNL Commerce Intelligence] Adobe使用資料庫證明資料時，建議您使用SSH通道等經驗證的加密方法。 這可確保您的資料在進入Data Warehouse時保持安全和安全。

視連線方法和資料庫型別而定，可能需要一些技術專業才能完成設定。

## `SaaS` 整合

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 整合是類似以下的服務 [[!DNL Google Adwords]](../integrations/google-adwords.md)， [[!DNL Salesforce]](../integrations/salesforce.md)、和 [[!DNL Zendesk]](../integrations/zendesk.md). 由於協力廠商資料位於供應商的伺服器上，因此您無法像使用資料庫中的資料一樣直接存取這些資料。

通常是在中設定整合 [!DNL Commerce Intelligence] 就像直接輸入您的帳戶憑證一樣簡單。 有些服務可能需要API金鑰才能完成授權。 檢視 [整合區段](../integrations/integrations.md) 以取得有關產生任何所需憑證的說明。

## 檔案上傳

不確定如何將補充來源的資料匯入Data Warehouse？ [使用 `File Upload` 功能](../connecting-data/using-file-uploader.md) 這是提取資料的好方法，您在日常決策中不需要這些資料。 依照格式化規則，您可以快速上傳 `.csv` 將檔案匯入您的Data Warehouse，並將它們與其他資料來源聯結。

## [!DNL Commerce Intelligence] `Import API`

如果您想從自己的來源中自動擷取資料，可以使用 [!DNL Commerce Intelligence] `Import API`. 基本上，如果不在資料庫或 `SaaS` 整合， `Import API` 函式是您的最佳選擇。

使用API需要一點技術專業知識 — 熟悉編寫和維護小型Ruby或PHP指令碼的人絕非合格人士。

若要進一步瞭解開始使用 `Import API`，檢視 [開發人員網站](https://developer.adobe.com/commerce/services/reporting/) 和 [如何產生API金鑰](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 新增整合

若要新增整合，請按一下 **[!UICONTROL Manage Data** > **Connections]** 然後按一下 **[!UICONTROL Add a New Data Source]**. 按一下要新增之整合的圖示，然後依照說明主題中的指示進行設定：

* [整合常見問題集](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [可用 ](../integrations/integrations.md)
* [合併您的表格](../../../best-practices/consolidating-your-tables.md)
* [限制對資料庫的存取](../../../administrator/account-management/restrict-db-access.md)

**沒有看見您想要的整合？** 您必須啟用部分整合，才會在您的帳戶中顯示。 如果您要尋找類似以下的專案 [!DNL Facebook] 但並未列出， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**如果您看到整合的錯誤狀態**，檢視 [疑難排解章節](https://support.magento.com/hc/en-us/sections/360003078151) 以取得協助。
