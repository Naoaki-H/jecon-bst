このbstファイルは，日本語で論文を書く人を対象にしています．英語で書く人は，`natbib`を用いた方が設定もシンプルでしょう．
このファイルでは，jecon_KU.bstを用いて参考文献リストを作成する主に日本語論文向けの方法と，jecon_KU.bstを使わずに参考文献リストを作成する英語論文向けの方法をともに紹介します．

## BibLaTeX + biberを用いる方法（英語論文向け）
```
%\usepackage[backend=biber, style=authoryear, maxbibnames=9, maxcitenames=3, mincitenames=1, date=year,uniquename=false , isbn=false, url=false, doi=false, eprint=false]{biblatex}
%\addbibresource{references.bib}
\documentclass[uplatex]{jsarticle}

\usepackage{biblatex}
\addbibresource{sample.bib}

\begin{document}

私は\cite{elements}を引用する。

%\bibliographystyle{unsrt}
%\bibliography{sample}

\printbibliography

\end{document}
```
