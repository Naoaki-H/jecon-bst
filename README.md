<!--
Filename:       README.md
Author:         Shiro Takeda
e-mail          <shiro.takeda@gmail.com>
First-written:  <2006/12/04>
Time-stamp:     <2021-09-14 10:18:09 st>
-->

jecon_KU.bst
==============================

"jecon_KU.bst"は京都大学経済学会が出版する経済論叢の様式にあわせて作られた，BibTeX スタイルファイルです。京都大学の学生が修士論文や博士論文を日本語で書く際にも使えます。
*このBibTeXスタイルファイルは Shiro Takedaさんの[jecon.bst](https://github.com/ShiroTakeda/jecon-bst)を一部改変したものです。また，このファイルは京都大学経済学会が公式に認めたものではありません。このファイルが原因で不採択などになった場合も責任は取りかねます．*

* 「著者（年）」形式（author-year format) で引用できます。
*  経済学でよく利用されるような参考文献（reference）の形式を実現できます（ただし、
  特定の雑誌向けというわけではないです）。
* 英語の文献だけでなく、日本語の文献も適切に処理できます。
* 他の BibTeX 用のスタイルファイルよりも表示形式のカスタマイズが簡単にできます。

## コンパイル
LaTeX エンジンとして `lualatex`、BibTeX エンジンとしては `upbibtex` を使うようにしてください。（TeX Live 2020までの）古い upbibtex、あるいは pbibtex を使いたい場合は、[`jecon-example.pdf`](jecon-example.pdf) の「BibTeXエンジンの選択」という節を見てください

## jecon.bstとの相違点
jecon.bst（多分2022/1/1くらいのバージョン）のどの部分を変更したのかを記述します。今後jecon.bstのマイナーアップデートが行われても，以下の通りにコピペすればとりあえず問題ないかと思われます。
### 著者名を3名までは省略しない
```
% 何人以上の著者がいるときに引用部分で et al.で省略するか。3人以上のとき
% に略すときは #3 を指定。
FUNCTION {bst.and.others.num}
{ #3 }	  % 3人以上なら省略する。(default)
% { #4 }
```
↓
```
% 何人以上の著者がいるときに引用部分で et al.で省略するか。3人以上のとき
% に略すときは #3 を指定。
FUNCTION {bst.and.others.num}
%{ #3 }	  % 3人以上なら省略する。(default)
 { #4 }
 ```

### URL, DOI, noteの非表示
これはフォーマットで要請されているものではありませんが，参考文献の例では諸々が省略されているようなので，それに準じました。
```
FUNCTION {format.url}
{ url empty$
    { "" }
    { type$ "online" = bst.show.url or
	{ is.kanji.entry
	    { bst.url.pre.jp url * bst.url.post.jp *
		access empty$
		    { "" * }
		    { bst.access.pre.jp * access * bst.access.post.jp * }
		if$
	    }
	    { bst.url.pre url * bst.url.post *
		access empty$
		    { "" * }
		    { bst.access.pre * access * bst.access.post * }
		if$
	    }
	  if$
	}
	{ "" }
      if$
    }
  if$
}

FUNCTION {format.doi}
{ doi empty$ bst.show.doi not or
    { "" }
    { is.kanji.entry
	{ bst.doi.pre.jp doi * bst.doi.post.jp * }
	{ bst.doi.pre doi * bst.doi.post * }
      if$
    }
  if$
}

FUNCTION {format.url.doi}
{ url empty$
    { format.doi }
    { doi empty$
	{ format.url }
	{ bst.url.doi #0 =
	    { format.url output.nocomma
	      format.doi }
	    { bst.url.doi #1 =
		{ format.url } 
		{ format.doi }
	      if$
	    }
	  if$
	}
      if$
    }
  if$
}

FUNCTION {format.note}
{ note empty$
    { "" }
    { is.kanji.entry
	{ bst.note.pre.jp note * bst.note.post.jp * }
	{ bst.note.pre note * bst.note.post * }
      if$
    }
  if$
}
```
↓
```
FUNCTION {format.url}{}

FUNCTION {format.doi}{}

FUNCTION {format.url.doi}{}

FUNCTION {format.note}{}
```
### ファーストネームの省略．
これもフォーマットで要請されているものではありませんが，参考文献の例ではファーストネームが省略されているようなので，それに準じました。
```
FUNCTION {bst.first.name.initial}
{ #0 }	  % #0 -> 略さない。 (default)
%{ #1 }    % #0 以外 -> first name
```
↓
```
FUNCTION {bst.first.name.initial}
%{ #0 }	  % #0 -> 略さない。 (default)
{ #1 }    % #0 以外 -> first name
```
## ファイル

| ファイル                                 | 説明                                                       |
|:-----------------------------------------|:-----------------------------------------------------------|
| `jecon.bst`                              | これが bst ファイルです。                                  |
| `README.md`                              | このファイルです。                                         |




<!--
--------------------
Local Variables:
mode: markdown
fill-column: 80
coding: utf-8-dos
End:
-->

