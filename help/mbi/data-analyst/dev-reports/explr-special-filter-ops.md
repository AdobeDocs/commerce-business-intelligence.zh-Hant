---
title: 特殊篩選運算子
description: 了解建立報表或建立量度時，篩選器中使用的一些特殊運算子。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 篩選選項

在本文中，我們將探索一些特殊的 `operators` 用於 `filters` when [建立報表](../../tutorials/using-visual-report-builder.md){:target=&quot;_blank&quot;}或 [建立量度](../../data-user/reports/ess-manage-data-metrics.md){:target=&quot;_blank&quot;}。

## `Filter Operators`

* `LIKE` 模式比對。 這必須與通配符%（用於字母數可變的通配符）或_（用於通配符單字母）一起使用。  例如，限制 `LIKE \_ake%` 會傳回true `Jake Stein`, `Jake Smith`，或 `Fake Smith`.  若為，則會傳回false `Drake Smith`.

* `NOT LIKE` 類似於上述的模式比對，但會檢查哪些模式不相符。

* `IS` 檢查列是否為 `NULL`，或空白。

* `IS NOT` 類似於 `IS` 運算子，但檢查非NULL欄。

* `IN` 檢查值是否以逗號分隔的清單存在。 (例如，「顏色」 `IN` 紅色，橙色」等同於顏色 `equal to` 紅色或顏色 `equal to` 橙色)。

* `NOT IN` 類似 `IN` ，但會檢查值是否缺少。
