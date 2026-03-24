---
title: 首次購買報告的平均時間
description: 瞭解如何使用平均首次購買時間報表。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 0%

---

# 首次購買報告的平均時間

許多Adobe客戶都有名為`Average time to first purchase`的量度和圖表，其中顯示一組使用者的註冊日期與首次購買日期之間的平均時間。 當時間更接近目前時，資料幾乎總是會向下傾斜。

![平均第一筆訂購時間](../../assets/average-time-to-first-order.png)

這是因為這些較新的客戶還沒有機會產生從加入日期起超過一個月的任何購買。 由於從未購買的使用者完全不包括在內（直到他們真的購買為止），這會使較新客戶群組的平均向下偏好。

有些看待此量度的其他可能方式會引入較少偏差。 探索一個範例。

## 範例：對第一筆訂單執行`cohort`分析

您的`Users`儀表板上可能會有一個名為`Time to first order cohort`的圖表。 此報告使用`Distinct buyers`量度，將使用者按`cohort`周或註冊月分組，並顯示註冊後未來幾週或幾個月內首次購買的使用者比率（介於`0`到`1`之間）。

圖表可能會顯示，對於在2014年12月註冊的使用者，`0.56` （或`56%`）在第2個月（例如2015年1月）前做了第一筆訂單。

此同類群組分析是隨時間變化之使用者啟用率的良好指標。 如果此圖表開始平面化或停滯，而您對購買者的轉換率仍然未接近100%，則可能是時候透過電子郵件行銷活動啟用其餘的使用者。
