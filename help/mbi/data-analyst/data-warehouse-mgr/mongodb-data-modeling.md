---
title: MongoDB資料模式
description: 瞭解如何避免造成問題的資料模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: 'https://experienceleague.adobe.com/L9xlGE4hAQssTHJzzxQD9EGUVaIZFY-2-ALOLM9vym4'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%
---
# [!DNL MongoDB]資料模式

當[!DNL Adobe Commerce Intelligence]提取[!DNL MongoDB]資料時，該資料會轉換為關聯式模型。

壞消息：雖然大部分的資料模式不會造成問題，但有一些是[!DNL Commerce Intelligence]不支援的，因為轉換為關聯模型。

好消息：可以避免所有這些模式。

## 子巢狀陣列 {#subnested}

如果您的集合如下列範例所示，[!DNL Commerce Intelligence]只會複製專案陣列中的資料。 不會提取子專案陣列中的資料。

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## 變數物件索引鍵 {#varobjectkeys}

包含具有變數物件金鑰之物件的集合不會在[!DNL Commerce Intelligence]中復寫。 例如：

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

這通常發生在使用物件且陣列更合適的地方。 現在，請重製上述範例：

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
