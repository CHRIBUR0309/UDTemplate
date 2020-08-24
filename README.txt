Beamer UD Template
製作者：九州大学大学院システム情報科学府情報学専攻　2IE20027Y　坂井法仁
製作日：ver1.0 2020年8月24日
素材：texlive/2020/texmf-dist/tex/latex/beamer/beamerbasethemes.sty
% Copyright 2003--2007 by Till Tantau
% Copyright 2010 by Vedran Mileti\'c
% Copyright 2017 by Joseph Wright
%
% This file may be distributed and/or modified
%
% 1. under the LaTeX Project Public License and/or
% 2. under the GNU Public License.
%
% See the file doc/licenses/LICENSE for more details.

%
% Basic commands for including themes
%

1. これは何？
研究室のスライドUD化の一環で，beamerを用いて日本語のUDスライドを作成するためのテンプレート。
基本的な日本語対応は出来ている。

2. インストール
UDTemplate.styを編集する.texファイルと同じディレクトリに置く。
もしくはこのフォルダごとD:/texlive/texmf-local/tex/latex/local/localに入れる。> sudo mktexlsr等のコマンドを叩く必要がある。

3. .texファイルと.styファイルの説明
\documentclass[uplatex,aspectratio=43,14pt,hyperref={bookmarksnumbered=true,bookmarksopen=true,hidelinks,breaklinks=true,pdfusetitle},dvipdfmx]{beamer}
documentclassとそのオプション。
取り敢えずupLaTeX+dvipdfmxの組み合わせで記述しているが他のLaTeXエンジンを使用している場合は適宜調整すること。
アスペクト比は4:3。16:9にしたい場合はaspectratio=169にすること。
フォントサイズは14pt。相似拡大してPowerPointと同じ大きさに直すと28ptよりもやや小さい位になる。
hyperrefは適宜中身を抜き差しできる。

\usepackage{UDTemplate}
UDTemplate.styを使用するための命令。

\RequirePackage{bxdpx-beamer}
dvipdfmxでbeamerするために必要。
使用するDVIウェア（ないしLaTeXエンジン）によって必要なパッケージが変わるので，環境に合わせて調整が必要。
https://qiita.com/zr_tex8r/items/69e8cc32038ff29f5ac3
↑
これを参考にされたし。

\renewcommand{\familydefault}{\sfdefault}
\renewcommand{\kanjifamilydefault}{\gtdefault}
\renewcommand{\baselinestretch}{1.3}
基本をサンセリフ・ゴシック体にし，行間を1.3倍に広げる。

\RequirePackage{amsmath,amssymb}
\RequirePackage[OT1,T2A,X2,OT2,LGR,T1]{fontenc}
数式を打つために必要なパッケージ群と諸外国の非ASCII文字言語をある程度取り扱える様にするためのパッケージ。

\RequirePackage{lmodern,exscale}
%\RequirePackage{newtxtext,newtxmath}
%\RequirePackage{newpxtext,newpxmath}
半角英数や数式記号のフォントをデフォルトのComputer Modernから変えるパッケージ群。
Computer Modernは古くて色々アレなので変更すべき。
Latin ModernはComputer Modernの見た目はそのままに中身を改良した物。
newtx，newpxはまた別のフォント群。

\RequirePackage[expert,deluxe]{otf}
日本語を上手く出力するために絶対に必要なパッケージ。
(u)pLaTeXはこれで良いが，Lua系やXe系では別のパッケージに変える必要がある。
https://texwiki.texjp.org/?OTF
↑
これを参考にされたし。
expertオプションは縦書き横書きで和文フォントを使い分けるのに使われる。この業界のスライドでは基本的に使わないと思うが。
deluxeオプションは和文フォントの多ウェイト化に必要。といってもTeX Live 2019以前のデフォルトであるIPAexフォントでは多ウェイト化できないのでヒラギノや源ノ等のフォントを用意する必要があるのだが。TeX Live 2020からはデフォルトが原ノ味になったので特に気にせずに多ウェイト化可能になった。

\RequirePackage[noalphabet,unicode]{pxchfon}
\RequirePackage[prefernoncjk]{pxcjkcat}
\cjkcategory{sym04,sym08,sym09,sym10,sym11,sym12,sym15,sym18,sym19,sym20,brai,sym33}{cjk}
\RequirePackage[english,japanese]{pxbabel}
\RequirePackage{mathrsfs,bm}
おまじない。意味が分かっていて不要だと判断すれば外しても構わないと思う。

\RequirePackage{tcolorbox}
\tcbuselibrary{most}
UDTemplate.styでも数ヶ所で使用している。PowerPointのテキストボックスの様な物を生成できる。
beamer標準のblock環境と比べて自由度が高いのでオススメ。

\RequirePackage[bigcode]{pxjahyper}
PDFの栞が文字化けしない様に。

\renewcommand{\UrlBreaks}{\do\:\do\/\do\-\do\a\do\b\do\c\do\d\do\e\do\f\do\g\do\h\do\i\do\j\do\k\do\l\do\m\do\n\do\o\do\p\do\q\do\r\do\s\do\t\do\u\do\v\do\w\do\x\do\y\do\z\do\A\do\B\do\C\do\D\do\E\do\F\do\G\do\H\do\I\do\J\do\K\do\L\do\M\do\N\do\O\do\P\do\Q\do\R\do\S\do\T\do\U\do\V\do\W\do\X\do\Y\do\Z}
hyperref下での\url{}の折り返しを自由にする。

\RequirePackage{colortbl}
表の罫線の色を変えるパッケージ。

\RequirePackage{graphicx,xcolor}
おまじない。

\definecolor{MyCyan}{rgb}{0,1,1}
\definecolor{MyBlue}{rgb}{0.2,0,1}
これから使用するMyCyan，MyBlueという色の定義。

\tcbset{%
	width=\paperwidth,%
	height=2zh,%
	valign upper=center,%
	valign lower=center,%
	sidebyside,%
	lower separated=false,%
	sidebyside gap=0truemm,%
	halign lower=flush right,%
	colframe=MyCyan,%
	colback=black,%
	coltext=white,%
	sharp corners=all,%
	boxrule=-1pt,%
	beforeafter skip=0truemm,%
	leftright skip=0truemm,%
	left=0truemm,%
	right=0truemm,%
	top=0truemm,%
	bottom=0truemm,%
	boxsep=0truemm}
\newtcolorbox{titlepageblock}{%
	width=8zw,%
	height=3zh,%
	split=0.5,%
	sidebyside=false,%
	middle=0truemm,%
	halign upper=flush center,%
	halign lower=flush center,%
	colframe=MyBlue,%
	boxrule=0.5truemm}
\newtcolorbox{titlepagetitleblock}{%
	height=8zh,%
	sidebyside=false,%x
	halign upper=flush center,%
	colframe=MyBlue}
\newtcolorbox{headerblock}{%
	lefthand ratio=0.83,%
	bottomrule=0.5truemm}
\newtcolorbox{footerblock}{%
	halign upper=flush center,%
	lefthand ratio=0.78,%
	toprule=0.5truemm}
tcolorbox下で使えるテキストボックス環境の設定。

\setbeamersize{text margin left=0truemm,text margin right=0pt}
\usefonttheme[onlymath]{serif}
\setbeamertemplate{navigation symbols}{}
\setbeamercolor{normal text}{fg=white,bg=black}
\setbeamertemplate{title page}{%
	\nointerlineskip
	\vspace{1zh}
	\begin{titlepageblock}
		{\footnotesize\insertdate}
		\tcblower
		{\footnotesize\insertsubtitle}
	\end{titlepageblock}
	\vspace{1zh}
	\begin{titlepagetitleblock}
		{\Large\inserttitle}
	\end{titlepagetitleblock}
	\vspace{2zh}
	{%
		\raggedleft
		\begin{titlepageblock}
			{\small\insertinstitute}
			\tcblower
			{\small\insertauthor}
		\end{titlepageblock}
	}
}
\setcounter{tocdepth}{1}
\setbeamercolor{section in toc}{fg=white,bg=black}
\setbeamerfont{section in toc}{size=\normalsize}
\setbeamercolor{frametitle}{fg=white,bg=black}
\setbeamertemplate{frametitle}{%
	\nointerlineskip
	\begin{headerblock}
		\insertframetitle
		\tcblower
		\insertframenumber/\inserttotalframenumber
	\end{headerblock}
}
\setbeamerfont{frametitle}{size=\Large,series=\sffamily\bfseries}
\addtobeamertemplate{frametitle}{}{\vspace{-0.8em}}
\setbeamercolor{section in head/foot}{fg=white,bg=black}
\setbeamercolor{institute in head/foot}{fg=white,bg=black}
\setbeamertemplate{footline}{%
	\begin{footerblock}
		\insertsection
		\tcblower
		\insertshortinstitute
	\end{footerblock}
	\vskip0pt%
}
\setbeamercolor{item}{fg=MyCyan}
\setbeamercolor{subitem}{fg=MyCyan}
\setbeamercolor{description item}{fg=white,bg=black}
\setbeamerfont{description item}{series=\sffamily\bfseries}
\setbeamertemplate{itemize item}{●}
\setbeamertemplate{itemize subitem}{○}
\setbeamertemplate{itemize subsubitem}{・}
\setbeamertemplate{description item}{\insertdescriptionitem　}
\setbeamercolor{caption name}{fg=white,bg=black}
\setbeamertemplate{caption}[numbered]
\setbeamertemplate{caption label separator}{　}
\newcommand{\makeframe}[2]{%
	\begin{frame}[t]{#1}
		#2
	\end{frame}%
}
\AtBeginDocument{
	\abovedisplayskip=0truemm
	\abovedisplayshortskip=0truemm
	\belowdisplayskip=0truemm
	\belowdisplayshortskip=0truemm
}
\setbeamerfont{footline}{size=\tiny,series=\sffamily\bfseries}
\AtBeginSection[]{
	
	\setbeamercolor{section in toc}{fg=yellow,bg=black}
	\setbeamerfont{section in toc}{series=\bfseries\sffamily}
	\setbeamercolor{section in toc shaded}{fg=white,bg=black}
	\setbeamerfont{section in toc shaded}{series=\normalfont}
	\setbeamertemplate{section in toc shaded}[default][100]
	\makeframe{目次}{\tableofcontents[currentsection]}
}
UD化の実質本体。
\usefonttheme[onlymath]{serif}を外すと数式もサンセリフ体になる。
多ウェイト化しないと\bfseriesが和文フォントで効かなくなるので見た目が変わる。

\arrayrulecolor{white}
colortblパッケージのコマンド。表の罫線を白色にする。

\renewcommand{\emph}[1]{{\color[rgb]{1,1,0}\textgt{#1}}}
\newcommand{\strongemph}[1]{{\color[rgb]{1,1,0}\textgt{\textbf{#1}}}}
文字強調命令の設定。
\emph{}で文字が黄色に，\strongemph{}で太字かつ黄色になる。
多ウェイト化しなければ和文フォントでこの二つの出力結果は同じになる。

\renewcommand{\figurename}{図}
\renewcommand{\tablename}{表}
図表のキャプションラベルを日本語にする。

\newcommand{\ownitem}[2]{%
	\setlength{\leftmargini}{1zw}%
	\setlength{\leftmarginii}{1zw}%
	\setlength{\leftmarginiii}{1zw}%
	\setlength{\leftmarginiv}{1zw}%
	\begin{#1}
		\setlength{\topsep}{0truemm}%
		\setlength{\itemsep}{0truemm}%
		\setlength{\parskip}{0truemm}%
		\setlength{\itemindent}{0truemm}%
		\setlength{\labelsep}{0truemm}%
		#2
	\end{#1}%
}
箇条書きの調整。余白を詰め詰めにしている。

\title{タイトルタイトルタイトルタイトルタイトル}
\subtitle{サブタイトル}
\author{名前}
\institute[IKEDA Lab., Kyushu Univ.]{池田研究室}
\date{yyyy/mm/dd}
表紙やフッタに入る情報。
instituteのみshortinstituteを使っているが，他のshortは現状使っていないのでオプションを入れる意味は無い。
subtitleには「情報学演習」「サマープロジェクト」「中間発表」や学会名を入れれば良いのではなかろうか。

\begin{document}
必要。

	{%
		\setbeamertemplate{footline}{}
		\makeframe{}{\titlepage}
	}
タイトルページを出力。フッタは出て来ない。

	\makeframe{目次}{\tableofcontents}
目次を出力。

	\section{導入}
節の設定。
UDTemplate.sty側の調整で，sectionが始まる度にそこを強調（\strongemph{}と実質同じ）した目次が得られる。

		\makeframe{導入1枚目}{%
			次の等式は\emph{有名}である。
			\begin{equation}
				e^{i\theta}=\cos{\theta}+i\sin{\theta}
			\end{equation}
		}
		\makeframe{導入2枚目}{%
			次の方程式も\emph{有名}である。
			\begin{align*}
				&\nabla\cdot\bm{E}=\frac{\rho}{\varepsilon_0}\\
				&\nabla\times\bm{E}=-{\frac{\partial\bm{B}}{\partial t}}\\
				&\nabla\cdot\bm{B}=0\\
				&\nabla\times\bm{B}=\mu_0{\left(\bm{j}+\varepsilon_0\frac{\partial\bm{E}}{\partial t}\right)}
			\end{align*}
			この連立1階偏微分方程式は電磁気学分野の基礎方程式である。
		}
	\section{本論}
		\makeframe{本論1枚目}{
			導入で示した式はそれぞれ次の名前で呼ばれている。覚えておくと何処かで役に立つ……かもしれない。
			\ownitem{itemize}{
				\item Eulerの等式
				\item Maxwell方程式
				\ownitem{enumerate}{
					\item hoge
					\item foo
				}
			}
		}
		\makeframe{本論2枚目}{
			私が最も好きな定理は\strongemph{留数定理（residue theorem）}である。
			\begin{theorem}
				複素関数\(\displaystyle{f{\left(z\right)}}\)が正の向きを持つJordan曲線\(\displaystyle{C\subset\mathbb{C}}\)の上と内部で比較的良い性質を持つならば，
				\begin{equation*}
					\oint_{C}{f{\left(z\right)}\,dz}=2\pi i\sum_{k=1}^n{\operatorname{Res}{\left(f;\, z_k\right)}}
				\end{equation*}
				が成り立つ。
			\end{theorem}
		}
	\section{まとめ}
		\makeframe{結論}{
			私は数学が大好きだ！
		}
	\section{おまけ①}
		\makeframe{hogehoge}{
			ああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああああ
		}
	\section{おまけ②}
		\makeframe{foo}{
			ああああああああああああああああああああああああああああああああああああああ

			いいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいいい
		}
中身の例。ここを主に編集する。

	\appendix
以下をappendix環境にする。

	\backupbegin
後で出て来る\backupendとセット。

	\section{\appendixname}
		\makeframe{表の作り方}{
			\begin{table}[btp]
				\centering
				\caption{これは表です。}
				\label{tab:appendtable}
				\begin{tabular}{lrr}\hline
					& あ & い\\ \hline
					0 & 1.36538 & 0.74289\\
					1 & 5.84792 & 7.74682\\ \hline
				\end{tabular}
			\end{table}
			表\ref{tab:appendtable}はこうやって作れるんだよ！
		}
\appendix下で\backupbeginと\backupendに挟まれた\section{\appendixname}は本体の目次に載らない上に総ページ数にも計上されなくなるので，質疑応答用の隠しスライドとして仕込める。

	\backupend
先で出て来た\backupbeginとセット。

\end{document}
必要。

4. PowerPoint並みに自由な配置を行う方法。
\vspace{}，\hspace{}，minipage環境を組み合わせれば何とかなる。

4. ToDoリスト
・theorem環境の再定義
　今の所凄くダサいので。
・フッタの見直し
　dateやsubtitleを左下に加えたい。
・左側余白の改善
　ヘッダが巻き込まれない形で1zw程度下げたい。
・enumerate環境の番号の再定義
　①②③を使いたい。

5. 更新履歴
v1.0　公開