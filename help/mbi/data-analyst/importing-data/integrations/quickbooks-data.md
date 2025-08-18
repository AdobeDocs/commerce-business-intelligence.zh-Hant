---
title: 預期的QuickBooks資料
description: 瞭解如何輕鬆追蹤相關的資料欄位以進行分析。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 必須有[!DNL QuickBooks]個資料

在連線[您的 [!DNL QuickBooks] 帳戶](../../../data-analyst/importing-data/integrations/quickbooks.md)後，您可以使用[Data Warehouse管理員](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)輕鬆追蹤相關的資料欄位以進行分析。 下清單格會在您的Data Warehouse中建立：

若要檢視所有可用於追蹤的欄位，請按一下表格名稱欄中的連結。

## 交易實體 {#transactionentities}

| **資料表名稱** | **描述** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | `bills`表格包含有關AP交易的資訊，或來自協力廠商的付款要求。 屬性包括貨幣型別、匯率、總金額、到期日、餘額等。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment`個實體是從供應商收到的票據的最終付款交易。 此表格包含供應商資訊、付款型別、總金額、交易日期等。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | `creditmemos`表格會記錄全部與部份付款的退款或銷退折讓交易。 部分屬性包括客戶名稱、客戶的帳單和送貨資訊、金額和日期。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits`包括直接存款和客戶付款，這些付款在存入`Undeposited Funds`帳戶後移入資產帳戶。 屬性包括金額、存款ID和日期。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates`是提供給客戶的交易，其中包含商品或服務的建議定價。 此表格會記錄金額、任何折扣資訊、客戶資訊及日期。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices`是客戶稍後付款的銷售表單。 商業發票表格會記錄任何存款資訊、日期、明細行專案、稅捐資訊及客戶資訊。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | `journalentries`表格會記錄AR與AP帳戶資訊，包括分錄識別碼、交易日期及明細專案資訊。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | `payment`記錄包含付款ID、套用和未套用金額、交易日期、交易型別和處理狀態等屬性。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | `purchases`表格代表您的費用，並包含購買ID、付款型別、金額及任何明細專案資訊。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | `purchaseorders`表格包含傳送給廠商的貨品要求。 此表格包含供應商資訊、採購單識別碼、交易日期、明細行料號資訊、總金額及AP帳戶資訊。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | `refundreceipts`表格會記錄給予客戶的退款。 屬性包括退款收款識別碼、明細行專案資訊、總金額、客戶資訊及餘額。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | `salesreceipts`表格會記錄指定給客戶的銷售收款資訊，包括銷售收款識別碼、明細專案資訊、總金額、客戶資訊、交易日期及任何訂金。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | `timeactivities`表格包含廠商和/或員工的時間記錄，並包含時間活動ID、員工/廠商資訊、記錄時間、活動說明和記錄的日期。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | `transfers`表格會記錄帳戶之間已移動資金的資訊。 屬性包括移轉ID、金額、帳戶資訊和日期。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 廠商貸方是指退款或給予廠商貸方的AP交易。 `vendorcredits`表格包含廠商信用識別碼、明細專案資訊、廠商資訊、AP帳戶、總金額和日期。 |

{style="table-layout:auto"}

## 為清單實體命名 {#namelistentities}

| **資料表名稱** | **描述** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | 此表格包含帳戶ID、名稱、狀態、型別、餘額、貨幣和建立時間。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | 此表格會記錄與公司預算相關的所有資訊，包括預算識別碼、名稱、開始與結束日期、型態、狀態及明細。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | 套用至交易明細行的類別可讓您追蹤未與客戶或專案繫結的區段。 此表格會記錄類別ID、名稱、子類別和狀態。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | `customers`表格包含與您客戶相關的所有資訊，包括客戶ID、名稱、帳單和送貨地址、電話號碼及電子郵件地址。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | `departments`表格包含部門ID、名稱和型別（子部門與最上層部門）。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | `employees`表格會記錄您公司員工的資訊。 如果公司已啟用給薪功能，則屬性包括員工識別碼、姓名、地址、電話號碼及可開立帳單的資訊。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | `items`表格包含貴公司銷售的產品或服務的詳細資料。 此表格包含料號識別碼、名稱、摘要、單價、型態、採購資訊、庫存量以及收入與資產帳戶資訊。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | `paymentmethods`表格會記錄收到的貨品與服務付款方式。 它包含付款ID、型別和名稱。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | 此表格會記錄稅務代理的相關資訊，包括稅務代理識別碼，以及針對採購與銷售所追蹤的稅捐資訊。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 稅捐代碼可用來追蹤產品、服務及客戶的稅捐狀態（應稅與不納稅）。 `taxcodes`表格包含稅捐代碼識別碼、名稱、說明、狀態、應稅狀態、稅率及稅捐群組。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 稅率是用來計算稅捐負債。 此表格包含稅率識別碼、名稱、說明、稅率、稅務代理等。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | 此實體代表進行銷售所依據的條款。 字詞表包含字詞ID、名稱、型別、折扣百分比和到期日。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 「廠商」表格包含您購買之廠商的相關資訊。 表格屬性包括廠商ID、公司名稱、帳號、帳戶餘額、1099狀態、帳單地址、電話號碼、電子郵件地址和網址。 |

{style="table-layout:auto"}

## 相關：

* [正在連線 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [正在重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
