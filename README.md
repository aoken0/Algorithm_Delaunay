# ドローネ三角分割(Delaunay Triangulation)

### アルゴリズム
1. とある点の集合すべてを含むような巨大な三角形を追加する
    1. 点集合をすべて囲うような矩形を追加
    2. 矩形を囲うような円を追加
        * 中心座標 $(c_x, c_y)=(|min_x+max_x|/2, |min_y+max_y|/2)$
        * 半径 $r=\sqrt{|min_x-max_x|^2+|min_y-max_y|^2} / 2$
    3. 円に外接する正三角形を追加
        * 中心座標 $(c_x, c_y)$
        * 中心から各頂点までの距離 $2r$
        ![alt text](img/外接三角形.png)


2. 点集合のうち、i番目の点（Pi）を三角形分割図形に追加（初期であれば、巨大三角形の中に集合の中のどれかの点を入れるところから開始）
    
    1. 点Piを含む三角形ABCを見つけ (※1)、点Piを使ってその三角形を分割する（ABPi,BCPi, CAPiの3つの三角形）  
    このとき、辺AB, BC, CAをスタックに積む（仮にスタックをSとする）
    
    2. スタックSが空になるまで以下を繰り返す

        1. スタックSの一番上のedgeをpopする。これを辺ABとする

        2. 辺ABを含む2個の三角形をABC, ABDとする  
        三角形ABCの外接円にDが含まれる場合は、辺ABをフリップし、辺AD/DB/BC/CAをスタックSにpushする  
        そうでないなら処理をスキップする

3. super triangleとそれに関する頂点を破棄する（巨大三角形は処理をシンプルにするための架空のものなのでそれを消去する）


> 参考
> * https://qiita.com/edo_m18/items/7b3c70ed97bac52b2203  
> * https://tercel-sakuragaoka.blogspot.com/2011/06/processingdelaunay_3958.html  

