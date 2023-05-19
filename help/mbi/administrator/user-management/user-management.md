---
title: 管理Adobe Commerce用戶和權限
description: 瞭解如何管理Commerce Intelligence用戶。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 管理用戶權限

[!DNL Adobe Commerce Intelligence] 意在成為整個組織內唯一的真相來源。 每個用戶都有自己的儀表板集，他們可以 [與其他用戶共用](../../data-user/dashboards/share-dashboard-with-users.md)。

## 用戶權限級別

在 [!DNL Commerce Intelligence]，有三個一般權限級別，這些級別適用於建立帳戶時選擇的用戶：

* `Admin`
* `Standard`
* `Read-Only`

這些權限使用戶能夠執行某些操作或訪問 [!DNL Commerce Intelligence]。 下面是每個權限級別可以執行的操作的表 [!DNL Commerce Intelligence]:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **建立/管理用戶** | ✔ |  |  |
| **建立電子郵件摘要** | ✔ | ✔ |  |
| **建立/編輯/共用儀表板** | ✔ | ✔ |  |
| **查看儀表板** | ✔ | ✔ | ✔ |
| **建立/編輯/刪除可視報告** | ✔ | ✔* |  |
| **建立/編輯/刪除SQL報告** | ✔ |  |  |
| **克隆儀表板** | ✔ |  |  |
| **添加/管理整合** | ✔ |  |  |
| **訪問Data Warehouse管理器** | ✔ |  |  |
| **同步/取消同步表和列** | ✔ |  |  |
| **建立/編輯度量** | ✔ |  |  |
| **建立/編輯篩選器集** | ✔ |  |  |
| **建立/編輯計算列** | ✔ |  |  |
| **建立從屬報表清單** | ✔ |  |  |
| **訪問系統摘要** | ✔ |  |  |
| **訪問時區設定** | ✔ |  |  |
| **訪問計費** | ✔ | ✔** |  |
| **聯繫支援** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_您可以限制&#x200B;**[!UICONTROL Standard]**用戶 [訪問特定度量](../../administrator/user-management/restrict-metric-access.md)。_
>
>**[!UICONTROL Standard] _用戶可以使用額外權限設定訪問計費。_
>
>**[!UICONTROL Read-Only]** 用戶只能 _視圖_ 與他們共用的儀表板；不能建立或編輯任何 [!DNL Commerce Intelligence]，他們也不能搜索新儀表板並將其添加到帳戶。 Adobe建議您與 **[!UICONTROL Read-Only]** 您或您團隊的其他成員維護的用戶。 不要為其克隆一組儀表板。

## 其他權限：計費和技術 {#billingtech}

除了一般權限級別，還存在另外兩個用戶指定 —  `Billing` 和 `Technical`。 這些指定應與一般權限級別一起使用。

### 計費

`Billing` 用戶有權訪問計費頁並可以更改付款資訊。 此外，Adobe也可以聯繫他們，瞭解帳單問題。

`Admin` 用戶有權訪問 `Billing` ，但 `Standard` 如果用戶擁有 `Billing` 複選框。

![計費](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` 用戶沒有任何特定權限 — 此設定僅標籤您組織內的技術聯繫人。 Adobe可以聯繫這些用戶以瞭解技術問題。

`Admin` 用戶可以通過按一下 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** 並按提示操作。 建立用戶後 [!DNL Commerce Intelligence]，您邀請的幸運者將收到有關如何完成帳戶設定過程的電子郵件說明。

隨時， `Admins` 可以通過按一下 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**。 此頁顯示用戶的權限以及他們可以訪問的度量和儀表板。
