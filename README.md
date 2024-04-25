# Unity-Note-SpriteAtlas
製作遊戲時會使用相當多的Sprite來構成畫面與UI，當然這也相應的帶來性能上的消耗。

但大學時期的我還不太有這些概念，當時的流程就是畫好一個UI或物件，儲存然後放進Unity內，接著就直接拉到場景上。

當完成後整個畫面豐富的同時，Batches也高上去了。

一般來說使用一張圖就會產生一個Batches，如果是小場景沒多少圖可能會覺得沒影響。

但試想一下，當今天是一張大地圖，勢必要夠多的物件來堆疊，這樣就會影響到效能表現。

要解決這問題也很簡單，既然圖越多Batches也越高，那把所有圖合成一張大圖就沒問題了，就是這麼簡單暴力。

動態的Sprite通常會輸出成一張序列圖。

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/Double%20Jump%20(32x32).png)

而場景物件與UI則會拚入一張大圖，放進Unity後再使用Multiple Mode進行切割。


