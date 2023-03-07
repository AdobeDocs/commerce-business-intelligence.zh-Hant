---
title: 建立自動電子郵件摘要
description: 了解如何建立自動化電子郵件摘要。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 建立自動電子郵件摘要

電子郵件摘要是功能強大的通訊工具，可用來與主要利害關係人分享您的業務狀態和趨勢。 使用電子郵件摘要，您可以：

* 包含報表的電子郵件圖形摘要
* 納入或排除電子郵件摘要作者不接收電子郵件
* 排程電子郵件的傳送時間
* 編輯、刪除和暫停現有的已排程電子郵件摘要

## 建立新電子郵件摘要

1. 按一下 **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** 欄。

   如果這是您第一次建立電子郵件摘要，則此頁面不會顯示任何儲存的摘要。

1. 按一下 **[!UICONTROL Create New Email Summary]** 在右上角。

1. 輸入摘要的名稱。

   選擇傳達摘要中所包含內容的名稱。 例如， `AOV Comparison`.

1. 在 `Choose Content` 區段，選擇要包含在摘要中的報表。

   您最多可以選取10個您擁有的報表。 選取報表後，請使用顯示的圖示來選取您要將該報表以表格或圖表傳送。 如果您將報表儲存為數字，則只能以數字傳送。 如需傳送包含含有過時資料之報表之電子郵件摘要的相關資訊，請參閱 [管理您的帳戶設定](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` 只有在您使用新架構時，才可使用報表。

1. （選用）選取 `Send Email To Me` 如果您想要收到電子郵件。

1. 若要將其他使用者納入電子郵件，請在 `Add Email Recipients` 欄位以逗號、空格、制表符或分號分隔。

## 排程電子郵件摘要

在 `Set when to send the Email Summary` 欄位中，您可以指定傳送電子郵件摘要的時間。 選項包括：

* `Manual`
* `Once`
* `Repeating`

### 儲存要在稍後傳送的電子郵件摘要

1. 選擇 `Manual` 從 `Set when to send the Email Summary` 欄位。

1. 按一下 **[!UICONTROL Save]**.

   這會將摘要儲存至電子郵件摘要清單。

1. 準備好傳送摘要時，按一下齒輪圖示並選取 `Send Now`.

### 傳送電子郵件摘要一次

1. 選擇 `Once` 從 `Set when to send the Email Summary` 欄位。

1. 在 `Select Start Date` 日曆。

1. 指定在 `Select time to send` 欄位。

### 建立重複調度

1. 選擇 `Repeating` 從 `Set when to send the Email Summary` 欄位。

1. 在 `Set Frequency` 欄位，選擇 `Daily`, `Weekly`，或 `Monthly`.

1. 在 `Select Start Date` 日曆。

1. 指定在 `Select time to send` 欄位。

1. （可選）若要指定結束日期，請選取 `End Date` 並從日曆中選取結束日期。

## 修改現有電子郵件摘要

建立並儲存電子郵件摘要後， `Email Summaries` 頁面顯示所有已儲存摘要的清單。 您可以展開(`+`)，以取得詳細資訊。 此檢視中的欄為：

* `Email Name`  — 電子郵件摘要的名稱
* `Content`  — 摘要內的內容類型，例如任何報表的名稱。 如需傳送包含含有過時資料之報表之電子郵件摘要的相關資訊，請參閱 [管理您的帳戶設定](../../administrator/account-management/managing-account-settings.md).
* `Scheduled`  — 電子郵件摘要的傳送頻率、日期和時間
* `Recipients`  — 電子郵件摘要的收件者
* `Created Date`  — 建立電子郵件摘要的日期
* `Status` - `Paused` 或 `Active`

按一下每列右側的齒輪圖示，以：

* `Send Now`  — 立即向所有指定的收件人發送電子郵件摘要
* `Edit`  — 可讓您修改電子郵件摘要的詳細資訊
* `Pause/Active`  — 可讓您暫停傳送電子郵件摘要，或根據其設定方式啟用摘要
* `Delete`  — 刪除電子郵件摘要
