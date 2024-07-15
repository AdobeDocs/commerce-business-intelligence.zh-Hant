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

本主題探討[建立報告](../../tutorials/using-visual-report-builder.md){： target=&quot;_blank&quot;}或[建立量度](../../data-user/reports/ess-manage-data-metrics.md){： target=&quot;_blank&quot;}時`filters`使用的一些特殊`operators`。

## `Filter Operators`

* `LIKE`模式比對。 這必須搭配萬用字元% （適用於包含可變字母數的萬用字元）或_ （適用於萬用字元單一字母）。  例如，限制`LIKE \_ake%`會針對`Jake Stein`、`Jake Smith`或`Fake Smith`傳回true。  會針對`Drake Smith`傳回false。

* `NOT LIKE`類似於上述的模式比對，但檢查哪些模式不相符。

* `IS`檢查資料行是`NULL`或空白。

* `IS NOT`類似於上面的`IS`運運算元，但檢查非NULL資料行。

* `IN`檢查逗號分隔清單中是否有值。 （例如，「Color `IN` red，orange」等於`equal to` red或`equal to` orange的顏色）。

* `NOT IN`與上述`IN`類似，但檢查某值是否缺席。
