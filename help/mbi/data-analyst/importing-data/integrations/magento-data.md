---
title: 預期的Commerce資料
description: 探索Commerce使用者匯入Commerce Intelligence的主要資料表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 預期 [!DNL Adobe Commerce] 資料

在您擁有 [已連線您的 [!DNL Adobe Commerce] 儲存](../../../data-analyst/importing-data/integrations/magento.md)，您可使用Data Warehouse管理員輕鬆地從Commerce資料庫追蹤相關資料欄位以進行分析。

本主題探討Commerce使用者匯入的主要資料表格 [!DNL Commerce Intelligence].

| **表格名稱** | **說明** |
|-----|-----|
| `Customers` | 此 `customer\_entity` 和相關表格說明與每個頁面相關的資訊 *註冊客戶* ，例如其電子郵件地址和註冊日期。 有了這些資訊，您就可以開始依客戶層級的屬性和同類群組進行分段。 |
| `Orders` | 此 `sales\_flat\_order` 表格會記錄所有訂單，包括 `created\_at` 下訂單的時間戳記，以及 `base\_grand\_total` 總計收入的欄位。 這些欄位是訂單層級量度的基礎。 如果訂單是由 *註冊客戶*，則 `customer\_id` 欄位連結返回  `customer\_entity` 此表格可分析客戶的購買行為。 |
| `Order items` | 此 `sales\_flat\_order\_item` 表格會記錄每個屬於訂單的專案。 這包括 `price` 和 `qty\_ordered` 欄位，以及 `order\_id` 連線至的欄位 `sales\_flat\_order` 表格。 此表格為下列量度的基礎 `Item sold`，並可讓您依據以下條件進行分段： `product` 和 `product type`. |
| `Products` | 此 `catalog\_product\_entity` 表格會儲存產品層級屬性的相關資訊，例如類別、大小和顏色。 |
| `Categories` | 您的產品屬於一或多個不同專案 `product categories`，視您的Commerce組建設定方式而定。 此 `catalog\_category\_entity` 表格會儲存這些類別的階層（例如「服飾>上衣> T恤」），以及 `catalog\_category\_product` 表格會記錄您的產品與那些類別之間的連線。 |

{style="table-layout:auto"}

## 相關

* [正在連線 [!DNL Adobe Commerce]](../integrations/magento.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
