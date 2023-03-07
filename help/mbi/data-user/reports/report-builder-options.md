---
title: 選擇報告建立工具
description: 了解如何選擇您的Report Builder。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 選擇報告建立工具

>[!NOTE]
>>需要 [管理權限](../../administrator/user-management/user-management.md).


現在您有更多建立分析的選項，有時候您可能很難確切知道報告建立工具的哪一種風格符合您的需求。 本文會引導您選擇建立分析的最佳方式。

## 何時應使用 `SQL Report Builder`? {#whensql}

請查看您使用SQLReport Builder(而非傳統Report Builder)的一些更常見原因。

### 如果要使用SQL特定函式……

這是 `SQL Report Builder` 即可讓您使用「Data Warehouse管理員」中目前未提供的函式。 過去，分析師可能不得不介入，幫助你充分實現自己的願景。

SQLReport Builder支援以下功能： [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 和 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)，而您之前無法使用。 您可以存取 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但其他一些特定於SQL的函式包括：

* [`Bitwise aggregate` 函式](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 運算子](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果你想做些測試……

如果您想嘗試不同的技巧和策略，以找出最適合您分析的項目，您可能想使用 `SQL Report Builder`. 在「Data Warehouse管理器」中建立列需要時間，而您使用DWM建立的列取決於更新週期。

最多只能等待一個更新週期，才能使用欄。 如果你意識到你在建柱子時犯了錯誤，你必須等待 *two* 週期：一個要初始填入欄，另一個要傳播的修訂週期。

### 如果只使用新列一次……

如上節所述，在「Data Warehouse管理員」中建立欄需要時間。 如果您只打算使用在單一報表中建立的欄，Adobe建議使用 `SQL Report Builder`. 如此一來，您便不需要等待更新週期完成，就能更快地重新開始工作。

### 如果您使用的資料具有一對多關係……

有時，您的資料結構可能會將 `SQL Report Builder` 更有效、更符合邏輯的選擇來建立分析。 在「Data Warehouse管理員」中，為一對一關係建立欄是簡單明瞭的，但當您處理一對多關係時，情況可能會有些混亂。

假設單一產品被視為多個產品類別的一部分，而您想要檢視與每個產品的每個類別相關聯的收入。 嘗試使用DWM建立此關係可能既繁瑣又困難，但編寫SQL查詢可能會比較簡單：

![](../../assets/When_should_I_use_the_RB_2.png)

## 何時應使用傳統Report Builder? {#whentraditionalrb}

若 `SQL Report Builder` 讓您能夠更多控制並存取先前無法使用的功能，但可能並不總是正確的選擇。 Adobe建議您在決定要使用的報表建立工具類型時，也應考量下列事項。

### 如果您要建立簡單報表……

如果您要建立的內容簡單明瞭，則使用傳統Report Builder可能比編寫完整SQL查詢快得多。 如果您建立分析所需的任何欄已在「Data Warehouse管理員」中，則此功能會有所幫助。

### 如果您正在與其他用戶共用您的工作……

貴組織的使用者是否使用/檢視此分析？ 根據您與誰共用您的工作，有時堅持視覺Report Builder可能會更好。 使用者可以快速查看可視化Report Builder中的定義，而不是讀取可能長的SQL查詢。

如果有些人需要報表，但不熟悉SQL,Adobe建議使用Report Builder的原始風格。 讓他們更輕鬆。

## 包裝 {#wrapup}

兩者 `SQL Report Builder` 和 `Visual Report Builder` 適合多種使用情況。 這通常取決於您的分析需求以及使用分析的人員。
