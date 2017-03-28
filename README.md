長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
#install.packages("rvest")
#install.packages("XML")
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Loading required package: xml2

``` r
library(XML)
```

    ## 
    ## Attaching package: 'XML'

    ## The following object is masked from 'package:rvest':
    ## 
    ##     xml

``` r
pttNBA <- c("https://www.ptt.cc/bbs/NBA/index4614.html","https://www.ptt.cc/bbs/NBA/index4615.html", "https://www.ptt.cc/bbs/NBA/index4616.html", "https://www.ptt.cc/bbs/NBA/index4617.html", "https://www.ptt.cc/bbs/NBA/index4618.html", "https://www.ptt.cc/bbs/NBA/index4619.html", "https://www.ptt.cc/bbs/NBA/index4620.html")
for(n in 1:7) {
    pttNBAContent <- read_html(pttNBA[n])
post_title <- pttNBAContent %>%
    html_nodes(".title") %>% html_text()
post_pushNum <- pttNBAContent %>%
    html_nodes(".nrec") %>% html_text()
post_author <- pttNBAContent %>%
    html_nodes(".author") %>% html_text()
if(n == 1) {
    pttNBA_postsAll <- data.frame(Title = post_title, PushNum = post_pushNum, Author = post_author)
} else {
    pttNBA_posts <- data.frame(Title = post_title, PushNum = post_pushNum, Author = post_author)  
    pttNBA_postsAll <- rbind(pttNBA_postsAll, pttNBA_posts)
  }
}
```

爬蟲結果呈現
------------

``` r
knitr::kable(
    pttNBA_postsAll[c("Title", "PushNum", "Author")])
```

| Title                                                 | PushNum | Author       |
|:------------------------------------------------------|:--------|:-------------|
| \[討論\] booker的70分要打星號嗎?                      | 16      | kiversonx17  |
| \[討論\] 70分和贏球你選哪個？                         | 98      | jack7614614  |
| Re: \[情報\] Lebron右眼角膜劃傷，可能缺席對戰巫師     | 45      | VVVBB124     |
| \[討論\] 用數據理性分析詹皇能刷幾分                   | 27      | ChaoSong5566 |
| \[專欄 2017屆百大高中生介紹:Trevon Duval              | 4       | bithmuth602  |
| \[新聞\] 對比體測，Rose 和Westbrook 誰天賦更高        | 68      | ilovekobe824 |
| Re: \[討論\] 70分和贏球你選哪個？                     | 36      | supereight   |
| Re: \[新聞\] Booker賽後發推：成為傳奇！               | 23      | Raskolnikov  |
| Re: \[情報\] Lebron右眼角膜劃傷，可能缺席對戰巫師     | 20      | lauren1788   |
| \[新聞\] 活塞近況低迷 教頭向子弟兵喊話                | 6       | sampsonlu919 |
| Re: \[討論\] 70分和贏球你選哪個？                     | 9       | KevinLove    |
| \[討論\] 用一個字來形容球員                           | 14      | roy1190      |
| \[新聞\] Jokic無所不能 金塊勝溜馬穩固老8席次          | 31      | jailkobe5566 |
| \[外絮\] 熱火老闆IG趣圖恭喜O'Neal                     | 6       | bigDwinsch   |
| \[討論\] Booker 70分之練新秀迷思                      |         | asonofdevily |
| Re: \[討論\] 全盛時期的俠客歐尼爾有多強？             | X2      | backere0720  |
| Re: \[討論\] 70分和贏球你選哪個？                     | 11      | deepinheart  |
| Re: \[討論\] 全盛時期的俠客歐尼爾有多強？             | 4       | pinjose      |
| \[討論\] booker跟全盛期歐肥同隊的話會幾連霸?          | X2      | zsert13322   |
| \[討論\] 這三種球員怎麼選擇                           | X3      | backere0720  |
| Re: \[討論\] 70分和贏球你選哪個？                     | 9       | abc7360393   |
| \[討論\] 球沒進 在籃框旁撥三次撥進算幾個籃版          | 24      | teeo         |
| \[情報\] NBA Standings(2017.03.25)                    | 22      | kadasaki     |
| Re: \[討論\] 這三種球員怎麼選擇                       | 47      | black32044   |
| \[討論\] KOBE算小弟趕老大中趕過最大咖的老大嗎?        | 2       | KyrieIrving1 |
| \[討論\] 輸球卻很高興 ?                               | 爆      | Turtle100    |
| Re: \[討論\] 70分和贏球你選哪個？                     | 6       | feyako       |
| Re: \[討論\] 全盛時期的俠客歐尼爾有多強？             | X1      | KDimitrov313 |
| \[討論\] 73勝跟總冠軍會選哪個                         | 8       | zxc88597     |
| \[討論\] NBA七個最奇怪的紀錄                          | 爆      | shiuichi     |
| \[花邊\] O'Neal談Kobe：沒有他我完成不了這些成就       | 76      | Yui5         |
| \[花邊\] NBA+黑子籃球 對照看板                        | 13      | KyrieIrving1 |
| \[新聞\] 籃網敗給巫師 林書豪感到沮喪                  | 16      | iam168888888 |
| \[情報\] 本季團隊大三元排行榜                         | 爆      | checktime    |
| \[新聞\] 大鬍子極力促成 湖人砍將得以轉戰火箭          | 22      | leo755269    |
| \[情報\] J.Noah 因違反禁毒項目，將遭禁賽20場          | 24      | super1315566 |
| (本文已被刪除) \[zzzz8931\]                           | X2      | -            |
| \[花邊\] 美國知名饒舌歌手新歌怒嗆KD <叛徒>            | 91      | zsert13322   |
| \[Live\] 爵士 @ 快艇                                  | 16      | Rambo        |
| Re: \[討論\] 全盛時期的俠客歐尼爾有多強？             |         | ilovesumika  |
| \[BOX \] Jazz 95:108 Clippers 數據                    | 21      | Rambo        |
| \[Live\] 巫師 @ 騎士                                  | 爆      | Rambo        |
| \[新聞\] 違反禁藥規定　他被聯盟禁賽20場               | X6      | HANASUCIA    |
| \[Live\] 暴龍 @ 小牛                                  | 7       | Rambo        |
| \[Live\] 尼克 @ 馬刺                                  | 爆      | Rambo        |
| Re: \[花邊\] O'Neal談Kobe：沒有他我完成不了這些成就   | X2      | backere0720  |
| \[Live\] 灰狼 @ 拓荒者                                | 5       | Rambo        |
| \[新聞\] MVP好難選 鵜鶘教練建議選兩個                 | 23      | DantesChen   |
| \[討論\] 拿到單季MVP大滿貫有多難                      | 7       | kyoiori100   |
| \[BOX \] Wizards 127:115 Cavaliers 數據               | 爆      | Rambo        |
| \[討論\] 大三元與MVP                                  | 爆      | feyako       |
| \[閒聊 \] Kobe發推特祝賀Booker 70分                   | 54      | dragon803    |
| \[花邊\] 最長連續罰球金氏世界紀錄保持者逝世           | 93      | bigDwinsch   |
| \[討論\] 長相是否影響人氣很多？                       | 99      | yokann       |
| \[BOX \] Knicks 98:106 Spurs 數據                     | 44      | Rambo        |
| \[新聞\] 詹皇帶傷當眼鏡俠硬拚 騎士仍遭巫師擊敗        | 12      | kingtseng    |
| \[BOX \] Raptors 94:86 Mavericks 數據                 | 10      | Rambo        |
| \[討論\] KP是不是過譽了?                              | 25      | randy225     |
| \[情報\] POPO開玩笑：不會在季後賽開始前簽下秘密       | 38      | Wall62       |
| \[花邊\] Kobe：湖人聯繫我就一個電話的事               | 56      | lovea        |
| \[討論\] Kobe的雕像要做成什麼姿勢？                   | 93      | tpc302       |
| \[情報\] 盧：有些防守戰術將留到季後賽用               | 93      | CCULaoDa     |
| \[討論\] 騎士的最大心魔                               | 6       | ppeerrrryy   |
| Re: \[討論\] 長相是否影響人氣很多？                   | 34      | rukawa28     |
| Fw: \[新聞\] 鮑爾父親：一場比賽並不能決定整個賽季     | 55      | olively      |
| \[BOX \] Timberwolves 100:112 Blazers 數據            | 36      | Rambo        |
| \[情報\] TODAY+2001TODAY                              | 9       | Ivers        |
| \[新聞\] 成就不只如此？歐尼爾：奈許2座MVP是我的       | X5      | vm04vm04     |
| \[花邊\] 庫班對BG被JJ推倒感到抱歉                     | 爆      | firstsg      |
| \[花邊\] 歐肥爆粗口　幹譙當年沒投他MVP的記者          |         | adam7148     |
| \[討論\] 關於一些籃球的英文                           | 54      | js2a117573   |
| \[新聞\] 爵士近5戰輸4場 戈貝爾：球隊有人只想刷        | 爆      | whj0530      |
| \[新聞\] 護目鏡隨手扔 詹皇差點丟到巫師二哥（影        |         | dameontree   |
| \[討論\]大家覺得 ALT如何？                            | XX      | ccps970915   |
| Re: \[花邊\] 最長連續罰球金氏世界紀錄保持者逝世       | 4       | sscck5       |
| \[討論\] 一個教練優劣的觀察期要多長？                 | 17      | h1212123tw   |
| (本文已被刪除) \[MrSatan\]                            | 4       | -            |
| \[情報\] James重申:這是我生涯中最有挑戰性的賽季       | 70      | knic52976    |
| \[討論\] MVP：西河還是鬍子？                          | 88      | ddd123       |
| \[新聞\] 成最年輕得分王 布克期許自己謙虛              | 4       | adam7148     |
| Re: \[討論\] 關於一些籃球的英文                       | 40      | ej04cj86     |
| \[新聞\] 柯爾：杜蘭特復出還需要幾周時間               | 26      | iso2288      |
| \[討論\] 開季前~整季勝場預測 vs 現在                  | 15      | checktime    |
| \[情報\] 小河流:單挑能打爆我爹，即使他巔峰            | 42      | bigDwinsch   |
| \[新聞\] 克勞佛爆發 快艇連6季駛進季後賽               | 22      | gt097231     |
| Re: \[心得\] 看了單場得分50+統計，原來老大這麼強!     | 10      | huntai       |
| Re: \[討論\] 長相是否影響人氣很多？                   | 96      | lariat       |
| \[情報\] TNT: LBJ 像 好 酒                            | 20      | Turtle100    |
| \[討論\] Brett Brown算是有料的教練嗎                  | 11      | whattheduck  |
| (本文已被刪除) \[waiting0212\]                        |         | -            |
| \[新聞\] NBA／伊巴卡歸隊轟下18分 助暴龍連4季闖        | 6       | iam168888888 |
| \[新聞\] Kobe退休後最大的困擾 居然是看不到NBA         | 76      | zzzz8931     |
| \[情報\] ★今日排名(2017.03.26)★ 6                     | Ra      | mbo          |
| \[討論\] 布拉與大歐                                   | 27      | fliesa       |
| \[心得\] 突然想紀念看過的現場                         | 44      | walkerold    |
| \[情報\] 各隊場均kWPA &gt;0.2者(綜合勝率提升指數)     | 23      | checktime    |
| Re: \[討論\] 布拉與大歐                               | 9       | Tina741214   |
| \[新聞\] 單打他準沒錯！NBA各位置防守最糟糕的現        | 爆      | brandon0415  |
| \[新聞\] 本季最絕望球隊 籃網得第一                    | 40      | jailkobe5566 |
| \[新聞\] 客場一日遊累趴 湖人主帥砲轟賽程安排          | 10      | sampsonlu919 |
| \[Live\] 籃網 @ 老鷹                                  | 爆      | Rambo        |
| (本文已被刪除) \[dragon803\]                          |         | -            |
| \[Live\] 國王 @ 快艇                                  |         | Rambo        |
| \[Live\] 雷霆 @ 火箭                                  | 爆      | Rambo        |
| \[BOX \] Suns 106:120 Hornets 數據                    | 19      | Rambo        |
| \[BOX \] Nets 107:92 Hawks 數據                       | 爆      | Rambo        |
| \[Live\] 七六人 @ 溜馬                                | 2       | Rambo        |
| \[Live\] 熱火 @ 超賽                                  | 3       | Rambo        |
| Re: \[新聞\] 本季最絕望球隊 籃網得第一                | 5       | sasolala     |
| \[BOX \] Bulls 109:94 Bucks 數據                      | 31      | Rambo        |
| \[BOX \] Thunder 125:137 Rockets 數據                 | 爆      | Rambo        |
| \[BOX \] Kings 98:97 Clippers 數據                    | 47      | Rambo        |
| \[新聞\] Kobe的第1座銅像　竟然在中國廣州              | 26      | JAL96        |
| \[新聞\] 林書豪勇奪19分　籃網3月第7勝到手比騎士還厲害 | 79      | jay0601zzz   |
| \[Live\] 灰熊 @ 勇士                                  | 爆      | Rambo        |
| \[Live\] 鵜鶘 @ 金塊                                  | 12      | Rambo        |
| \[BOX \] Sixers 94:107 Pacers 數據                    | 12      | Rambo        |
| \[BOX \] Heat 108:112 Celtics 數據                    | 28      | Rambo        |
| \[討論\] 小蟲V.S.嘴綠                                 | 4       | lovero61108  |
| \[Live\] 拓荒者 @ 湖人                                | 8       | Rambo        |
| \[專欄\] 騎士漏洞愈來愈多 衛冕軍狂拉警報LYS           |         | pneumo       |
| \[新聞\] 哈登魏少難割愛 Kobe支持「雙MVP」             | 爆      | pneumo       |
| \[BOX \] Pelicans 115:90 Nuggets 數據                 | 63      | Rambo        |
| \[討論\] 這幾場籃網的板凳有什麼改變                   | 30      | mimi8598     |
| \[花邊\] 老鷹主場球迷用屁股走路                       | 36      | jay0601zzz   |
| \[BOX \] Grizzlies 94:106 Warriors 數據               | 爆      | Rambo        |
| \[情報\] 爵士鎖定季後賽位置                           | 15      | sthho        |
| Re: \[討論\] 這幾場籃網的板凳有什麼改變               | 28      | lopopo001    |
| (本文已被刪除) \[sthho\]                              |         | -            |
| \[新聞\] 騎士內憂外患 東區龍頭快不保                  | 42      | jailkobe5566 |
| \[討論\] Booker將來能拿幾冠?                          | 2       | yenyu73      |
| \[情報\] Lue談防守：不能過早暴露我們的實力            | 39      | knic52976    |
| \[情報\] Ryan Anderson 腳踝扭傷將休養兩週             | 18      | thnlkj0665   |
| \[討論\] 書豪是不是其實真的蠻強的啊                   | 爆      | kiske011     |
| (本文已被刪除) \[sincerity37\]                        | 53      | -            |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？             | 14      | strmof22     |
| \[BOX \] Blazers 97:81 Lakers 數據                    | 40      | Rambo        |
| Re: \[討論\] 書豪是不是其實真的蠻強的啊               |         | belief0816   |
| Re: \[討論\] 季後全力詹這說法是光彩的嗎？             | 7       | chxx         |
| Re: \[討論\] 書豪是不是其實真的蠻強的啊               | X2      | c1236        |

解釋爬蟲結果
------------

-   共爬出幾篇文章標題？

``` r
str(pttNBA_postsAll)
```

    ## 'data.frame':    140 obs. of  3 variables:
    ##  $ Title  : Factor w/ 129 levels "\n\t\t\t\n\t\t\t\t[討論] 70分和贏球你選哪個？\n\t\t\t\n\t\t\t",..: 6 1 13 2 12 9 14 16 13 10 ...
    ##  $ PushNum: Factor w/ 61 levels "","11","14","16",..: 4 15 11 7 10 13 9 6 5 12 ...
    ##  $ Author : Factor w/ 89 levels "asonofdevily",..: 11 8 18 5 4 7 17 14 12 16 ...

A: 總共有140篇文章。

-   哪個作者文章數最多？

``` r
authorCount <- data.frame(Author = unique(pttNBA_postsAll$Author), Count = 0)
for(i in 1:nrow(authorCount)) {
    for(j in 1:nrow(pttNBA_postsAll)) {
        if(authorCount$Author[i] == pttNBA_postsAll$Author[j]){
            authorCount$Count[i] = authorCount$Count[i] + 1
        }
    }
}
authorCount <- authorCount[order(-authorCount$Count, authorCount$Author),]
knitr::kable(
    authorCount[1:5, c("Author", "Count")])
```

|     | Author       |  Count|
|-----|:-------------|------:|
| 36  | Rambo        |     29|
| 35  | -            |      6|
| 16  | backere0720  |      3|
| 14  | bigDwinsch   |      3|
| 13  | jailkobe5566 |      3|

A: 發文數排名前五名如上，Rambo的文章最多。

-   其他爬蟲結果解釋
    -   在NBA版有個文章分類是Live，應該是在有直撥比賽的時候的討論串。可以發現一些人氣較高的球隊的比賽關注人數及討論熱度都比較高，例如：勇士、騎士、火箭隊等，堆文數都到達「爆」的等級。其他像是一些八卦的討論串討論熱度也很高，由此可見台灣人有多愛八卦了。反而像是戰術分析之類的討論串討問熱度就不如前兩種高，所以我們可以推論出：喜歡觀賞NBA比賽的人不見得會（喜歡）打籃球。
