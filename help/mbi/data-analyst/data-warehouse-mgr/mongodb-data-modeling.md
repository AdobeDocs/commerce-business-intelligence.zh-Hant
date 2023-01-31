---
title: MongoDB資料模型
description: 了解如何避免造成問題的資料模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# [!DNL MongoDB] 資料模型

當 [!DNL MBI] 拉進 [!DNL MongoDB] 資料，該資料被轉換為關係模型。

壞消息是：雖然大多數資料模式都不會造成問題，但由於轉換為關係模型， [!DNL MBI] 不支援。

好消息是：所有這些模式都可以避免。

## 子巢狀陣列 {#subnested}

如果您的集合如下列範例， [!DNL MBI] 只會復寫項目陣列中的資料。 不會提取子項目陣列中的資料。

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

不會在中複製包含物件及變數物件索引鍵的集合 [!DNL MBI]. 例如：

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

這通常發生在使用物件且陣列更適當的地方。 現在，我們將重新處理上述範例：

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
