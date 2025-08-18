---
title: 預期Commerce資料
description: 探索Commerce使用者匯入Commerce Intelligence的主要資料表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 預期[!DNL Adobe Commerce]資料

連線[您的 [!DNL Adobe Commerce] 存放區](../../../data-analyst/importing-data/integrations/magento.md)後，您可以使用Data Warehouse Manager輕鬆追蹤Commerce資料庫中的相關資料欄位以進行分析。

本主題探索Commerce使用者匯入至[!DNL Commerce Intelligence]的主要資料表。

| **資料表名稱** | **描述** |
|-----|-----|
| `Customers` | `customer\_entity`和相關表格說明與資料庫中每個&#x200B;*已註冊客戶*&#x200B;相關聯的資訊，例如其電子郵件地址和註冊日期。 有了這些資訊，您就可以開始依客戶層級的屬性和同類群組進行分段。 |
| `Orders` | `sales\_flat\_order`表格會記錄所有訂單，包括下訂單的`created\_at`時間戳記，以及總和收入的`base\_grand\_total`欄位。 這些欄位是訂單層級量度的基礎。 如果訂單是由&#x200B;*註冊客戶*&#x200B;所訂，`customer\_id`欄位會連結回`customer\_entity`表格，以允許分析客戶購買行為。 |
| `Order items` | `sales\_flat\_order\_item`表格會記錄每個屬於訂單的專案。 這包含`price`和`qty\_ordered`欄位，以及連線至`order\_id`資料表的`sales\_flat\_order`欄位。 此表格是`Item sold`等量度的基礎，可讓您依`product`和`product type`分段。 |
| `Products` | `catalog\_product\_entity`表格儲存產品層級屬性的資訊，例如類別、大小和顏色。 |
| `Categories` | 您的產品屬於一或多個不同的`product categories`，端視您的Commerce組建設定方式而定。 `catalog\_category\_entity`表格會儲存這些類別的階層（例如，「服飾>上衣> T恤」），`catalog\_category\_product`表格會記錄您的產品與這些類別之間的連線。 |

{style="table-layout:auto"}

## 相關

* [正在連線 [!DNL Adobe Commerce]](../integrations/magento.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
