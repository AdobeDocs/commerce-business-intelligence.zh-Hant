---
title: 資料移轉服務
description: 瞭解提交請求並開始移轉所需的一切。
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 資料移轉

移轉至新的資料庫結構描述、伺服器或報告資料庫並不一定會有壓力。 此 [[!DNL Adobe] 服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 提供移轉協助。

為確保轉換儘可能順暢，提交移轉請求時請務必儘可能詳細說明。 本主題提供提交請求並開始移轉所需的一切。 提供您需求的全面資訊，確保您的專案範圍設定正確，而且估計準確。

## 快速入門 {#started}

開始之前，您必須知道下列問題的答案：

* **新資料庫是在新伺服器上嗎？** 在提交請求之前，請更新下方的資料連線設定 **[!UICONTROL Manage Data** > **Connections]**. 如果您需要有關如何執行此動作的複習程式，請前往 [`Integrations`](../integrations/integrations.md) 區段，並尋找您使用之資料庫型別的指示。

* **您所有的歷史資料都存在於新資料庫中嗎？還是需要移轉這些資料？** 您可以在移轉過程中合併歷史資料與新資料。 即使您不需要合併，請在您的請求中告知我們。

取得上述答案後，您需瞭解移轉型別。 新資料庫是否會 [`same`](#sameschema) 結構描述，或它是否有 [`different`](#newschema) 綱要？ 在下列討論中，您會找到每種移轉型別的詳細說明。

## 移轉至具有相同結構描述的新資料庫 {#sameschema}

送出要求時，請告知我們資料庫結構並未變更，而且連線已設定於 [!DNL Adobe Commerce Intelligence].

如果資料庫有新名稱，請將其納入請求中，以便您的儀表板可以正確移轉。

如果資料庫名稱未變更，則移轉完成。 在下次完整更新完成後，儀表板和報表將重新整理。

## 移轉至具有不同結構描述的新資料庫 {#newschema}

>[!IMPORTANT]
>
>如果某些資料欄在新資料庫中沒有對等欄，則某些分析可能會在此過程中遺失。

若要成功完成這類移轉，現有資料欄必須與新資料庫中的對應資料欄相符。 這不是強制性的，但是對我們執行比對有助於加快請求的返回時間，並降低移轉的成本。

如果您覺得可以自行比對，請依照下列指示，將完成的試算表附加至您的請求：

1. 檢閱目前同步處理至Data Warehouse的所有表格和欄(**[!UICONTROL Manage Data** > **Data Warehouse]**)。

1. 在試算表中，為每個要移轉至新資料庫的表格建立一個標籤。

1. 在每個索引標籤中，為需要移轉的所有現有欄建立一個欄。 Adobe建議將其命名如下 `Existing column name`.

1. 您還需要在試算表的每個索引標籤中，為新資料庫中的欄對應內容建立另一個欄。 Adobe建議將欄命名如下 `New column name`.

1. 輸入現有欄及其對應欄。 如果現有欄沒有新的對等專案，請輸入 `N/A`.

   此外，如果有新方法可計算新資料庫中的相同資訊，請在 [`New column name`] 欄。

以下是範例說明：

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>如果某些資料欄在新資料庫中沒有對等欄，則某些分析可能會在此過程中遺失。

## 如何提交請求？ {#submitreq}

您可以透過以下方式聯絡我們 [提交支援要求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

如果您依照上一節中的步驟建立欄位比對試算表，別忘了附加試算表。

## 接下來呢？ {#wrapup}

確定專案的範圍時，需要您和執行移轉的商務服務團隊分析師之間的一些共同作業。 變更的複雜度以及您與分析人員的回應能力，會直接影響移轉所需的時間。 當您確定了詳細資訊後，就會建立時間表，並傳送給您一份工作宣告。
