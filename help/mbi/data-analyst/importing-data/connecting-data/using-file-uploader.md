---
title: 使用檔案上載程式
description: 瞭解如何將所有資料放入單個Data Warehouse。
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# 使用檔案上載程式

>[!NOTE]
>
>需要 [管理權限](../../../administrator/user-management/user-management.md)。

[!DNL Adobe Commerce Intelligence] 功能強大，不僅因為它的可視化功能，還因為它讓您能夠將所有資料放入一個Data Warehouse。 即使是位於資料庫和整合之外的資料，也可以納入 [!DNL Commerce Intelligence] 在「Data Warehouse管理器」中使用「檔案上載」工具。

以廣告市場活動為例。 如果您同時運行線上和離線市場活動，則如果您只分析線上整合中的資料，則無法獲得整幅圖景。 上傳包含離線市場活動資料的電子錶格允許您分析這兩組資料，並更深入地瞭解市場活動的表現。

## 限制和要求 {#require}

1. **檔案上載的唯一支援格式是 `CSV` 或`comma separated values`**。 如果在Excel中工作，則可以使用「另存為」功能將檔案保存到 `.csv` 的子菜單。
1. **`CSV`必須使用`UTF-8 encoding`**。 大多數時候，這不是問題。 如果上載檔案時遇到此錯誤， [查閱此支援文章](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html)。
1. **檔案不能大於100MB**。 如果檔案大於此值，請將表分成塊，並將它們另存為單個檔案。 可在載入初始檔案後追加資料。
1. **所有表必須具有`primary key`**。 表中至少需要有一列可用作 `primary key`或表中每行的唯一標識符。 指定為 `primary key` 能 *從不* 為空。 A `primary key` 可以簡單到添加給每行一個數字的列，也可以是連接為唯一值的列的列(例如， `campaign name` 和 `date`)。

   如果列（或列）被指定為唯一，但有重複行，則不導入重複行。

## 格式化資料以用於上載 {#formatting}

在將資料上載到 [!DNL Commerce Intelligence]，檢查是否根據本節中的指導原則設定格式。

### 標題行 {#header}

要確保正確標籤和導入列，請確保電子錶格的第一行是描述每列中資料的標題。

列名必須唯一，並且只包含字母、數字、空格和以下符號： `$ % # /`。 如果列名包含逗號，則在檔案上載時將分為兩列。 此外，Adobe還建議檔案中少於85列以優化更新速度。

### 帶逗號的資料 {#commas}

因為檔案必須在 `CSV` 格式化，使用逗號可能會導致上載資料時出現問題。 `CSV` 檔案使用逗號來指示新值，因此具有名稱(如 `Campaigns`。 `August` 讀為兩列(`Campaigns` 和 `August`)，而不是將所有資料移到一行上。 Adobe建議盡可能避免逗號。 您可以使用 `Data Preview` 查看更新完成後資料是否正確顯示。

### 日期

任何包含日期的資料集都必須使用 [標準日期格式](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` 或 `MM/DD/YYYY`。

### 特殊字元

某些特殊字元不被接受。 例如，管道符號 `& # 1 2 4` 解釋為建立列，並在上載檔案時導致錯誤。

### 小數

貨幣值應具有資料類型 `Decimal Number` ，並且這些列會自動捨入到Data Warehouse中的兩個小數位。 如果不想捨入小數或精度大於此值，應選擇 `Non-Currency Decimal Number` 資料類型。

### 百分比

百分比必須以小數輸入。 例如：

| **對：** | **錯誤：** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### 帶前導和/或尾隨零的值 {#zeroes}

檔案中的某些值（如郵遞區號和ID）可以以零開頭或結尾。 為確保正確保留和上載零，可更改格式類型(例如， [從數字到文本](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us))或強制數字格式。

使用 `US ZIP codes` 作為更改數字格式的示例。 在 [!DNL Excel]，突出顯示包含 `ZIP codes` 和 [更改數字格式](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) 至 `ZIP code`。 也可以選擇自定義數字格式， `Type` 輸入 `00000`。 請記住，如果某些代碼格式化為 `00000` 其他 `00000-0000`。

的 `Type` 可以 [格式不同，以適應其他資料類型](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us)，如ID。 如果 `ID` 長度為9位數，例如 `Type` 可能 `000000000` 或 `000-000-000`。 這會改變 `123456` 至 `000-123-456`。

對於 [!DNL Google Docs] 和 [!DNL Apple Numbers] 資源，請參閱 [相關](#related) 清單。

## 正在上載資料 {#uploading}

現在您的電子錶格格式正確， [!DNL Commerce Intelligence] — 友好，將其添加到Data Warehouse。

1. 要開始，請轉到 **[!UICONTROL Data** > **File Uploads]**。

1. 按一下 **[!UICONTROL Upload to New Table]** 頁籤。

1. 按一下 **[!UICONTROL Choose File]** 並選擇檔案。 按一下 **[!UICONTROL Open]** 開始上載。

   上載完成後，列的清單 [!DNL Commerce Intelligence] 在檔案中找到。

1. 檢查列名和資料類型是否正確。 具體來說，請檢查是否將任何日期列讀取為日期，而不是數字。

   >[!NOTE]
   >
   >的 `datatype` 很重要，所以不要跳過此步驟！

1. 選擇組成 `primary key` 複選框。

1. 命名表。

1. 按一下 **[!UICONTROL Save Table]**。

A *成功！* 保存表後，螢幕頂部將顯示消息。

如果需要視覺，請查看整個過程：

![](../../../assets/fileupload.gif)

上載的表顯示在 **檔案上載** Data Warehouse管理器中表清單的「所有表」和「已同步表」選項中的「」部分：

![](../../../assets/upload-tables.png)

## 更新資料或將資料附加到現有表 {#appending}

是否已獲取一些新資料以添加到已上載的檔案中？ 無問題 — 您可以輕鬆更新和追加資料 [!DNL Commerce Intelligence]。

1. 要開始，請轉到 **[!UICONTROL Manage Data** > **File Uploads]**。

1. 按一下 **[!UICONTROL Edit/Upload `.csv`到現有表]** 頁籤。

1. 在下拉清單中，按一下要更新或追加的表的名稱。

1. 使用下拉清單選擇處理重複行的選項：

   | 選項 | 說明 |
   |---|---|
   | `Overwrite old row with new row` | 如果行在現有表和新檔案中具有相同的主鍵，則此操作會用新資料覆蓋現有資料。 這是用於具有隨時間變化的值的列的方法，例如，「狀態」列。 現有資料將被覆蓋並用新資料更新。 主鍵不在現有表中的行將作為新行添加。 |
   | `Retain old row; discard new row` | 如果行與現有表和新檔案中的主鍵相同，則這將導致忽略新資料。 |
   | `Purge all existing rows first and ignore duplicate keys within the file` | 這將刪除任何現有資料，並用檔案中的新資料替換它。 僅當不需要現有表中的任何資料時，才使用此選項。 |

1. 按一下 **[!UICONTROL Choose File]** 並選擇檔案。

1. 按一下 **[!UICONTROL Open]** 開始上載。

   上載完成後， [!DNL Commerce Intelligence] 將驗證檔案中的資料結構。 A *成功！* 保存表後，螢幕頂部將顯示消息。

## 資料可用性 {#availability}

與計算列一樣，檔案上載的資料在下一個更新週期完成後可用。 如果在檔案上載期間正在進行更新，則在下次更新之後資料才可用。 完成更新週期後，您可以導航至 `Data Preview` 頁籤，以確保正確上載檔案並按預期顯示資料。

## 收尾 {#wrapup}

本主題僅介紹了使用導入資料的基本知識，但您可能希望執行更高級的操作。 請查看相關文章，以獲取有關格式化和導入金融、電子商務、廣告支出和其他類型資料的指導。

此外，檔案上載不是將資料 [!DNL Commerce Intelligence]。 的 [資料導入API](https://developer.adobe.com/commerce/services/reporting/import-api/) 函式允許您將任意資料推送到 [!DNL Commerce Intelligence] Data Warehouse。

## 相關 {#related}

* [格式化和導入財務資料](../../../best-practices/format-import-financial-data.md)
* [導入離線/其他廣告支出資料](../connecting-data/import-offline-ad-data.md)
* [預期[!DNL Google ECommerce] 資料](../integrations/google-ecommerce-data.md)

## 第三方資源

* [數字資料格式指南](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] 資料格式指南](https://support.google.com/docs/answer/56470?hl=en)
