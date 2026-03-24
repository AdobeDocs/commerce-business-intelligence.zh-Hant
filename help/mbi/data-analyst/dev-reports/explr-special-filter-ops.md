---
title: 特殊篩選運運算元
description: 瞭解建立報告或建立量度時，篩選器中使用的幾個特殊運運算元。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 143
ht-degree: 0%

---

# 篩選器選項

本主題探討`operators`建立報告`filters`或[建立量度](../../tutorials/using-visual-report-builder.md){: target="_blank"}時[中使用的一些特殊](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}。

## `Filter Operators`

* `LIKE`模式比對。 這必須搭配萬用字元% （適用於包含可變字母數的萬用字元）或_ （適用於萬用字元單一字母）。  例如，限制`LIKE \_ake%`會針對`Jake Stein`、`Jake Smith`或`Fake Smith`傳回true。  會針對`Drake Smith`傳回false。

* `NOT LIKE`類似於上述的模式比對，但檢查哪些模式不相符。

* `IS`檢查資料行是`NULL`或空白。

* `IS NOT`類似於上面的`IS`運運算元，但檢查非NULL資料行。

* `IN`檢查逗號分隔清單中是否有值。 （例如，「Color `IN` red，orange」等於`equal to` red或`equal to` orange的顏色）。

* `NOT IN`與上述`IN`類似，但檢查某值是否缺席。
