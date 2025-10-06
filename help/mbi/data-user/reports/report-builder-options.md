---
title: 選擇Report Builder
description: 瞭解如何選擇您的Report Builder。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# 選擇Report Builder

>[!NOTE]
>>需要[管理員許可權](../../administrator/user-management/user-management.md)。

現在您有了更多建立分析的選項，有時候可能很難確切知道Report Builder的哪一種風格適合您的需求。 本主題將引導您選擇最佳方法來建置分析。

## 何時應使用[!DNL SQL Report Builder]？ {#whensql}

檢視在[!DNL SQL Report Builder]上使用[!DNL traditional Report Builder]的一些較常見的原因。

### 如果您要使用[!DNL SQL]特定函式……

[!DNL SQL Report Builder]的優點部分在於它可讓您使用Data Warehouse Manager中目前無法提供的功能。 在過去，分析師可能必須介入以幫助您完全實現您的願景。

[!DNL SQL Report Builder]支援[`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html)和[`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)等您先前無法使用的功能。 您可以存取[`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)，但其他一些SQL特定函式包括：

* [`Bitwise aggregate`個函式](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation`運運算元](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 如果您想要執行一些測試……

如果您想要嘗試不同的技巧和策略來找出最適合您的分析方式，您可能會想要使用[!DNL SQL Report Builder]。 在Data Warehouse Manager中建置欄需要一些時間，而您使用DWM建立的欄則取決於更新週期。

您最多只能等待一個更新週期，才能使用欄。 如果您發現建置欄時發生錯誤，您必須等待&#x200B;*兩個*&#x200B;週期：一個最初填入欄，另一個週期用於傳播修訂。

### 如果您只使用新欄一次……

如上一節所述，在Data Warehouse Manager中建立欄需要時間。 如果您只打算在一個報表中使用您建立的欄，Adobe建議使用[!DNL SQL Report Builder]。 如此一來，您就不需要等待更新週期完成，可以更快速地恢復工作。

### 如果您使用的資料具有一對多關係……

有時候，資料的結構可能會讓[!DNL SQL Report Builder]成為建置分析時更有效率且更符合邏輯的選擇。 在Data Warehouse Manager中直接建立一對一關係的欄，但在處理一對多關係時，可能會有點混亂。

假設將單一產品視為多個產品類別的一部分，而您想要檢視與每個產品的每個類別相關聯的收入。 嘗試使用DWM建立此關聯性可能既繁瑣又困難，但撰寫[!DNL SQL]查詢可能更簡單明瞭：

![SQL查詢顯示具有一對多關係的產品類別收入](../../assets/When_should_I_use_the_RB_2.png)

## 我何時應使用傳統Report Builder？ {#whentraditionalrb}

雖然[!DNL SQL Report Builder]可讓您對先前無法使用的功能擁有更多控制權和存取權，但可能並不一定都是正確的選擇。 Adobe建議您也在決定要使用的Report Builder風格時，考量下列事項。

### 如果您要建置簡單的報表……

如果您要建立的查詢簡單明瞭，則使用傳統Report Builder的速度會比撰寫完整[!DNL SQL]查詢快很多。 如果您需要建立分析的任何欄已位於Data Warehouse Manager中，這會有所幫助。

### 如果您正在與其他使用者共用您的工作……

貴組織的使用者是否使用/檢視此分析？ 視您和誰共用您的工作而定，有時候使用Visual Report Builder可能會更好。 使用者可以快速檢視[!DNL Visual Report Builder]中的定義，而不是讀取可能較長的[!DNL SQL]查詢。

如果有人需要報告但不熟悉[!DNL SQL]，Adobe建議使用Report Builder的原始風格。 這樣會讓事情變得更容易。

## 正在結束 {#wrapup}

[!DNL SQL Report Builder]和[!DNL Visual Report Builder]都適合各種使用案例。 這通常取決於您的分析需求以及分析的使用者。
