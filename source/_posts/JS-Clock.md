---
title: JS Clock
date: 2024-05-03 18:13:44
tags: JS 30 天挑戰
---


> [成品](https://skar5268.github.io/JavaScript30/02%20-%20JS%20and%20CSS%20Clock/index-START.html)

其實我現在還是不太懂時間角度的算法，數學都還給老師ㄌ。
因此試著紀錄看看，說不定會比較能理解？

## 一、首先需要一個時鐘，並設定秒針、時針、分針樣式

這邊直接拿教材使用，所以沒什麼好講解ㄉ

## 二、取得時間

``` bash
const now = new Date();  /*取得現在時間*/
const seconds = now.getSeconds(); // 取得秒鐘
const minutes = now.getMinutes(); // 取得分鐘
const hours = now.getHours(); // 取得小時
```

## 三、取得秒針、分針、時針的角度

```bash
let secondsDegrees = seconds / 60 * 360 + 90;
let minutesDegrees = (minutes / 60) * 360 + 90 + ((seconds / 60) * (360 / 60)); 
let hoursDegrees = (hours / 12) * 360 + 90 + ((minutes / 60) * (360 / 12));
```

### 秒針角度：
秒針走一圈是 60 秒，因此秒鐘 / 60 = 秒針所在的位置。
由於時鐘是圓形的，且時鐘的起點是 90 度，所以秒針的角度為秒針所在的位置 * 360 後再 + 90。

### 分針角度：
分針走一圈是 60 分鐘，因此分鐘 / 60 = 分針所在的位置。
由於時鐘是圓形的，且時鐘的起點是 90 度，所以分針的角度為分針所在的位置 * 360 後再 + 90。
然而秒針也會影響分針的角度，秒針走一圈，分針會走一格（一分鐘）。換句話說， 分針一秒鐘會移動 1 度。
因此實際分針的角度為：先前所得出的分針角度 + 秒數

### 時針角度：
時針走一圈是 12 小時，因此小時 / 12 = 時針所在的位置。
由於時鐘是圓形的，且時鐘的起點是 90 度，所以時針的角度為時針所在的位置 * 360 後再 + 90。
然而分針也會影響時針的角度，分針走一圈，時針會走一格（一小時）。換句話說， 時針一分鐘會移動  0.5 度。
因此實際時針的角度為：先前算出的角度 + 分鐘 * 0.5

**簡化後程式碼：**
```bash
let secondsDegrees = (seconds / 60) * 360 + 90;
let minutesDegrees = (minutes / 60) * 360 + 90 + seconds; 
let hoursDegrees = (hours / 12) * 360 + 90 + (minutes * 0.5);
```

## 四、取得 DOM，並給予他們樣式（目前時間的角度）

```bash
const secondHand = document.querySelector('.second-hand');
const minHand = document.querySelector('.min-hand');
const hourHand = document.querySelector('.hour-hand');

secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
minHand.style.transform = `rotate(${minutesDegrees}deg)`;
hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
```

## 五、設定秒、分、時針每秒移動的角度
      
```bash      
function setDate() {
 hoursDegrees = hoursDegrees +  360 / (12 * 60 * 60); // 一秒鐘移動 1/120 度
 minutesDegrees = minutesDegrees + 360 / (60 * 60);  // 一秒鐘移動 1 度
 secondsDegrees = secondsDegrees + 360 / 60; // 一秒鐘移動 6 度

 secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
 minHand.style.transform = `rotate(${minutesDegrees}deg)`;
 hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
}
```

**簡化後程式碼**
```bash      
function setDate() {
 hoursDegrees = hoursDegrees +  1/120;
 minutesDegrees = minutesDegrees + 1;
 secondsDegrees = secondsDegrees + 6;

 secondHand.style.transform = `rotate(${secondsDegrees}deg)`;
 minHand.style.transform = `rotate(${minutesDegrees}deg)`;
 hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
}
```

## 六、執行函式

```bash
setInterval(setDate, 1000) 
```
