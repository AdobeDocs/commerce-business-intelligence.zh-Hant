---
title: MongoDB資料建模
description: 瞭解如何避免造成問題的資料模式。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# [!DNL MongoDB] 資料建模

當 [!DNL Adobe Commerce Intelligence] 拉進 [!DNL MongoDB] 資料，資料被轉換為關係模型。

壞消息是：雖然大多數資料模式都不會帶來問題，但有一些資料不受支援 [!DNL Commerce Intelligence]，因為轉換為關係模型。

好消息是：所有這些圖案都可以避免。

## 子嵌套陣列 {#subnested}

如果你的收藏看起來像下面的例子， [!DNL Commerce Intelligence] 只複製items陣列中的資料。 不會從子項陣列中提取資料。

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

## 變數對象鍵 {#varobjectkeys}

不在中複製包含具有變數對象鍵的對象的集合 [!DNL Commerce Intelligence]。 例如：

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

這通常發生在使用對象和更合適的陣列的位置。 現在，重新編寫上面的示例：

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
