---
title: SSH主機金鑰驗證
description: 瞭解Commerce Intelligence如何註冊SSH主機金鑰、如何重新整理金鑰、疑難排解錯誤，以及何時應聯絡SSH通道連線支援。
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# SSH主機金鑰驗證 {#ssh-host-keys}

[!DNL Commerce Intelligence]對加密的（SSH通道）資料庫連線使用嚴格的SSH主機金鑰驗證，包括[MySQL](mysql-via-ssh-tunnel.md)、[MongoDB](mongodb-via-ssh-tunnel.md)和[PostgreSQL](postgresql.md)。

在&#x200B;**[!UICONTROL Save & Test]**&#x200B;期間，系統會為您連線註冊SSH堡壘主機金鑰，並在每個連線中安全地儲存這些金鑰。 註冊之後，只有當即時堡壘主機金鑰與已註冊的金鑰相符時，複製和通道傳送才會成功。

此模型可封鎖中間人攻擊及非預期的主機變更，進而提高安全性。 這也表示主機金鑰輪換、缺少信任資料或基礎架構變更可能會出現在連線上，作為SSH主機金鑰錯誤，而不是一般的通道失敗。

>[!NOTE]
>
>**管理員**&#x200B;是指擁有您[!DNL Commerce Intelligence]帳戶之管理員許可權的使用者，除非另有說明，否則不是您的Adobe組織主控台。 只有管理員可以執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 如果您沒有看到此控制項，請要求您帳戶上的管理員執行重新整理，或聯絡Adobe支援。

您沒有編輯、上傳或管理`known_hosts`個檔案。 在指派給您帳戶的Adobe基礎結構上註冊並重新整理。

>[!IMPORTANT]
>
>主機金鑰輪換需要管理員才能執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 如果堡壘主機金鑰已變更，或堡壘身分已變更（主機名稱、IP或連線埠），再次執行&#x200B;**[!UICONTROL Save & Test]**&#x200B;或重新儲存連線不會更新已註冊的金鑰。 連線可能會一直失敗，直到管理員重新整理主機金鑰為止。

## 儲存並測試 {#save-and-test}

**[!UICONTROL Save & Test]**&#x200B;僅執行&#x200B;**初始SSH主機金鑰註冊**。 這是保守的設計，不會旋轉或覆寫已註冊連線的金鑰。

| 已註冊主機金鑰狀態 | 儲存和測試的作用 |
| --- | --- |
| 尚未註冊主機金鑰 | **[!UICONTROL Save & Test]**&#x200B;會掃描堡壘主機和連線埠、註冊主機金鑰，並儲存這些金鑰以供此連線使用。 |
| 主機金鑰已註冊 | **[!UICONTROL Save & Test]**&#x200B;略過註冊。 它不會覆寫、旋轉或刪除現有的已註冊金鑰，即使即時堡壘金鑰不再相符。 |
| 已註冊金鑰遺失、空白或無效 | **[!UICONTROL Save & Test]**&#x200B;本身不會修復無效的信任資料。 管理員必須執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，如果錯誤持續發生，請連絡支援人員 |

第一次註冊成功後，稍後&#x200B;**[!UICONTROL Save & Test]**&#x200B;會執行驗證認證和連線設定，但保留已註冊的SSH主機金鑰不變。

## 重新整理SSH主機金鑰 {#refresh-ssh-host-keys}

當堡壘變更或必須修復信任資料時，**[!UICONTROL Refresh SSH Host Keys]**&#x200B;更新已註冊的SSH主機金鑰。 管理員從&#x200B;**[!UICONTROL Data]** > **[!UICONTROL Connections]**&#x200B;中的連線開始重新整理。

重新整理會在指派給您帳戶的Adobe基礎結構上以非同步方式執行。 [!DNL Commerce Intelligence]會在重新整理排入佇列後傳回。 它不會在您的工作站上執行掃描。

重新整理&#x200B;**會重新寫入**&#x200B;已註冊的主機金鑰，但前提為下列其中一個條件為True：

* 已註冊的主機金鑰遺失
* 註冊的主機金鑰為空白
* 無法讀取已註冊的主機金鑰
* 已註冊的主機金鑰無法驗證
* 新掃描傳回的主機按鍵行與已註冊按鍵不同
* 掃描和註冊金鑰的指紋不符

如果註冊的金鑰為最新且有效，則重新整理會完成，而不會變更金鑰。

>[!TIP]
>
>在您的團隊旋轉堡壘上的SSH主機金鑰、變更堡壘主機名稱或IP，或取代SSH端點後，執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**。 請稍候幾分鐘，然後執行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以確認連線。

## 帳戶移轉 {#migration}

您沒有觸發帳戶移轉。 Adobe會在維護或擴充期間執行資料伺服器移動，並複製已註冊的SSH主機金鑰，因此嚴格驗證可在移動後繼續運作。

在Adobe通知您移轉已完成後：

1. 執行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以確認連線。 如果成功複製金鑰，則應跳過註冊。
1. 如果SSH主機金鑰錯誤持續存在，請要求管理員執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等候幾分鐘，然後再次執行&#x200B;**[!UICONTROL Save & Test]**。
1. 如果錯誤在&#x200B;**[!UICONTROL Save & Test]**&#x200B;後繼續發生，且最多嘗試&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;次，請聯絡Adobe支援。

## ssh主機金鑰錯誤訊息 {#ssh-host-key-errors}

連線狀態會顯示單一使用者易記的SSH主機金鑰訊息。 原始的OpenSSH錯誤不會顯示在儀表板中。

下表將常見訊息對應至可能的原因和一般後續步驟。

| 訊息或狀態 | 其含義 | 可能的原因 | 典型的下一步 |
| --- | --- | --- | --- |
| SSH主機金鑰驗證失敗 | 堡壘主機金鑰與已註冊金鑰不符，或信任資料無法使用 | 在堡壘上輪換的SSH主機金鑰；堡壘主機名稱、IP或連線埠已變更；已註冊的金鑰遺失、空白、無效或無法讀取 | 確認&#x200B;**遠端位址**&#x200B;和&#x200B;**SSH連線埠**。 詢問您的基礎結構團隊是否變更了堡壘主機金鑰。 要求系統管理員執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等候幾分鐘，然後執行&#x200B;**[!UICONTROL Save & Test]**。 |
| 無法註冊SSH主機金鑰 | **[!UICONTROL Save & Test]**&#x200B;無法掃描或儲存基本主機金鑰 | 無法從Adobe基礎結構連線到堡壘；DNS失敗；防火牆封鎖[!DNL Commerce Intelligence]個IP位址；錯誤的&#x200B;**遠端位址**&#x200B;或&#x200B;**SSH連線埠**；堡壘上的主機金鑰掃描失敗 | 使用資料庫認證頁面上的[!DNL Commerce Intelligence] IP位址來驗證防火牆允許清單。 確認堡壘在設定的連線埠上接受SSH。 請修正連線欄位，然後再次執行&#x200B;**[!UICONTROL Save & Test]**。 |
| SSH主機金鑰遺失或無效 | 嚴格驗證已封鎖通道，因為已註冊的信任資料不存在或已損毀 | 第一個連線從未完成註冊；先前重新整理失敗；移轉未複製金鑰；Adobe基礎結構上的問題 | 要求系統管理員執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，然後&#x200B;**[!UICONTROL Save & Test]**。 如果錯誤持續發生，請聯絡支援人員。 |
| 無法完成重新整理SSH主機金鑰 | 重新整理未更新已註冊的金鑰 | 重新整理期間發生網路、DNS或掃描失敗；Adobe基礎結構發生問題 | 等候幾分鐘。 要求系統管理員再次執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]** （如果第一次嘗試失敗，則進行第二次嘗試）。 確認堡壘可達性和允許清單。 如果連線在兩次重新整理嘗試和&#x200B;**[!UICONTROL Save & Test]**&#x200B;後仍然失敗，請連絡支援人員。 |

## 疑難排解檢查清單 {#troubleshooting}

1. 確認&#x200B;**遠端位址**、**SSH連線埠**&#x200B;以及Linux使用者設定符合您的堡壘設定。
1. 確認防火牆允許資料庫認證頁面上顯示的[!DNL Commerce Intelligence]個IP位址。
1. 詢問您的基礎結構團隊最近是否變更過堡壘上的SSH主機金鑰。
1. 執行&#x200B;**[!UICONTROL Save & Test]**&#x200B;以驗證設定並註冊金鑰（如果尚未存在）。
1. 要求系統管理員執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，等候幾分鐘，然後再次執行&#x200B;**[!UICONTROL Save & Test]**。 如果首次重新整理無法解決錯誤，請重複此步驟。
1. 如果連線在兩次重新整理嘗試後仍顯示SSH主機金鑰錯誤，請按一下連線頁面（或您的帳戶支援管道）上的&#x200B;**[!UICONTROL Contact Support]**。

## 何時聯絡Adobe支援 {#contact-support}

發生下列情況時請聯絡支援人員：

* SSH主機金鑰錯誤在管理員執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;兩次，**[!UICONTROL Save & Test]**&#x200B;仍然失敗後繼續發生
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;從未完成，或連線狀態在15-30分鐘後未變更
* Adobe通知您帳戶移轉或資料伺服器維護作業後，錯誤立即開始
* 堡壘設定和防火牆允許清單正確，您的團隊尚未輪換主機金鑰，您仍然無法連線
* 您需要系統管理員才能執行&#x200B;**[!UICONTROL Refresh SSH Host Keys]**，但此帳戶沒有可用的系統管理員

包括連線名稱、上次&#x200B;**[!UICONTROL Save & Test]**&#x200B;或重新整理嘗試的大約時間，以及最近是否變更過堡壘主機金鑰。 請勿傳送私密金鑰或密碼短語。

## 相關 {#related}

* [透過SSH通道連線MySQL](mysql-via-ssh-tunnel.md)
* [透過SSH通道連線MongoDB](mongodb-via-ssh-tunnel.md)
* [透過SSH通道連線PostgreSQL](postgresql.md)
* [重新驗證整合](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
