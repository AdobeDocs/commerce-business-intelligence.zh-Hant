---
title: 預期的QuickBooks資料
description: 了解如何輕鬆追蹤相關資料欄位以進行分析。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# 預期 [!DNL QuickBooks] 資料

![](../../../assets/Quickbooks.png)

之後 [您已將 [!DNL QuickBooks] 帳戶](../../../data-analyst/importing-data/integrations/quickbooks.md)，您可以使用 [Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆追蹤相關資料欄位以進行分析。 會在您的資料倉庫中建立下清單格：

若要檢視所有可用於追蹤的欄位，請按一下表格名稱欄中的連結。

## 交易實體 {#transactionentities}

| **表名** | **說明** |
|-----|-----|
| [`bill`](https://developer.intuit.com/docs/api/accounting/Bill) | 票據表包含有關AP事務處理或第三方付款請求的資訊。 屬性包括幣種類型、匯率、總金額、到期日、餘額等。 |
| [`billpayments`](https://developer.intuit.com/docs/api/accounting/BillPayment) | BillPayment實體是從供應商接收的票據的付款的最終事務處理。 此表包括供應商資訊、付款類型、總金額、事務處理日期等。 |
| [`creditmemos`](https://developer.intuit.com/docs/api/accounting/CreditMemo) | 貸項通知單表記錄作為全額付款和部分付款的退款或貸項的事務處理。 某些屬性包括客戶名稱、客戶的帳單和運送資訊、金額和日期。 |
| [`deposits`](https://developer.intuit.com/docs/api/accounting/Deposit) | 存款包括直接存款及客戶款項，於資產賬戶持有 `Undeposited Funds` 帳戶。 屬性包括金額、存款ID和日期。 |
| [`estimates`](https://developer.intuit.com/docs/api/accounting/Estimate) | 估計乃給予客戶之交易，包括就商品或服務而建議之定價。 此表記錄金額、任何折扣資訊、客戶資訊和日期。 |
| [`invoices`](https://developer.intuit.com/docs/api/accounting/Invoice) | 發票是客戶以後支付的銷售表單。 發票表記錄所有存款資訊、日期、行項、稅資訊和客戶資訊。 |
| [`journalentries`](https://developer.intuit.com/docs/api/accounting/JournalEntry) | 日記帳分錄表記錄AR和AP帳戶資訊，包括日記帳分錄ID、事務處理日期和行項資訊。 |
| [`payments`](https://developer.intuit.com/docs/api/accounting/Payment) | 付款記錄包括諸如付款ID、已核銷和未核銷金額、交易日期、交易類型和處理狀態等屬性。 |
| [`purchases`](https://developer.intuit.com/docs/api/accounting/Purchase) | 採購表表示您的費用，並包括採購ID、付款類型、金額和任何行項資訊。 |
| [`purchaseorders`](https://developer.intuit.com/docs/api/accounting/PurchaseOrder) | 採購訂單是向供應商發送貨物的請求。 此表包括供應商資訊、採購訂單ID、交易日期、行項資訊、總金額和AP帳戶資訊。 |
| [`refundreceipts`](https://developer.intuit.com/docs/api/accounting/RefundReceipt) | 此表記錄給客戶的退款。 屬性包括退款收款標識、行項資訊、總金額、客戶資訊和餘額。 |
| [`salesreceipts`](https://developer.intuit.com/docs/api/accounting/SalesReceipt) | 銷售收款表記錄分配給客戶的銷售收款中的資訊，包括銷售收款標識、行項資訊、總金額、客戶資訊、交易日期和任何存款。 |
| [`timeactivities`](https://developer.intuit.com/docs/api/accounting/TimeActivity) | 時間活動是供應商和/或員工的時間記錄。 時間活動表包括時間活動ID、員工/供應商資訊、記錄的時間、活動說明和記錄的日期。 |
| [`transfers`](https://developer.intuit.com/docs/api/accounting/Transfer) | 轉移表記錄有關在帳戶之間移動的資金的資訊。 屬性包括轉移ID、金額、帳戶資訊和日期。 |
| [`vendorcredits`](https://developer.intuit.com/docs/api/accounting/VendorCredit) | 供應商貸項是指提供給供應商的退款或貸項的AP事務處理。 此 `vendorcredits` 表包括供應商信用ID、行項資訊、供應商資訊、AP帳戶、總金額和日期。 |

{style=&quot;table-layout:auto&quot;}

## 名稱清單實體 {#namelistentities}

| **表名** | **說明** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/docs/api/accounting/Account) | 此表包括帳戶ID、名稱、狀態、類型、餘額、幣種和建立時間。 |
| [`budgets`](https://developer.intuit.com/docs/api/accounting/Budget) | 此表記錄與公司預算相關的所有資訊，包括預算ID、名稱、起始日期和終止日期、類型、狀態和詳細資訊。 |
| [`classes`](https://developer.intuit.com/docs/api/accounting/Class) | 類別，套用至交易明細，可讓您追蹤未系結至用戶端或專案的區段。 此表記錄類ID、名稱、子類和狀態。 |
| [`customers`](https://developer.intuit.com/docs/api/accounting/Customer) | 「客戶」表格包含與客戶相關的所有資訊，包括客戶的ID、姓名、帳單和運送地址、電話號碼和電子郵件地址。 |
| [`departments`](https://developer.intuit.com/docs/api/accounting/Department) | 「部門」(departments)表包括部門ID、名稱和類型（子部門與頂級部門）。 |
| [`employees`](https://developer.intuit.com/docs/api/accounting/Employee) | 員工表記錄有關為您公司工作的人員的資訊。 屬性包括員工ID、姓名、地址、電話號碼和計費資訊（如果公司啟用工資單）。 |
| [`items`](https://developer.intuit.com/docs/api/accounting/Item) | 「項目」(items)表格包含貴公司所銷售產品或服務的詳細資訊。 此表包括項目標識、名稱、說明、單價、類型、採購資訊、現有量以及收入和資產帳戶資訊。 |
| [`paymentmethods`](https://developer.intuit.com/docs/api/accounting/PaymentMethod) | 付款方法表記錄為貨物和服務收到的付款方法。 它包含付款ID、類型和名稱。 |
| [`taxagencies`](https://developer.intuit.com/docs/api/accounting/TaxAgency) | 此表記錄有關稅務機構的資訊，包括稅務機構ID，以及有關採購和銷售稅的跟蹤資訊。 |
| [`taxcodes`](https://developer.intuit.com/docs/api/accounting/TaxCode) | 稅碼用於跟蹤產品、服務和客戶的稅狀態（應稅與非應稅）。 稅碼表包括稅碼標識、名稱、說明、狀態、應納稅狀態、稅率和稅組。 |
| [`taxrates`](https://developer.intuit.com/docs/api/accounting/TaxRate) | 稅率乃用於計算稅項負債。 此表包括稅率標識、名稱、說明、稅率、稅務代理等。 |
| [`terms`](https://developer.intuit.com/docs/api/accounting/Term) | 該實體指進行銷售之條款。 術語表包括術語ID、名稱、類型、折扣百分比和到期日。 |
| [`vendors`](https://developer.intuit.com/docs/api/accounting/Vendor) | 供應商表包含有關您從中購買的供應商的資訊。 表屬性包括供應商ID、公司名稱、帳號、帳戶餘額、1099狀態、帳單地址、電話號碼、電子郵件地址和網址。 |

{style=&quot;table-layout:auto&quot;}

## 相關：

* [連接 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [重新驗證整合](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
