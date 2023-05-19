---
title: 資料遷移服務
description: 瞭解提交請求並開始遷移所需的一切。
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 資料遷移

遷移到新的資料庫架構、伺服器或報告資料庫不必感到壓力。 的 [[!DNL Adobe] 服務團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 提供遷移幫助。

為確保過渡盡可能順利，在提交遷移請求時應盡可能詳細。 本主題包含您提交請求和開始遷移所需的一切內容。 為我們提供您需求的全面圖片，確保您的項目範圍正確且估計準確。

## 入門 {#started}

在開始之前，您必須瞭解以下問題的答案：

* **新資料庫是否位於新伺服器上？** 在提交請求之前，請在以下位置更新資料連接的設定 **[!UICONTROL Manage Data** > **Connections]**。 如果您需要複習如何執行此操作，請轉至 [`Integrations`](../integrations/integrations.md) ，並查找所使用的資料庫類型的說明。

* **您的所有歷史資料是否都存在於新資料庫中，或是需要遷移它？** 您可以在遷移過程中整合歷史資料和新資料。 即使您不需要整合，請在您的請求中告知我們。

在您對上述問題做出回答後，您需要瞭解遷移的類型。 新資料庫是否 [`same`](#sameschema) 架構，或者 [`different`](#newschema) 架構？ 在下面的討論中，您可以找到每種遷移類型的詳細說明。

## 遷移到具有相同架構的新資料庫 {#sameschema}

提交請求時，請讓我們知道資料庫架構沒有更改，並且已在中設定連接 [!DNL Adobe Commerce Intelligence]。

如果資料庫具有新名稱，請將其包含在請求中，以便可以正確遷移儀表板。

如果資料庫名稱未更改，則遷移完成。 下次完成完整更新後，儀表板和報表將刷新。

## 使用不同模式遷移到新資料庫 {#newschema}

>[!IMPORTANT]
>
>如果某些資料列在新資料庫中沒有相等的列，則某些分析可能會在進程中丟失。

要成功完成此類遷移，必須將現有資料列與新資料庫中的等效資料列相匹配。 這不是強制性的，但為我們執行匹配有助於加快您請求的週轉時間並降低遷移的價格。

如果您覺得自己可以進行匹配，請按照以下說明操作，並將完成的電子錶格附加到您的請求：

1. 查看當前同步到您的Data Warehouse的所有表和列(**[!UICONTROL Manage Data** > **Data Warehouse]**)。

1. 在電子錶格中，為每個要遷移到新資料庫的表建立一個頁籤。

1. 在每個頁籤中，為所有需要遷移的現有列建立一個列。 Adobe建議給它命名 `Existing column name`。

1. 您還需要為電子錶格的每個頁籤中的新資料庫中的列的等效項建立另一個列。 Adobe建議將列命名為類似 `New column name`。

1. 輸入現有列及其等效項。 如果現有列沒有新的等效項，請輸入 `N/A`。

   此外，如果有新方法計算新資料庫中的相同資訊，請在 [`New column name`] 的雙曲餘切值。

下面是一個示例：

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>如果某些資料列在新資料庫中沒有相等的列，則某些分析可能會在進程中丟失。

## 如何提交請求？ {#submitreq}

你可以通過 [提交支援請求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

如果按照上一節中的步驟建立列匹配電子錶格，請不要忘記附加它。

## 接下來呢？ {#wrapup}

確定項目範圍需要您與執行遷移的Commerce Services團隊的分析師進行一些協作。 更改的複雜性以及您和分析員的響應能力直接影響遷移所花費的時間。 在確定詳細資訊後，將建立時間表並將工作說明發送給您。
