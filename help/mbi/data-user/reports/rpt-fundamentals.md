---
title: 使用報表
description: 了解如何使用您的報表資料。
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# 使用報表

在中使用報表 [!DNL MBI] 幫助您回答業務問題 — 無論您只想了解本月的收入與去年相比，還是了解您最新的收購成本 [!DNL Google AdWords] 行銷活動。

從問題到答案的路究竟是什麼？

為協助您具體了解此程式，該路由會在下方對應。 本主題同時說明您處理分析問題的方式，以及取得所需資料所需的後端物流。

## 從問題開始

您知道，您不斷提出問題以改進您的業務，從提高客戶滿意度到降低供應成本。 您專注於如何將您的問題翻譯成分析，協助您做出決策。

在此範例中，假設您要回答下列問題：

* 我的新註冊者轉換的速度如何？

## 識別測量

現在應該確定一份可能的分析和測量清單，以幫助回答這個問題。 在此範例中，請著重於下列量度：

* 每次使用從註冊到首次購買日期的平均時間。

這會顯示註冊日期與使用者首次購買日期之間的平均時間，並說明使用者在轉換漏斗的最後一個步驟的行為方式。

## 尋找資料

了解要衡量的只能讓我們了解。 若要評估每位使用者從註冊到首次購買日期的平均時間，您必須識別測量所包含的所有資料點。

將測量劃分為核心元件。 您必須知道已註冊的人數、購買的人數，以及這兩個事件之間經過的時間。

在更高的級別，您需要知道在資料庫中查找此資料的位置，具體是：

* 每次有人註冊時記錄一列資料的表格
* 記錄每次有人購買時的資料列的表格
* 可用於連接或引用 `purchase` 表格 `customer` 表格 — 這可讓我們了解購買者

在更精細的層級，您需要識別用於此分析的確切資料欄位：

* 包含客戶註冊日期的資料表和列：例如 `user.created\_at`
* 包含購買日期的資料表和列：例如 `order.created\_at`

## 建立資料欄以進行分析

除了上述的原生資料欄之外，您還需要一組計算資料欄位以啟用此分析，包括：

* `Customer's first purchase date` 會傳回特定使用者的 `MIN(order.created_at`)

接著，系統會使用以建立：

* `Time between a customer's registration date and first purchase date`，這會傳回特定使用者在註冊和首次購買之間經過的時間。 這是之後量度的基礎。

這兩個欄位都需在使用者層級建立(例如 `user` 表格)。 這可讓使用者標準化平均分析（換句話說，此平均計算中的分母是使用者計數）。

這是 [!DNL MBI] 進去！ 您可以使用 [!DNL MBI] Data Warehouse建立上述欄。 請聯絡Adobe分析團隊，為我們提供您建立新欄的特定定義。 您也可以使用 [欄編輯器](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

建議您避免直接在資料庫中建立這些計算的資料欄位，因為這會對生產伺服器造成不必要的負擔。

## 建立量度

現在您有分析所需的資料欄位了，您可以尋找或建立相關量度來建構分析。

您想在此執行下列計算：


_[總和 `Time between a customer's registration date and first purchase date`] / [註冊和購買的客戶總數]_

您想看看這個計算圖，根據客戶的註冊日期，隨時間或趨勢繪製。 下面是如何 [建立此量度](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL MBI]:

1. 前往 **[!UICONTROL Data]** ，然後選取 `Metrics` 標籤。
1. 按一下 **[!UICONTROL Add New Metric]** ，然後選取 `user` 表格（您在此建立上述維度）。
1. 從下拉式清單中，選取 `Average` 在`Time between a customer's registration date and first purchase date` 欄中 `user` 表按順序排列 `Customer's registration date`  欄。
1. 新增任何相關的篩選器或篩選器集。

此量度現已準備就緒。

## 建立報表

設定新量度後，您就可以用它來報告依註冊日期的註冊與首次購買日期之間的平均時間。

只需前往任何控制面板，然後 [建立報表](../../data-user/reports/ess-manage-data-metrics.md) 使用上述建立的量度。

### `Visual Report Builder` {#visualrb}

[此 `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) 是視覺化資料的最簡單方式。 如果您不熟悉SQL或想要快速建立報表，最好選擇可視化Report Builder。 只需按幾下，您就可以在整個組織中新增量度、劃分資料，以及建立報表。 這個選項無論是初學者還是專家都是最合適的，因為它不需要任何技術專長。

|  |  |
|--- |--- |
| **這是最好的……** | **這對……** |
|  — 所有層級的分析/技術體驗<br> — 快速建立報表<br> — 建立分析以與其他用戶共用 |  — 需要SQL特定函式的分析<br> — 測試新列 — 計算列取決於初始資料母體的更新週期，而使用SQL建立的列則否。 |

{style="table-layout:auto"}

### 報表說明和影像

#### 新增說明至報表

建立與團隊其他成員共用的報表時，Adobe建議您新增說明，讓其他使用者能更清楚了解您的分析。

1. 按一下 **[!UICONTROL i]** 的上方。
1. 在單詞框中輸入說明。
1. 按一下 **[!UICONTROL Save Description]**.

請參閱下列內容：

![圖表說明](../../assets/Chart_Description.gif)

#### 將報表匯出為影像

需要在演示文稿或文檔中包含報告嗎？ 任何報表都可以儲存為影像(以PNG、PDF或SVG格式)，使用 `Report Options` 功能表，位於每個報表的右上角。

1. 按一下任何報表右上角的齒輪圖示。
1. 從下拉式清單中，選取 `Enlarge`.
1. 當報告放大時，按一下 **[!UICONTROL Download]** 在報表的右上角。
1. 從下拉式清單中選取偏好的影像格式。 下載會立即開始。

請參閱下列內容：

![](../../assets/exp-rep-as-image.gif)
