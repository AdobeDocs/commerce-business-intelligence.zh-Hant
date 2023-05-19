---
title: 選擇報表生成器
description: 瞭解如何選擇報表生成器。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# 選擇報表生成器

>[!NOTE]
>>需要 [管理權限](../../administrator/user-management/user-management.md)。


現在，您有了建立分析的更多選項，有時可能很難確切知道報告生成器的哪種風格適合您的需要。 本主題指導您選擇構建分析的最佳方法。

## 我何時應使用 [!DNL SQL Report Builder]? {#whensql}

看看一些比較常見的原因， [!DNL SQL Report Builder] 在 [!DNL traditional Report Builder]。

### 如果您想使用 [!DNL SQL] — 特定函式……

這是 [!DNL SQL Report Builder] 即它使您能夠使用Data Warehouse管理器中當前不可用的函式。 過去，分析師可能不得不介入，幫助你充分實現自己的願景。

的 [!DNL SQL Report Builder] 支援函式 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) 和 [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)，您以前不能使用。 您可以訪問 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但是其他一些特定於SQL的函式包括：

* [`Bitwise aggregate` 函式](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 算子](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果你想做些測試……

如果您想嘗試不同的技術和策略來找出最適合分析的方法，則可能希望使用 [!DNL SQL Report Builder]。 在Data Warehouse管理器中構建列需要時間，而使用DWM建立的列取決於更新週期。

最好，您必須等待一個更新週期，然後才能使用列。 如果你意識到你在建造柱子時犯了錯誤，你必須等待 *二* 循環：一個用於初始填充列，另一個用於傳播修訂的週期。

### 如果只使用新列一次……

如上節所述，在Data Warehouse管理器中建立列需要時間。 如果您僅計畫使用在一個報表中建立的列，Adobe建議使用 [!DNL SQL Report Builder]。 這樣就無需等待更新週期完成，從而讓您更快地恢復工作。

### 如果您正在處理具有一對多關係的資料……

有時，資料的結構可能會 [!DNL SQL Report Builder] 構建分析的更高效、更符合邏輯的選擇。 在「Data Warehouse經理」中，為一對一關係建立列很簡單，但在處理一對多關係時，情況可能會有些混亂。

假設單個產品被視為多個產品類別的一部分，並且您希望查看與每個產品的每個類別關聯的收入。 嘗試使用DWM建立此關係可能既繁瑣又困難，但編寫 [!DNL SQL] 查詢可能更簡單：

![](../../assets/When_should_I_use_the_RB_2.png)

## 我何時應該使用傳統Report Builder? {#whentraditionalrb}

當 [!DNL SQL Report Builder] 使您能夠更好地控制和訪問以前不可用的功能，它可能並不總是正確的選擇。 Adobe建議您在確定要使用的報表生成器的類型時，還應考慮以下因素。

### 如果您要構建簡單的報告……

如果要建立的內容是直接的，則使用傳統Report Builder比編寫完整檔案要快得多 [!DNL SQL] 的子菜單。 如果需要建立分析的任何列已在「Data Warehouse管理器」中，則此選項會有所幫助。

### 如果您正在與其他用戶共用您的工作……

整個組織的用戶是否在使用/查看此分析？ 根據您與誰共用您的工作，堅持視覺Report Builder有時可能會更好。 用戶可以快速查看 [!DNL Visual Report Builder] 與閱讀可能很長 [!DNL SQL] 的子菜單。

如果有人需要報告，但不熟悉 [!DNL SQL],Adobe建議使用Report Builder的原味。 這讓事情變得容易。

## 收尾 {#wrapup}

都 [!DNL SQL Report Builder] 和 [!DNL Visual Report Builder] 適合各種使用場合。 這通常取決於您的分析需求以及分析的使用者。
