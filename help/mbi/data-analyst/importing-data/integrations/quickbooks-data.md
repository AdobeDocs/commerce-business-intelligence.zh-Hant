---
title: 需要的QuickBook資料
description: 瞭解如何輕鬆跟蹤相關資料欄位以便進行分析。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# 預期 [!DNL QuickBooks] 資料

之後 [您已連接 [!DNL QuickBooks] 帳戶](../../../data-analyst/importing-data/integrations/quickbooks.md)，可以使用 [Data Warehouse管理器](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 輕鬆跟蹤相關資料欄位進行分析。 在您的Data Warehouse中建立了以下表：

要查看所有可用於跟蹤的欄位，請按一下表名列中的連結。

## 事務實體 {#transactionentities}

| **表名** | **說明** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | 的 `bills` 表包含有關AP交易或第三方付款請求的資訊。 屬性包括幣種類型、匯率、總額、到期日、餘額等。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` 實體是從供應商接收的票據付款的最終交易記錄。 此表包括供應商資訊、付款類型、總額、交易記錄日期等。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | 的 `creditmemos` 表記錄全額付款和部分付款的退款或貸項交易記錄。 某些屬性包括客戶名稱、客戶的開單和發運資訊、金額和日期。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` 包括直接存款及客戶付款，該等款項於資產 `Undeposited Funds` 帳戶。 屬性包括金額、存款ID和日期。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` 是指給予客戶的交易，包括建議的商品或服務定價。 此表記錄金額、任何折扣資訊、客戶資訊和日期。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` 是客戶以後支付的銷售表。 發票表記錄任何存款資訊、日期、行項目、稅務資訊和客戶資訊。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | 的 `journalentries` 表記錄AR和AP帳戶資訊，包括日記帳分錄ID、事務處理日期和行項資訊。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | A `payment` 記錄包括付款ID、已核銷金額和未核銷金額、交易記錄日期、交易記錄類型和處理狀態等屬性。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | 的 `purchases` 表表示您的支出，包括採購ID、付款類型、金額和任何行項目資訊。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | 的 `purchaseorders` 表包含發送給供應商的貨物請求。 此表包括供應商資訊、採購訂單ID、交易記錄日期、行項目資訊、總金額和AP帳戶資訊。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | 的 `refundreceipts` 表記錄給客戶的退款。 屬性包括退款收款ID、行項目資訊、總額、客戶資訊和餘額。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | 的 `salesreceipts` 表記錄提供給客戶的銷售收據中的資訊，包括銷售收據ID、行項目資訊、總額、客戶資訊、交易記錄日期和任何存款。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | 的 `timeactivities` 表保存供應商和/或員工的時間記錄，包括時間活動ID、員工/供應商資訊、記錄的時間、活動說明和記錄的日期。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | 的 `transfers` 表記錄有關在帳戶之間移動的資金的資訊。 屬性包括轉移ID、金額、帳戶資訊和日期。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 供應商貸項是退款或貸項給供應商的AP交易記錄。 的 `vendorcredits` 表包括供應商信用ID、行項目資訊、供應商資訊、AP帳戶、總金額和日期。 |

{style="table-layout:auto"}

## 名稱清單實體 {#namelistentities}

| **表名** | **說明** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | 此表包括帳戶ID、名稱、狀態、類型、餘額、幣種和建立時間。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | 此表記錄與公司預算相關的所有資訊，包括預算ID、名稱、起始日期和終止日期、類型、狀態和詳細資訊。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | 類（應用於事務處理的明細行）允許您跟蹤未綁定到客戶端或項目的段。 此表記錄類ID、名稱、子類和狀態。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | 的 `customers` 表包含與客戶有關的所有資訊，包括客戶的ID、名稱、帳單和發運地址、電話號碼和電子郵件地址。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | 的 `departments` 表包括部門ID、名稱和類型（子部門與頂級部門）。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | 的 `employees` 表記錄了有關為您的公司工作的人員的資訊。 屬性包括員工ID、姓名、地址、電話號碼和可開單資訊（如果公司啟用了工資單）。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | 的 `items` 表包含您公司銷售的產品或服務的詳細資訊。 此表包括物料ID、名稱、說明、單價、類型、採購資訊、現有量以及收入和資產帳戶資訊。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | 的 `paymentmethods` 表記錄了貨物和服務的付款方式。 它包含付款ID、類型和名稱。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | 此表記錄有關稅務機構的資訊，包括稅務機構ID，以及有關採購和銷售的稅的跟蹤資訊。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 稅碼用於跟蹤產品、服務和客戶的稅狀態（應稅與不應稅）。 的 `taxcodes` 表包括稅碼標識、名稱、說明、狀態、應納稅狀態、稅率和稅組。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 稅率用於計算稅項負債。 此表包括稅率ID、名稱、說明、稅率、稅務代理等。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | 該實體指進行銷售之條款。 術語表包括術語ID、名稱、類型、折扣百分比和到期日。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 供應商表包含有關您從中購買的供應商的資訊。 表屬性包括供應商ID、公司名稱、帳號、帳戶餘額、1099狀態、開單地址、電話號碼、電子郵件地址和網址。 |

{style="table-layout:auto"}

## 相關：

* [連接 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
