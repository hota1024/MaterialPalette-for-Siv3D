# MaterialPalette for Siv3Dについて
MaterialPalette for Siv3DはSiv3Dは[Material design color](https://material.io/guidelines/style/color.html)の色を扱えるようにするものです。

# 使い方
ダウンロードしたフォルダの中のMaterialPaletteをincludeすれば使えます。

Visual studioの場合は既存のファイルを追加でソリューションに追加してからincludeしてください。

# 内容
使える色の種類はMaterial design colorの

* Red
* Pink
* Purple
* DeepPurple
* Indigo
* Blue
* LightBlue
* Cyan
* Teal
* Green
* LightGreen
* Lime
* Yellow
* Amber
* Orange
* DeepOrange
* Brown
* Grey

の19種類が使えます。

例えばRedの色を使いたければ`MaterialPalette::Red`で使えます。

```c++
#include <Siv3D.hpp>
#include "MaterialPalette.h"
Main(){
    while(System::Update){
        Circle({100,100},100).draw(MaterialPalette::Red);
    }
}
```

Material design colorには色ごとにレベルがあります。

* Normal
* 50
* 100
* 200
* 300
* 400
* 500
* 600
* 700
* 800
* 900

の11個あります。

Redの400を使いたいなら`MaterialPalette::Red400`で使えます。

```c++
#include <Siv3D.hpp>
#include "MaterialPalette.h"
Main(){
    while(System::Update){
        Circle({100,100},100).draw(MaterialPalette::Red400);
    }
}
```

また色を２次元配列でも用意しています。

`MaterialPalette::List[色のインデックス][レベルのインデックス]`
色のインデックスは以下のとおりです。

0. Red
1. Pink
2. Purple
3. DeepPurple
4. Indigo
5. Blue
6. LightBlue
7. Cyan
8. Teal
9. Green
10. LightGreen
11. Lime
12. Yellow
13. Amber
14. Orange
15. DeepOrange
16. Brown
17. Grey

レベルのインデックスは以下のとおりです。

0. Normal
1. 50
2. 100
3. 200
4. 300
5. 400
6. 500
7. 600
8. 700
9. 800
10. 900

Blueの300なら`MaterialPalette::List[5][4]`でできます。

# サンプル

## 赤い円を書く
```RedCircle.cpp

# include <Siv3D.hpp>
#include "MaterialPalette.h"

void Main()
{
	while (System::Update()) {
		Circle({ 100,100 }, 100).draw(MaterialPalette::Red);
	}
}
```

## カラーライブラリ
```ColorLib.cpp
# include <Siv3D.hpp>
#include "MaterialPalette.h"

void Main()
{
	Player player;
	Color bgcolor = MaterialPalette::List[Random(0, 19)][Random(0, 11)];
	Font font(30, Typeface::Medium, FontStyle::Outline);

	while (System::Update()) {
		ClearPrint();
		Graphics::SetBackground(bgcolor);
		font(bgcolor).draw(100, 0);
		for (auto x = 0; x < MaterialPalette::ColorCount; x++) {
			for (auto y = 0; y < MaterialPalette::LevelCount; y++) {
				Rect rect({ 35 + x * 30 , 70 + y * 30 }, { 30,30 });
				rect.draw(MaterialPalette::List[x][y]);
				if (rect.leftClicked) {
					bgcolor = MaterialPalette::List[x][y];
				}
			}
		}
	}
}
```
