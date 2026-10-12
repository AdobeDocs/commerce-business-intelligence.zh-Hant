---
title: 特殊篩選運運算元
description: 瞭解建立報告或建立量度時，篩選器中使用的幾個特殊運運算元。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: 'https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
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
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%
---
# 篩選器選項

本主題探討[建立報告](../../tutorials/using-visual-report-builder.md){: target="_blank"}或[建立量度](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}時`filters`中使用的一些特殊`operators`。

## `Filter Operators`

* `LIKE`模式比對。 這必須搭配萬用字元% （適用於包含可變字母數的萬用字元）或_ （適用於萬用字元單一字母）。  例如，限制`LIKE \_ake%`會針對`Jake Stein`、`Jake Smith`或`Fake Smith`傳回true。  會針對`Drake Smith`傳回false。

* `NOT LIKE`類似於上述的模式比對，但檢查哪些模式不相符。

* `IS`檢查資料行是`NULL`或空白。

* `IS NOT`類似於上面的`IS`運運算元，但檢查非NULL資料行。

* `IN`檢查逗號分隔清單中是否有值。 （例如，「Color `IN` red，orange」等於`equal to` red或`equal to` orange的顏色）。

* `NOT IN`與上述`IN`類似，但檢查某值是否缺席。
