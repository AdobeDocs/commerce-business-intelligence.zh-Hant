---
title: 將資料庫最佳化以供分析
description: 瞭解如何最佳化資料庫以供分析。
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Developer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/5UkWGr-YOIfCy-BSomo2HWexXd-oM9ONvXpJkzyTPT0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 864
ht-degree: 0%

---

# 最佳化您的資料庫

對[!DNL Adobe Commerce Intelligence]使用作業資料庫的主要優點是，不需要建立或修改任何內容即可收集資料。 有價值資訊已經存在 — 您只需要解除鎖定即可。

本主題包含一些建議，可協助您最佳化資料庫以進行分析，以及從原始資料中得出可行的深入分析。

## 不要刪除資料

>[!TIP]
>
>影響您業務的當地和國際法律（以及您自己的服務條款）可能會影響您可以保留的資料型別，以及可以保留資料多久。 遵守這些法規應該是您的首要任務。

當訂單被取消、使用者停用其帳戶或產品被中止時，會嘗試刪除資料庫中的相關資訊。 增加表格數量及避免凌亂似乎是明智的作法。 不過，刪除列表示這些資訊會永遠遺失，或者您必須深入瞭解舊備份才能找到這些資訊。

反之，您可以將狀態列新增至表格，以指出資料列何時不再有效或相關。 也建議新增欄以儲存進行變更的日期，或建立歷史變更的記錄。 如果表格變得足夠大，效能開始受到影響，請考慮將舊資料封存到用於分析的表格。

## 很少覆寫資料

應謹慎覆寫資料。

許多公司以登入日期為例，儲存的是上次登入日期，而非歷史登入表格。 雖然您僅需上次登入日期即可使用功能，但若從分析角度來看，該被覆寫資料會造成巨大損失。 若未保留這些動作的完整記錄，則無法檢視有多少使用者長時間離開後又重新啟動。 此外，也無法根據登入建立使用者參與同類群組分析等專案。

一般而言，如果您因某類使用者動作而更新記錄，請勿覆寫有關先前或個別使用者動作的資訊。

## 包含`Updated_at`個資料行，這些資料會隨著時間更新

如果資料表的資料列會隨著時間而變更值（例如&#x200B;**order\_status**&#x200B;從`processing`變更為`complete`），請包含&#x200B;**updated\_at**&#x200B;資料行，以便在最新變更發生時加以記錄。 當&#x200B;**updated\_at**&#x200B;日期對應至&#x200B;**created\_at**&#x200B;日期時，請確定第一次插入新資料列時有&#x200B;**updated\_at**&#x200B;值可用。

除了針對分析最佳化，**updated\_at**&#x200B;資料行也可讓您使用[增量復寫方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)，以協助縮短更新週期的長度。

## 商店使用者贏取Source

最常見的錯誤之一是[使用者贏取來源](../data-analyst/analysis/google-track-user-acq.md) (UAS)未儲存在作業資料庫中。 在多數情況下，當這個問題出現時，只會透過[!DNL Google Analytics]或其他網站分析工具來追蹤UAS。 雖然這些工具可能很有價值，但僅在這些工具中儲存UAS有一些缺點；例如，您無法從這些工具中擷取使用者層級的資料。 如果可能的話，這通常是一個困難的過程。 應該可以輕鬆取得這些資訊，並將其與其他來源的資料結合，例如也儲存在資料庫中的行為和交易式資訊。

將UAS儲存在您自己的資料庫中，通常是線上企業對其分析能力所能做的最大改進。 這可讓UAS分析銷售額、使用者參與度、回收期、客戶期限值、流失率和其他關鍵量度。 [此資料在決定投資行銷資源的位置時十分重要](../data-analyst/analysis/most-value-source-channel.md)。

太多公司只關注尋找以最低成本提供新使用者的管道。 如果您沒有追蹤從每個管道取得的使用者品質，就有可能吸引未帶來業務價值的使用者。

## 資料表格設定

### 設定主索引鍵

[主索引鍵](https://en.wikipedia.org/wiki/Unique_key)是在資料表中產生唯一值的未變更資料行（或資料行集）。 主索引鍵非常重要，因為它們可確保您的資料表在[!DNL Commerce Intelligence]中正確複製。

建立主索引鍵時，請為自動增加的欄使用整數資料型別。 Adobe建議您儘可能避免使用多欄主索引鍵。

如果您的表格是SQL檢視，請新增可以當作主索引鍵的資料行。 [!DNL Commerce Intelligence]能夠自動識別此資料行為主索引鍵。

### 指派資料型別至您的資料欄

如果資料欄沒有指派的[資料型別](https://en.wikipedia.org/wiki/Data_type)，[!DNL Commerce Intelligence]會猜測要使用哪個資料型別。 如果系統猜測不正確，您可能無法執行相關的分析，直到Adobe支援團隊將欄調整為適當的資料型別。 例如，如果日期欄猜測為數值資料型別，您可以使用日期維度來分析一段時間內的趨勢。

### 如果您有多個資料庫，請在資料表格中新增前置詞

如果您有多個資料庫連線至[!DNL Commerce Intelligence]，Adobe建議您新增首碼至表格，以避免混淆。 字首可協助您記住量度或資料維度的來源位置。
