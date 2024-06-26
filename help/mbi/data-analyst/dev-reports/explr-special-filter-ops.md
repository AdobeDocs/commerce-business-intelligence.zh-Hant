---
title: 特殊篩選運運算元
description: 瞭解建立報告或建立量度時，篩選器中使用的幾個特殊運運算元。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# 篩選器選項

本主題探討幾項特殊優惠 `operators` 使用位置 `filters` 當 [建立報告](../../tutorials/using-visual-report-builder.md){： target=&quot;_blank&quot;}或 [建立量度](../../data-user/reports/ess-manage-data-metrics.md){： target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` 模式比對。 這必須搭配萬用字元% （適用於包含可變字母數的萬用字元）或_ （適用於萬用字元單一字母）。  例如，限制 `LIKE \_ake%` 會傳回true `Jake Stein`， `Jake Smith`，或 `Fake Smith`.  針對，系統會傳回false `Drake Smith`.

* `NOT LIKE` 類似於上述的模式比對，但檢查哪些模式不相符。

* `IS` 檢查欄是否為 `NULL`，或空白。

* `IS NOT` 與 `IS` 運運算元，但檢查非NULL欄。

* `IN` 檢查以逗號分隔的清單中是否有值的存在。 (例如，「顏色」 `IN` 紅色，橘色」等同於顏色 `equal to` 紅色OR顏色 `equal to` 橙色)。

* `NOT IN` 類似 `IN` 上方，但檢查某值的缺失。
