# Mini Messenger — 迷你星球郵差 🪐📮

參考 [Abeto「Messenger」](https://messenger.abeto.co/) 復刻的網頁小遊戲。
你扮演郵差,在一顆小到看得見地平線弧度的迷你星球上,把信件送到 5 個發光的信箱。

純前端、單一檔案,用 [Three.js](https://threejs.org/)(WebGL)製作。

## 玩法

| 操作 | 鍵盤 / 滑鼠 | 手機 |
| --- | --- | --- |
| 移動 | `W A S D` 或方向鍵 | 左下虛擬搖桿 |
| 跳躍 | `Space` | 右下「跳」 |
| 投遞 | `E` 或點擊畫面 | 右下「送」 |
| 轉視角 | 滑鼠拖曳 | — |
| 縮放 | 滾輪 | — |
| 表情 | 底部表情列 | 底部表情列 |
| 體感視角 | — | 右上「📱 體感視角」(iOS 需授權) |

靠近發光的紅色信箱,提示出現後按投遞鍵即可送件。送完 5 封即過關。
村莊之間有沙土小路相連,沿路走就能找到下一個信箱。

## 與原版的對應

- **迷你球面世界**:角色貼著球面行走(重力指向球心),半徑刻意取小,因此看得到地平線弧度。
- **送件任務**:5 個目標信箱以黃金螺旋均勻分布在星球各處,並用光環/光柱標示。
- **第三人稱相機**、低多邊形美術、走路擺手擺腳動畫、漂浮表情(emote)。

## 執行

直接用瀏覽器開啟 `index.html` 即可(需連網以從 CDN 載入 Three.js)。
或在本機起一個靜態伺服器:

```bash
python3 -m http.server 8000
# 開啟 http://localhost:8000
```

## 可替換的物件(想換美術從這裡下手)

所有場景物件都是 `index.html` 裡的程序化函式產生的,各自獨立,替換任一個都不影響其他:

| 物件 | 函式 | 說明 |
| --- | --- | --- |
| 郵差角色 | `makePlayer()` | 主角,可整組換成 glTF 模型 |
| 一般樹 / 松樹 | `makeTree()` / `makePine()` | 葉色在 `LEAF_COLORS` |
| 灌木 / 草叢 / 花 / 香菇 | `makeBush()` `makeGrass()` `makeFlower()` `makeMushroom()` | 花色在 `FLOWER_COLORS` |
| 石頭 | `makeRock()` | |
| 房屋 | `makeHouse(color)` | 顏色在 `HOUSE_COLORS` |
| 信箱(送件目標) | `makeMailbox()` | 含發光光環與光柱 |
| 道路 | `makeRoad(a,b)` / `roadMat` | 顏色改 `roadMat` 的 `color` |
| 星球地形 | `planetGeo` + 顏色區 `cValley/cGrass/cHill/cSand/cRock` | 起伏幅度改 `BUMP_AMP` |
| 天空 | `skyMat` 的 `topCol/midCol/botCol` | |

> 要換成真正的 3D 模型(glTF/GLB),可用 Three.js 的 `GLTFLoader` 載入後取代對應 `make*()` 的回傳物件即可。

> 本作為玩法/視覺概念的獨立復刻,與 Abeto 原作無關,僅供學習測試之用。
