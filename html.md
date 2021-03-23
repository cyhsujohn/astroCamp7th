# 0323 HTML/CSS
###### tags: `HTML/CSS`


#### box model (盒模型)：四個 box
![](https://i.imgur.com/SR4mUuj.png =200x)

實際佔掉空間
width: 預設為指定 content-box 的寬度
border
padding
------以上實際但得到的
margin
                  
box-sizing 改變 width 指定寬度的 box
e.g.
- box-sizing: border-box：變成border總寬度是200px
- width: 200px
- 再利用padding去調整內容物的位置跟寬度
-只能指定兩個值：
  - content-box
  - border-box 

![](https://i.imgur.com/4RyEJUX.png =300x)
預設為 content-box 的寬度
```css=
  .box{
            width: 200px;
            font-size: 20px;
            background-color: #ccc;
            border: 20px solid red;
            padding: 20px;
        }
```
改成border-box寬度
![](https://i.imgur.com/ImuE0yc.png =300x)
```css=
 .box{
            width: 200px;
            font-size: 20px;
            background-color: #ccc;
            border: 20px solid red;
            padding: 20px;
            box-sizing: border-box;
        }     
```

---
## Flex 的三個屬性
＊控制物件在主軸上佔據的空間（若主軸為橫，則控制寬度）
- flex-grow：伸展值 (分紅) => 適用於子層物件總空間較父層空間小的時候
- flex-basis：基本值 => 控制物件在主軸上的長度
- flex-shrink：收縮值 （減薪-共體時艱）=> 適用於子層物件總空間較父層空間大的時候

*flex box 
- 本身具有彈性收縮的特性，但也有基本的大小

父層使用 flex 時，子層會自動收縮，即使超過父層的寬度也會自動收縮
子層們扣除的寬度是使用**加權計算**來算個別扣除比例
- [ ] flex-grow.html 
```css=
        .wrap{
            width: 900px;
            display: flex;
            border: 10px solid red;
        }
        .item{
            width: 500px;
            height: 300px;
            font-size: 50px;
        }
        .item1{
            background-color: #faa;
            flex-shrink: 1;
        }
        .item2{
            background-color: #afa;
            flex-shrink: 2;
        }
        .item3{
            background-color: #aaf;
            flex-shrink: 0;
        }
```
![](https://i.imgur.com/lBn7CVP.png =x100)
- 若加權寫了但全為 0 都不收縮，則爆出
```css=
.item1{
            background-color: #faa;
            flex-shrink: 0;
        }
        .item2{
            background-color: #afa;
            flex-shrink: 0;
        }
        .item3{
            background-color: #aaf;
            flex-shrink: 0; 
        }
```
![](https://i.imgur.com/FmxrRYH.png  =x100)


- 讓哪個空間佔滿==剩餘空間==
- flex-grow 用來分配剩餘空間要給誰佔滿：一樣用加權指數計算
```css=
.item{
            width: 100px;
            height: 300px;
            font-size: 50px;
        }
        .item1{
            background-color: #faa;
            flex-grow: 3;
        }
        .item2{
            background-color: #afa;
            flex-grow: 0.5;
        }
        .item3{
            background-color: #aaf;
        }
```
![](https://i.imgur.com/I9xgQRk.png =x100)

- 搭配 margin 使用
```css=
.item{
            width: 0px;
            height: 300px;
            margin: 10px;
            font-size: 50px;
        }
        .item1{
            background-color: #faa;
            /* flex-shrink: 1; */
            flex-grow: 2;
        }
        .item2{
            background-color: #afa;
            /* flex-shrink: 2; */
            flex-grow: 0.5;
        }
        .item3{
            background-color: #aaf;
            /* flex-shrink: 0; */
            flex-grow: 1;   
        }
```
![](https://i.imgur.com/kNb3XDU.png =x100)

**flex-basis 基本值**
- 指定主軸上子物件長度
- 若主軸為橫，則為寬度
- *等同於子物件的長度*
```css=
.item{
            width: 500px;
            height: 300px;
            flex-basis: 100px; //主軸是橫
            margin: 10px;
            font-size: 50px;
        }
```
![](https://i.imgur.com/lkpNtGU.png =x100)

### order 排序
- flex order 預設為 0
- 可以更改子物件在主軸上的順序（排序）
- 比0大往終點移動
- 比0小往起點移動
- **不一定要 0，最終是比較子物件的order順序大小，小排到大**
- 順序是看整串，不是看列（因為flex-wrap會換列）
```css=
.item1 {
    background-color: #faa;
    order: 0;
    }
.item2 {
    background-color: #afa;
    order: 1;
    }
.item3 {
    background-color: #aaf;
    }
```
![](https://i.imgur.com/1jzhAUV.png =x100)
- 順序是看整串，不是看列（因為flex-wrap會換列）
```css=
.item1{
        background-color: #faa;
        order: 2;
        }
.item2{
        background-color: #afa;
        order: 4;
        }
.item3{
        background-color: #aaf;
        order: 3;;
        }
.item4{
        background-color: #ffa;
        order: -1;;
        }
```
![](https://i.imgur.com/uIVLxQ2.png =x200)


---
## inline v.s. block

|  | inline | block | inline-block|
| -- | -- | ---|--|
| width & height | X | O| O |
|margin上下|X|O|O|
|margin左右|O(但只有第一行，換行沒有)|O|O|
|padding上下|X(*當作沒作用*)|O|O|
|padding左右|O|O|O|
|預設排列方向|橫排|直排|橫排|
|預設寬度|內容決定|滿版寬(width:auto)|內容決定|
|空白字元影響|保留空白|無此問題|保留空白|
|垂直對其支援性（vertical-align)|有效(對自己及他人)|無效|有效|
- nav:block
- span: inline
- div:block
- strong:inline
- img:inline

### 預設換行空白：一個空白字元
- 黏起來
- 把空白註解掉
```htmlmixed=
   <a href="" class="1">link</a><!--
--><a href="" class="2">link</a>
   <a href="" class="3">link</a>
```
- 把尾巴</a>的>到下一行
```htmlmixed=
<a href="" class="2">link</a
><a href="" class="3">link</a>
```
- 父層的font-size為0，但必須在子層各自設定font-size大小
```css=
.span {
        background-color: #ccc;
        margin: 200px;
        }
.div {
        background-color: #faa;
        }
.nav {
        background-color: #aaa;
        font-size: 0;
        }
.nav a {
        background-color: #fa0;
        font-size: 20px;
        }
```
![](https://i.imgur.com/bCkhImd.png =x150)
- 依照字型大小做margin-4px或-5px
```css=
.nav a{
        background-color: #fa0;
        font-size: 20px;
        margin: -4px;
        }
```

### 字元線與位置
![](https://i.imgur.com/gqP3XMY.png =200x)
- 預設使用baseline
- 使用圖片需要注意:
  -圖片只要不要對齊基線就可以滿版(以下三種寫法皆可)
    ```CSS=
    vertical-align: top;
    vertical-align: middle;
    vertical-align: bottom;
    ```
    未改，預設為baseline
```css=
  .pic{
       background-color: #f00;
       font-size: 30px;
      }
  .pic img{
        }
```
![](https://i.imgur.com/bBtSGHK.png =x150)

  將VA改為非預設（上面三個選項）
 ```css=
  .pic{
       background-color: #f00;
       font-size: 30px;
      }
  .pic img{
    vertical-align: middle;
        }
``` 
![](https://i.imgur.com/iW7TIok.png =x150)





