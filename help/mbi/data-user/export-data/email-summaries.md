---
title: 建立自動化的電子郵件摘要
description: 瞭解如何建立自動化的電子郵件摘要。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 建立自動化的電子郵件摘要

電子郵件摘要是強大的溝通工具，可用來與關鍵利害關係人分享您的業務的狀態和趨勢。 透過電子郵件摘要，您可以：

* 以電子郵件傳送包含報告的圖形摘要
* 納入或排除電子郵件摘要作者，以停止接收電子郵件
* 排程電子郵件傳送時間
* 編輯、刪除和暫停現有的排程電子郵件摘要

## 建立新的電子郵件摘要

1. 在側邊欄中按一下&#x200B;**[!DNL Manage Data]**，然後再按&#x200B;**[!UICONTROL Email Summary]**。

   如果您是第一次建立電子郵件摘要，此頁面不會顯示任何已儲存的摘要。

1. 按一下右上角的&#x200B;**[!UICONTROL Create New Email Summary]**。

1. 輸入摘要的名稱。

   選擇傳達摘要中所包含內容的名稱。 例如，`AOV Comparison`。

1. 在`Choose Content`區段中，選取您要包含在摘要中的報告。

   您最多可以選取十個您擁有的報表。 選取報表後，使用顯示的圖示來選取是否要以表格或圖表形式傳送該報表。 如果以數字儲存報表，則只能以數字傳送。 如需傳送包含過時資料之報告的電子郵件摘要的相關資訊，請參閱[管理您的帳戶設定](../../administrator/account-management/managing-account-settings.md)。

   >[!NOTE]
   >
   >`Cohort`報告僅在您使用新架構時可用。

1. （選擇性）若要接收電子郵件，請選取`Send Email To Me`。

1. 若要在電子郵件中加入其他使用者，請在`Add Email Recipients`欄位中輸入其電子郵件地址，並以逗號、空格、定位字元或分號分隔。

## 排程電子郵件摘要

在`Set when to send the Email Summary`欄位中，您可以指定何時傳送電子郵件摘要。 選項包括：

* `Manual`
* `Once`
* `Repeating`

### 儲存電子郵件摘要以供稍後傳送

1. 從`Set when to send the Email Summary`欄位中選取`Manual`。

1. 按一下&#x200B;**[!UICONTROL Save]**。

   這會將摘要儲存到電子郵件摘要清單中。

1. 當您準備好傳送摘要時，請按一下齒輪圖示並選取`Send Now`。

### 傳送電子郵件摘要一次

1. 從`Set when to send the Email Summary`欄位中選取`Once`。

1. 在`Select Start Date`行事曆中指定開始日期。

1. 在`Select time to send`欄位中指定傳送電子郵件的時間。

### 建立重複排程

1. 從`Set when to send the Email Summary`欄位中選取`Repeating`。

1. 在`Set Frequency`欄位中，選取`Daily`、`Weekly`或`Monthly`。

1. 在`Select Start Date`行事曆中指定開始日期。

1. 在`Select time to send`欄位中指定傳送電子郵件的時間。

1. （選擇性）若要指定結束日期，請選取`End Date`並從行事曆中選取結束日期。

## 修改現有的電子郵件摘要

在您建立並儲存電子郵件摘要後，`Email Summaries`頁面會顯示所有已儲存摘要的清單。 您可以展開每一列(`+`)以取得詳細資訊。 此檢視中的欄為：

* `Email Name` — 電子郵件摘要的名稱
* `Content` — 摘要中的內容型別，例如任何報告的名稱。 如需傳送包含過時資料之報告的電子郵件摘要的相關資訊，請參閱[管理您的帳戶設定](../../administrator/account-management/managing-account-settings.md)。
* `Scheduled` — 傳送電子郵件摘要的頻率、日期和時間
* `Recipients` — 電子郵件摘要的收件者
* `Created Date` — 建立電子郵件摘要的日期
* `Status` - `Paused`或`Active`

按一下每列右側的齒輪圖示以：

* `Send Now` — 立即傳送電子郵件摘要給所有指定的收件者
* `Edit` — 可讓您修改電子郵件摘要的詳細資料
* `Pause/Active` — 可讓您根據設定方式，暫停傳送電子郵件摘要或啟用摘要
* `Delete` — 刪除電子郵件摘要
