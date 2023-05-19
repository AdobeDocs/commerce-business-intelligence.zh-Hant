---
title: 特殊篩選器運算子
description: 瞭解在建立報告或建立度量時篩選器中使用的幾個特殊運算子。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 篩選器選項

本主題探討 `operators` 用於 `filters` 何時 [建立報表](../../tutorials/using-visual-report-builder.md){:target=&quot;_blank&quot;或 [建立度量](../../data-user/reports/ess-manage-data-metrics.md){:target=&quot;_blank&quot;}。

## `Filter Operators`

* `LIKE` 模式匹配。 這必須與通配符%（用於字母數可變的通配符）或_（用於通配符單字母）一起使用。  例如， `LIKE \_ake%` 將返回true `Jake Stein`。 `Jake Smith`或 `Fake Smith`。  它將返回false `Drake Smith`。

* `NOT LIKE` 類似於上面的模式匹配，但檢查哪些模式不匹配。

* `IS` 檢查列是否為 `NULL`或空。

* `IS NOT` 與 `IS` 上的運算子，但檢查非NULL列。

* `IN` 檢查以逗號分隔的清單中是否存在值。 (例如，「顏色」 `IN` 紅色，橙色」等同於顏色 `equal to` 紅色或顏色 `equal to` 橙色)。

* `NOT IN` 與 `IN` 但檢查值的缺失。
