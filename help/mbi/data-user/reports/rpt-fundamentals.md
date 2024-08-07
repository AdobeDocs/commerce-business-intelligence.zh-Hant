---
title: 使用報表
description: 瞭解如何使用您的報告資料。
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 使用報表

使用[!DNL Adobe Commerce Intelligence]中的報告協助您回答業務問題 — 您只是想要檢視本月與去年比較的收入，或是瞭解您最新[!DNL Google AdWords]行銷活動的贏取成本。

從問題到答案的路徑看起來是什麼樣子？

為了協助您視覺化此流程，該路由如下圖所示。 本主題說明如何處理分析問題，以及獲取所需資料所需的後端後勤工作。

## 從問題開始

您知道您經常提出問題來改善您的業務，從提高客戶滿意度到降低供應成本。 您專注於如何將您的問題轉換為可幫助您推動決策的分析。

在此範例中，假設您要回答以下問題：

* 我的新註冊者轉換速度有多快？

## 識別測量

是時候找出一份可能的分析和測量清單來回答這個問題了。 在此範例中，著重於下列量度：

* 從註冊到每次使用的首次購買日期的平均時間。

這會顯示註冊日期與使用者首次購買日期之間經過的平均時間，並讓您瞭解使用者在轉換漏斗中的這最後一個步驟中的行為。

## 尋找資料

瞭解要測量什麼只能讓我們瞭解其中的一部分。 若要評估每位使用者從註冊到首次購買日期的平均時間，您必須識別您測量所包含的所有資料點。

將您的測量劃分為核心元件。 您必須知道已註冊的人數、購買的人數，以及兩次事件之間經過的時間。

在更高的層級，您需要知道在資料庫中哪裡可以找到此資料，特別是：

* 此表格會在每次有人註冊時記錄一列資料
* 此表格會記錄每次有人購買時的資料列
* 可用來聯結或參考`purchase`資料表至`customer`資料表的資料行 — 這可讓我們知道誰進行了購買

在更精細的層級，您需要識別用於此分析的確切資料欄位：

* 包含客戶註冊日期的資料表和資料行：例如`user.created\_at`
* 包含購買日期的資料表和資料行：例如`order.created\_at`

## 建立資料欄以供分析

除了上述的原生資料欄以外，您還需要一組計算的資料欄位以啟用此分析，包括：

* `Customer's first purchase date`會傳回特定使用者的`MIN(order.created_at`)

然後會用來建立：

* `Time between a customer's registration date and first purchase date`，會傳回從註冊到首次購買之間經過的特定使用者時間。 這是您日後量度的基礎。

這兩個欄位都必須在使用者層級（例如，`user`資料表）建立。 這可讓使用者標準化平均分析（換言之，此平均計算中的分母是使用者計數）。

這是[!DNL Commerce Intelligence]步驟的所在位置！ 您可以使用您的[!DNL Commerce Intelligence]Data Warehouse來建立上述欄。 請聯絡Adobe分析團隊，向我們提供建立新欄的特定定義。 您也可以使用[資料行編輯器](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)。

最佳實務是避免直接在資料庫中建立這些計算資料欄位，因為這會給生產伺服器帶來不必要的負擔。

## 建立量度

現在您已具備分析所需的資料欄位，您可以開始尋找或建立相關量度，以建構您的分析。

您想要在此執行下列計算：


_[總和`Time between a customer's registration date and first purchase date`] / [註冊並購買的客戶總數]_

而且您想根據客戶的註冊日期，檢視這項計算在一段時間內的繪製或趨勢。 以下說明如何在[!DNL Commerce Intelligence]中[建立此量度](../../data-user/reports/ess-manage-data-metrics.md)：

1. 移至&#x200B;**[!UICONTROL Data]**&#x200B;並選取`Metrics`標籤。
1. 按一下&#x200B;**[!UICONTROL Add New Metric]**&#x200B;並選取`user`表格（您建立上述維度的位置）。
1. 從下拉式清單中，選取依`Customer's registration date`欄排序之`user`表格中`Time between a customer's registration date and first purchase date`欄的`Average`。
1. 新增任何相關的篩選器或篩選器集。

此量度現已準備就緒。

## 建立報告

設定好新量度後，您就可以依註冊日期來報告註冊與首次購買日期之間的平均時間。

只要移至任何儀表板，並使用上述建立的量度[建立報告](../../data-user/reports/ess-manage-data-metrics.md)即可。

### `Visual Report Builder` {#visualrb}

[以視覺化方式呈現您的資料時，`Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md)是最簡單的方式。 如果您不熟悉SQL或想要快速建立報表，最好選擇視覺Report Builder。 只要按幾下，您就能新增量度、劃分資料，以及在整個組織中建立報表。 此選項不需要任何技術專業知識，是初學者和專家的完美選擇。

|  |  |
|--- |--- |
| **這是最適合的……** | **這不太適合……** |
|  — 所有層級的分析/技術體驗<br> — 快速建立報告<br> — 建立分析以與其他使用者共用 |  — 需要SQL特定函式的分析<br> — 測試新資料行 — 計算資料行取決於初始資料母體的更新週期，而使用SQL建立的資料行則不然。 |

{style="table-layout:auto"}

### 報表說明和影像

#### 新增說明至報表

建立與您團隊其他成員共用的報告時，Adobe建議新增說明，讓其他使用者更能瞭解您的分析。

1. 按一下任何報告頂端的&#x200B;**[!UICONTROL i]**。
1. 在文字方塊中輸入說明。
1. 按一下&#x200B;**[!UICONTROL Save Description]**。

請參閱下文：

![圖表說明](../../assets/Chart_Description.gif)

#### 將報表匯出為影像

需要在簡報或檔案中包含報告？ 使用每個報表右上角的`Report Options`功能表，可將任何報表儲存為影像(PNG、PDF或SVG格式)。

1. 按一下任何報表右上角的齒輪圖示。
1. 從下拉式清單中選取`Enlarge`。
1. 當報告放大時，按一下報告右上角的&#x200B;**[!UICONTROL Download]**。
1. 從下拉式清單中選取偏好的影像格式。 下載會立即開始。

請參閱下文：

![](../../assets/exp-rep-as-image.gif)
