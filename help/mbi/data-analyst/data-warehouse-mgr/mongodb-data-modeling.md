---
title: MongoDB資料模式
description: 瞭解如何避免造成問題的資料模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
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
