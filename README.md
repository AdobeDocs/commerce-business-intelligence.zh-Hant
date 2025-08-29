---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Adobe Commerce Intelligence技術檔案

我們歡迎社群以及檔案團隊以外的Adobe員工出力貢獻。

## Adobe Open Source行為準則

本專案已採用 [Adobe 開放原始碼管理辦法](code-of-conduct.md)或 [.NET Foundation 管理辦法](https://dotnetfoundation.org/code-of-conduct)。如需詳細資訊，請參閱[貢獻](contributing.md)一文。

## 關於您對Adobe內容的貢獻

請參閱[Adobe檔案投稿人指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hant)。

貢獻方式取決於您的身分和您要貢獻的變更型別：

### 微幅變更

如果您要提出微幅更新，請瀏覽文章，然後按一下文章底部的意見區域，按一下&#x200B;**詳細的意見選項**，然後按一下&#x200B;**建議編輯**，即可前往GitHub的Markdown來源檔案。 使用GitHub UI進行更新。 如需詳細資訊，請參閱一般[Adobe檔案投稿人指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hant)。

您在本存放庫為檔案和程式碼範例提交的小幅更正或釐清均包含在Adobe使用條款中。

### 來自社群成員的重大變更或新文章

如果您是Adobe社群的一分子，且想建立新文章或提交重大變更，請使用Git存放庫中的「問題」索引標籤，提交問題以便與檔案團隊開始對話。 一旦您同意了計畫，就需要與員工合作，透過結合公共和私有存放庫的工作來幫助引入新內容。

### 來自Adobe員工的重大變更

若您是Adobe Experience Cloud解決方案產品團隊的技術撰寫人員、專案經理或開發人員，且您的工作正是貢獻或撰寫技術文章，請使用`https://git.corp.adobe.com/AdobeDocs`的私人存放庫。

## 工具與設定

社群投稿人可以使用GitHub UI進行基本編輯或建立存放庫復本，以做出重大貢獻。

如需詳細資訊，請參閱[Adobe檔案貢獻者指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hant)。

## 如何使用Markdown將主題格式化

此存放庫中的所有文章皆使用GitHub Flavored Markdown。 如果您不熟悉Markdown，請參閱：

- [Markdown基本介紹](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [可列印的Markdown速查表](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## 影像最佳化的預先提交鉤點

此存放庫包括自動預先提交掛接，可在提交前最佳化影像。 **所有貢獻者都應該啟用這些鉤點**，以確保一致的影像最佳化並降低存放庫大小。

### 快速設定

複製存放庫後，請執行：

```bash
.githooks/setup-hooks.sh
```

### 鉤子會做什麼

- 自動偵測分階段影像檔案(PNG、JPG、JPEG、GIF、SVG)
- 執行`image_optim`以壓縮和最佳化影像
- 自動重新存放最佳化的影像
- 確保所有認可的影像都已適當最佳化

### 優點

- 縮小存放庫大小
- 加速說明檔案的頁面載入
- 所有貢獻者的影像品質一致
- 不需要手動最佳化

如需詳細的設定指示、疑難排解和組態，請參閱[`.githooks/README.md`](.githooks/README.md)。
