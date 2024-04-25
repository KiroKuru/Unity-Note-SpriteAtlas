# Unity筆記-SpriteAtlas
製作遊戲時會使用相當多的Sprite來構成畫面與UI，當然這也相應的帶來性能上的消耗。

但大學時期的我還不太有這些概念，當時的流程就是畫好一個UI或物件，儲存然後放進Unity內，接著就直接拉到場景上。

當完成後整個畫面豐富的同時，Batches也高上去了。

一般來說使用一張圖就會產生一個Batches，如果是小場景沒多少圖可能會覺得沒影響。

但試想一下，當今天是一張大地圖，勢必要夠多的物件來堆疊，這樣就會影響到效能表現。

要解決這問題也很簡單，既然圖越多Batches也越高，那把所有圖合成一張大圖就沒問題了，就是這麼簡單暴力。

而製作時會遇到的大致是這兩種狀況。

- 動態的Sprite通常會輸出成一張序列圖

![image](https://i.imgur.com/7Dqaszt.png)

- 而場景物件、地圖板塊與UI則會拚入一張大圖，放進Unity後再使用Multiple Mode進行切割

![image](https://imgur.com/Zq1oISa.png)

第一項序列圖沒什麼問題，但第二項如果碰到需要換圖、尺寸不對、加圖等，就需要重新編排跟切割。

這樣一來一往就增加了時間成本，顯然應該有更好的方法。

這時候就可以使用Unity本身自帶的Sprite Atlas功能。

https://docs.unity3d.com/Manual/class-SpriteAtlas.html

Sprite Atlas可以將散圖自動集成一張大圖，可以想成將拼成一張大圖這個步驟自動化了。

# 使用方法

首先建立一個Sprite Atlas

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/SpriteAtlasCreate.png)

這邊可以進行一些基本設定

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/SpriteAtlasSetting.png)

- Type
  
  有分Master與Variant，Master代表主圖，作為Variant的基礎，通常解析度比較高。

  Variant則是Master的衍生版本，根據特定要求生成，例如不同解析度、壓縮設定、針對特定平台的優化等。

- Allow Rotation
  
  允許打包時旋轉圖片，最大化圖片間的密度。但要注意如果有包含Canvas UI，需要取消勾選，因為也會同時旋轉他們在場景中的方向。

- Tight Packing

  勾選後會根據圖片的輪廓來打包，而非矩形框，最大化圖片間的密度。

- Padding

  這是設置圖片間相鄰的距離，用來防止圖片間相互重疊。

設定好後在下方Objects for Packing可以選擇需要打包的資料夾或圖片，最後選擇Pack Preview就會自動進行打包。

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/SpriteAtlasPacking.png)

可以看到同一場景Batches的數值從14降到2。(Statistics在Game視窗的右上角Stats)

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/SpriteAtlasBefore.png)

![image](https://github.com/KiroKuru/Unity-Note-SpriteAtlas/blob/main/SpriteAtlasAfter.png)

額外提一下，之前使用Shader的UV時，如果圖與圖的間距太近，會看到附近的其他圖。

這情況可以調整一下Padding的大小增加間距，或是乾脆另外處理。


Sprite Atlas是個蠻好用的功能，簡單幾個步驟就能改善，使用上也沒什麼大問題。
