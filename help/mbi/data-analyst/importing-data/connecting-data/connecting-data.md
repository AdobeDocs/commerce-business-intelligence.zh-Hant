---
title: 連接資料
description: 瞭解如何瀏覽可在Data Warehouse管理器中同步的表。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 連接資料

在 [!DNL Adobe Commerce Intelligence]，調用資料源 `integrations`。 在 `integration` 已成功連接，您將能夠瀏覽Data Warehouse管理器中可用於同步的表。

使用 `Connections` 頁，可通過按一下 **[!UICONTROL Manage Data** > **Connections]**。 在這裡，您看到：

* 與你的帳戶連接的所有整合的清單

* 整合類型

* 狀態(S)[!DNL Google Analytics] 和 [!DNL Data Import API] 連接的狀態欄位為空

* 上次連接test(`Last Connection Started` 列)

![資料\_源\_表.png](../../../assets/Data_Sources_Table.png)

## 整合類型

有四種方法可將資料 [!DNL Commerce Intelligence]:連接資料庫、連接SaaS整合、上載 `.csv` 或使用AdobeAPI。

## 資料庫整合

![資料庫\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] 支援基於SQL和NoSQL資料庫，如 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md)。 [MicrosoftSQL](../integrations/microsoft-sql-server.md)。 [蒙戈DB](../integrations/mongodb-via-ssh-tunnel.md), [PostgreSQL](../integrations/postgresql.md)。

您可以直接將資料庫連接到 [!DNL Commerce Intelligence] 使用資料庫憑據，Adobe建議您使用SSH隧道等經驗證的加密方法。 這可確保資料在進入您的Data Warehouse時保持安全。

根據連接方法和資料庫類型，可能需要一些技術專家才能完成安裝。

## `SaaS` 整合

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 整合服務 [[!DNL Google Adwords]](../integrations/google-adwords.md)。 [[!DNL Salesforce]](../integrations/salesforce.md), [[!DNL Zendesk]](../integrations/zendesk.md)。 由於第三方資料位於供應商的伺服器上，因此您不能像對資料庫中的資料那樣直接訪問它。

通常，在 [!DNL Commerce Intelligence] 只需輸入帳戶憑據即可。 某些服務可能需要API密鑰才能完成授權。 查看 [整合節](../integrations/integrations.md) 有關生成所需憑據的說明。

## 檔案上載

不確定如何從補充源獲取資料到您的Data Warehouse? [使用 `File Upload` 特徵](../connecting-data/using-file-uploader.md) 是收集資料的好方法，不需要日常決策。 遵循格式規則，可以快速上載 `.csv` 檔案到您的Data Warehouse中，並將它們與其他資料源連接。

## [!DNL Commerce Intelligence] `Import API`

如果您希望自動從您自己的源中檢索資料，則可以使用 [!DNL Commerce Intelligence] `Import API`。 基本上，如果它不在資料庫或 `SaaS` 整合， `Import API` 函式是最佳選擇。

使用API需要一些技術專業知識 — 對編寫和維護小型Ruby或PHP指令碼很滿意的人。

瞭解有關入門的詳細資訊 `Import API`，簽出 [開發人員網站](https://developer.adobe.com/commerce/services/reporting/) 和 [如何生成API密鑰](https://developer.adobe.com/commerce/services/reporting/import-api/)。

## 添加整合

要添加整合，請按一下 **[!UICONTROL Manage Data** > **Connections]** 然後按一下 **[!UICONTROL Add a New Data Source]**。 按一下要添加的整合表徵圖，然後按照幫助主題中的說明進行設定：

* [整合常見問題](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [可用 ](../integrations/integrations.md)
* [合併表](../../../best-practices/consolidating-your-tables.md)
* [限制對資料庫的訪問](../../../administrator/account-management/restrict-db-access.md)

**沒有看到您想要的整合？** 必須激活某些整合，才能在您的帳戶中看到這些整合。 如果你在尋找 [!DNL Facebook] 但沒有列出， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

**如果看到整合的錯誤狀態**，簽出 [「疑難解答」部分](https://support.magento.com/hc/en-us/sections/360003078151) 的雙曲餘切值。
