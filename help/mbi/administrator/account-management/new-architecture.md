---
title: 新架構
description: 瞭解遷移至新架構的好處。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# 新架構

[!DNL Adobe Commerce Intelligence]產品和工程團隊在過去一年中專注於儘可能進行最全面、要求最高的改進。 Adobe很高興宣佈推出新的[!DNL Commerce Intelligence]產品架構，讓這些改善成為現實。

## 新架構的優點

* 在Data Warehouse中建立欄型別，包括使用SQL的計算欄。
* 新欄可立即使用。
* 資料延遲大幅改善。

## 技術優點

主要差異列於上面，但主要變更是在更新週期中執行計算的方式。 計算不再於每次更新期間在每個欄上執行；而是從Visual Report Builder隨選執行。

### 遷移至新架構

由於帳戶是以不同方式建置，因此不會自動將您的Data Warehouse或報表移轉至新的架構帳戶。 要遷移至新架構，必須重新實作您現有的帳戶。

### 遷移至新架構的成本

沒有新增成本！ Adobe會為您建立此新帳戶，以開始重新實作（至少一個月免費）。 這可讓您有時間開啟兩個帳戶，以便更輕鬆地執行重新實作，並確保您的團隊在服務方面沒有間隙。

### 在新架構中重新實作帳戶所需的時間

重新實作時間視您要重建的專案而定。 Adobe建議您在現有帳戶中執行下列步驟，以瞭解重新實施中將涉及的步驟：

* 識別一組核心報表/控制面板。
* 識別建立這些報表所需的量度和維度。
* 識別重新建立這些量度和維度所需的欄。

完成此操作後，您就會知道您需要將哪些資料同步至新架構Data Warehouse，才能重新建置這些核心報表。

### 取得協助

[!DNL Adobe Commerce Intelligence] [服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)可以執行您的重新實作，但需額外付費。 請連絡您的[Adobe帳戶團隊](../../guide-overview.md#Submitting-a-Support-Ticket)，並準備好提供您想要優先在新帳戶中建立的控制面板/報告清單

### 繼續使用現有架構

如果這些功能對您來說並不重要，您可以繼續使用現有帳戶。 保留現有帳戶不需要額外付費。 Adobe會繼續支援這些帳戶，不會有任何變更。
