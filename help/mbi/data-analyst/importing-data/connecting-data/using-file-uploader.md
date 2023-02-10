---
title: 使用檔案上傳程式
description: 了解如何將所有資料放入單一資料倉庫。
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# 使用檔案上傳程式

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md).

[!DNL MBI] 功能強大，不僅是因為其視覺效果功能，還因為它可讓您將所有資料放入單一資料倉庫。 即使是存放在資料庫外部的資料和整合，也可以帶入 [!DNL MBI] 使用「Data Warehouse管理員」中的「檔案上傳」工具。

讓我們以廣告促銷活動為例。 如果您同時執行線上和離線行銷活動，如果您只分析線上整合的資料，則無法獲得整張圖片。 上傳含有離線促銷活動資料的試算表，可讓您分析這兩組資料，並更健全地了解您的促銷活動績效。

## 限制和要求 {#require}

1. **檔案上傳唯一支援的格式是 `CSV` 或`comma separated values`**. 如果您使用Excel，則可使用「另存新檔」功能，將檔案儲存於 `.csv` 格式。
1. **`CSV`檔案必須使用`UTF-8 encoding`**. 大多數情況下，這不會是問題。 如果您在上傳檔案時遇到此錯誤， [請參閱本支援文章](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=en).
1. **檔案不能大於100MB**. 如果檔案大於此，請將表分割為塊，並將它們另存為單個檔案。 您可以在載入初始檔案後使用附加資料。
1. **所有表必須具有`primary key`**. 表格中至少必須有一欄可作為 `primary key`，或表格中每一列的唯一識別碼。 任何指定為 `primary key` can *從不* 為null。 A `primary key` 可以像新增為每列指定數字的欄一樣簡單，或可以串連兩個欄來建立唯一值的欄(例如 `campaign name` 和 `date`)。

   如果欄（或欄）指定為唯一，但有重複項目，則不會匯入重複列。

## 格式化上傳資料 {#formatting}

將資料上傳至 [!DNL MBI]，檢查其格式是否根據本節中的准則。

### 標題列 {#header}

為確保欄已正確標示及匯入，請確定試算表的第一列是說明各欄資料的標題。

列名必須是唯一的，並且只包含字母、數字、空格和以下符號： `$ % # /`. 如果列名包含逗號，則在檔案上載時，它將被拆分為兩列。 此外，我們建議檔案中少於85欄，以最佳化更新速度。

### 含逗號的資料 {#commas}

因為檔案必須在 `CSV` 格式，使用逗號可能會造成上傳資料的問題。 `CSV` 檔案使用逗號來表示新值，因此，列的名稱如 `Campaigns`, `August` 會讀為兩欄(`Campaigns` 和 `August`)，而不是一列，將所有資料移至一列。 建議盡可能避免逗號。 您可以使用 `Data Preview` 以查看更新完成後，資料是否正確顯示。

### 日期

任何包含日期的資料集都必須使用 [標準日期格式](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` 或 `MM/DD/YYYY`.

### 特殊字元

部分特殊字元不接受。 例如，管道符號 `& # 1 2 4` 會解譯為建立新欄，且會在上傳檔案時造成錯誤。

### 小數位數

貨幣值應具有資料類型 `Decimal Number` ，則這些欄會自動四捨五入到資料倉庫中的兩位小數。 如果您不想四捨五入小數或精確度大於此，則應選取 `Non-Currency Decimal Number` 資料類型。

### 百分比

百分比必須輸入為小數。 例如：

| **對：** | **錯誤：** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style=&quot;table-layout:auto&quot;}

### 開頭為和/或結尾為零的值 {#zeroes}

您檔案中的某些值（例如郵遞區號和ID）可能會以零開頭或結尾。 若要確保正確保留和上傳零，您可以變更格式類型(例如 [從數字到文本](https://support.office.com/en-US/article/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4))或強制數字格式。

讓我們使用 `US ZIP codes` 以示如何更改數字格式。 在 [!DNL Excel]，反白標示包含 `ZIP codes` 和 [更改數字格式](https://support.office.com/en-za/article/Display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d) to `ZIP code`. 您也可以選取自訂數字格式，並在 `Type` 窗口，輸入 `00000`. 請記住，如果某些程式碼的格式為 `00000` 而其他 `00000-0000`.

此 `Type` 可以 [格式不同以適應其他資料類型](https://support.office.com/en-us/article/Keep-leading-zeros-in-number-codes-1bf7b935-36e1-4985-842f-5dfa51f85fe7?CorrelationId=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-US&amp;rs=en-US&amp;ad=US)，例如ID。 若 `ID` 是九位數，例如 `Type` 可以 `000000000` 或 `000-000-000`. 這會改變 `123456` to `000-123-456`.

針對 [!DNL Google Docs] 和 [!DNL Apple Numbers] 資源，請參閱 [相關](#related) 清單。

## 上傳資料 {#uploading}

試算表格格式正確，且 [!DNL MBI]友好，讓我們將其新增至您的資料倉庫。

1. 若要開始，請前往 **[!UICONTROL Data** > **File Uploads]**.

1. 按一下 **[!UICONTROL Upload to New Table]** 標籤。

1. 按一下 **[!UICONTROL Choose File]** 並選取檔案。 按一下 **[!UICONTROL Open]** 以開始上傳。

   上傳完成後，您會看到欄清單 [!DNL MBI] 在檔案中找到。

1. 檢查欄名稱和資料類型是否正確。 具體來說，請檢查任何日期欄是否讀取為日期，而非數字。

   >[!NOTE]
   >
   >此 `datatype` 非常重要，因此請勿跳過此步驟。

1. 選取將組成 `primary key` 使用索引鍵圖示下方的核取方塊，以取得表格。

1. 為表命名。

1. 按一下 **[!UICONTROL Save Table]**.

A *成功！* 儲存表格後，畫面頂端會顯示訊息。

如果您需要視覺化，以下是整個程式的概況：

![](../../../assets/fileupload.gif)

上傳的表格會顯示在 **檔案上傳** 「Data Warehouse管理器」中的「所有表」和「同步表」選項中的「表」部分：

![](../../../assets/upload-tables.png)

## 更新或附加資料至現有表格 {#appending}

有新資料要添加到已上載的檔案中嗎？ 無問題 — 您可以輕鬆更新和附加資料 [!DNL MBI].

1. 若要開始，請前往 **[!UICONTROL Manage Data** > **File Uploads]**.

1. 按一下 **[!UICONTROL Edit/Upload `.csv`到現有表]** 標籤。

1. 在下拉式清單中，按一下您要更新或附加的表格名稱。

1. 使用下拉式清單來選取處理重複列的選項：

   |  |  |
   |---|---|
   | `Overwrite old row with new row` | 如果現有表格和新檔案中的一列具有相同的主鍵，則這會以新資料覆寫現有資料。 這是用於值隨時間變化的欄的方法，例如狀態欄。 現有資料將被覆寫，並以新資料更新。 現有表格中沒有主鍵的行將作為新行添加。 |
   | `Retain old row; discard new row` | 如果現有表和新檔案中的行具有相同的主鍵，則這會導致忽略新資料。 |
   | `Purge all existing rows first and ignore duplicate keys within the file` | 這會刪除任何現有資料，並以檔案中的新資料取代。 只有在不需要現有表格中的任何資料時，才應使用此選項。 |

1. 按一下 **[!UICONTROL Choose File]** 並選取檔案。

1. 按一下 **[!UICONTROL Open]** 以開始上傳。

   上傳完成後， [!DNL MBI] 會驗證檔案中的資料結構。 A *成功！* 儲存表格後，畫面頂端會顯示訊息。

## 資料可用性 {#availability}

就像計算的欄一樣，檔案上傳的資料也會在下一個更新週期完成後提供使用。 如果檔案上傳期間進行了更新，則資料要等到下次更新後才能使用。 完成更新週期後，您可以導覽至 `Data Preview` 標籤，確保檔案已正確上傳，且資料可如預期顯示。

## 包裝 {#wrapup}

本文僅介紹使用匯入資料的基本知識，但我們打賭您想做一些更進階的工作。 請參閱相關文章，以取得有關金融、電子商務、廣告支出和其他類型資料的格式和匯入的指引。

此外，檔案上傳並非將資料傳入 [!DNL MBI]. 此 [資料匯入API](https://developer.adobe.com/commerce/services/reporting/import-api/) 函式可讓您將任意資料推送至 [!DNL MBI] 資料倉庫。

## 相關 {#related}

* [格式化和導入財務資料](../../../best-practices/format-import-financial-data.md)
* [離線匯入/其他廣告支出資料](../connecting-data/import-offline-ad-data.md)
* [預期[!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)

## 第三方資源

* [數字資料格式指南](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] 資料格式指南](https://support.google.com/docs/answer/56470?hl=en)
