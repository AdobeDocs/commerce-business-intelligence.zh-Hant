---
title: 管理Adobe Commerce使用者和許可權
description: 瞭解如何管理您的Commerce Intelligence使用者。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 管理使用者許可權

[!DNL Adobe Commerce Intelligence]是您組織的單一信任來源。 每個使用者都有自己的儀表板集，他們可以[與其他使用者共用](../../data-user/dashboards/share-dashboard-with-users.md)。

## 使用者許可權層級

在[!DNL Commerce Intelligence]中，有三個一般許可權層級適用於使用者，這些層級是在建立帳戶時選取的：

* `Admin`
* `Standard`
* `Read-Only`

這些許可權可讓使用者執行某些動作或存取[!DNL Commerce Intelligence]的特定部分。 以下表格列出每個許可權層級在[!DNL Commerce Intelligence]中可以執行的動作：

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **建立/管理使用者** | ✔ |   |   |
| **建立電子郵件摘要** | ✔ | ✔ |   |
| **建立/編輯/共用儀表板** | ✔ | ✔ |   |
| **檢視儀表板** | ✔ | ✔ | ✔ |
| **建立/編輯/刪除視覺化報告** | ✔ | ✔* |   |
| **建立/編輯/刪除SQL報告** | ✔ |  |   |
| **複製控制面板** | ✔ |   |   |
| **新增/管理整合** | ✔ |   |   |
| **存取Data Warehouse管理員** | ✔ |   |   |
| **同步/取消同步資料表和資料行** | ✔ |   |   |
| **建立/編輯量度** | ✔ |   |   |
| **建立/編輯篩選器集** | ✔ |   |   |
| **建立/編輯計算資料行** | ✔ |   |   |
| **建立相依報告的清單** | ✔ |   |   |
| **存取系統摘要** | ✔ |   |   |
| **存取時區設定** | ✔ |   |   |
| **存取帳單** | ✔ | ✔** |   |
| **連絡支援** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_您可以限制&#x200B;**[!UICONTROL Standard]**&#x200B;使用者對特定量度的[存取權](../../administrator/user-management/restrict-metric-access.md)。_
>
>**[!UICONTROL Standard] _使用者可以使用額外的許可權設定來存取帳單。_
>
>**[!UICONTROL Read-Only]**&#x200B;使用者只能&#x200B;_檢視_&#x200B;已與他們共用的儀表板；他們無法在[!DNL Commerce Intelligence]中建立或編輯任何內容，也無法搜尋並將新的儀表板新增到他們的帳戶。 Adobe建議您與您或團隊其他成員維護的&#x200B;**[!UICONTROL Read-Only]**&#x200B;位使用者共用一組特定的儀表板。 請勿為其複製一組儀表板。

## 其他許可權：帳單與技術 {#billingtech}

除了一般許可權層級之外，還有另外兩個使用者指定 — `Billing`和`Technical`。 這些指定應搭配一般許可權層級使用。

### 帳單

`Billing`個使用者有權存取帳單頁面，並可以變更付款資訊。 此外，Adobe也可能會聯絡他們以詢問帳單問題。

`Admin`使用者預設有權存取`Billing`標籤，但`Standard`使用者如果在他們的設定檔中選取`Billing`核取方塊，也可以取得存取權。

![帳單頁面](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical`使用者沒有任何特定許可權 — 此設定只會標示您組織內的技術連絡人。 Adobe可能會就技術問題聯絡這些使用者。

`Admin`使用者可以按一下&#x200B;**[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]**&#x200B;並按照提示操作，將使用者新增至其帳戶。 在[!DNL Commerce Intelligence]中建立使用者後，您邀請的幸運兒將會收到有關如何完成帳戶設定程式的電子郵件指示。

`Admins`可以隨時按一下&#x200B;**[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**&#x200B;來檢視其帳戶中的所有使用者。 此頁面會顯示使用者的許可權以及他們可以存取的量度和儀表板。
