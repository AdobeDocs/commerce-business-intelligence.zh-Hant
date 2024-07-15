---
title: 首次購買報告的平均時間
description: 瞭解如何使用平均首次購買時間報表。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
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
