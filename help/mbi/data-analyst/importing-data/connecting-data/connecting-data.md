---
title: 連線您的資料
description: 了解如何在「Data Warehouse管理員」中瀏覽可供同步的表格。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 連接資料

在 [!DNL MBI]，則會呼叫資料來源 `integrations`. 在 `integration` 已成功連接，您將能夠在「Data Warehouse管理器」中瀏覽可用於同步的表。

整合可透過 `Connections` 頁面，可按一下 **[!UICONTROL Manage Data** > **Connections]**. 您會在這裡看到連結至帳戶的所有整合、整合類型、狀態([!DNL Google Analytics] 和 [!DNL Data Import API] 連接將具有空白狀態欄位)，並且上次進行連接測試時(`Last Connection` 已啟動列)。

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 整合類型

有四種方式可將資料傳入 [!DNL MBI]:連接資料庫，連接SaaS整合，上傳 `.csv` 檔案，或使用我們的API。

## 資料庫整合

![資料庫\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] 支援基於SQL的資料庫和NoSQL資料庫，例如 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)，和 [PostgreSQL](../integrations/postgresql.md).

您可以直接將資料庫連接到 [!DNL MBI] 若使用資料庫憑證，建議您使用經驗證的加密方法，如SSH通道。 這可確保您的資料在進入您的資料倉庫時安全無虞。

根據連接方法和資料庫類型，完成設定可能需要一些技術專業知識。

## `SaaS` 整合

![](../../../assets/SaaS_icons.jpg)

`SaaS` 整合功能服務如 [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)，和 [[!DNL Zendesk]](../integrations/zendesk.md). 請務必注意，由於第三方資料位於供應商的伺服器上，因此您無法像使用資料庫中的資料那樣直接訪問它。

在大多數情況下，請在 [!DNL MBI] 就像輸入您的帳戶憑證一樣簡單。 某些服務可能需要API金鑰才能完成授權 — 請查看 [整合區段](../integrations/integrations.md) ，以了解有關生成您需要的任何憑據的說明。

## 檔案上傳

不確定如何將補充來源的資料匯入您的資料倉庫？ [使用 `File Upload` 功能](../connecting-data/using-file-uploader.md) 是提取日常決策不需要的資料的好方法。 依照我們的格式規則，您可以快速上傳 `.csv` 檔案放入您的資料倉庫，並與其他資料來源連結。

## [!DNL MBI] `Import API`

如果您想要自動擷取來自自己來源的資料，可使用 [!DNL MBI] `Import API`. 基本上：如果不在資料庫或 `SaaS` 整合， `Import API` 函式是最佳選擇。

使用API需要一些技術專業知識 — 熟悉編寫和維護小型Ruby或PHP指令碼的人將勝過資格。

若要進一步了解如何開始使用 `Import API`，請查看 [開發人員網站](https://developer.adobe.com/commerce/services/reporting/) 和 [如何產生API金鑰](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 新增整合

若要新增整合，請按一下 **[!UICONTROL Manage Data** > **Connections]** 然後按一下 **[!UICONTROL Add a New Data Source]**. 按一下您要新增的整合圖示，並依照說明文章中的指示進行設定：

* [整合常見問題集](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [可用 ](../integrations/integrations.md)
* [合併表](../../../best-practices/consolidating-your-tables.md)
* [限制對資料庫的訪問](../../../administrator/account-management/restrict-db-access.md)

**看不到您想要的整合？** 部分整合必須啟動，才能顯示在您的帳戶中。 如果您要尋找某些東西，例如 [!DNL Facebook]  — 但沒有列出， [提交支援票證](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

**如果您看到整合的錯誤狀態**，不要驚慌 — 請查看 [疑難排解區段](https://support.magento.com/hc/en-us/sections/360003078151) 來幫忙。
