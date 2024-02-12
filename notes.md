<!-- vscode-markdown-toc -->
* 1. [GCC (GNU Compiler Collection) 基本介紹](#GCCGNUCompilerCollection)
* 2. [C executable](#Cexecutable)
	* 2.1. [Depoly to other machines](#Depolytoothermachines)
* 3. [terminal](#terminal)
* 4. [Language features](#Languagefeatures)
	* 4.1. [bitflag](#bitflag)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc --># C learning notes

##  1. <a name='GCCGNUCompilerCollection'></a>GCC (GNU Compiler Collection) 基本介紹
gcc 是為 C、C++ 和 Fortran等語言提供編譯功能的工具組。

執行 C 語言程式，需先使用 gcc 編譯成可執行檔案，我們在 bash 環境中輸入以下指令

    gcc kilo.c -o kilo

這個指令會將名為 kilo.c 的文件編譯成名為 Kilo 的可執行檔案。
具體而言，這個命令的背後所做的事情包括：

1. 預處理 ( Preprocessing )
   1. 移除註釋
   2. 展開預處理指令
   3. 處理條件編譯
   4. 替換宏
   5. 處理預定義的宏
   6. 處理特殊符號
2. 編譯 (Compiling )
   1. 語法分析 ( Syntax Analysis )
   2. 語義分析 ( Semantic Analysis )
   3. 優化 ( Optimization )
   4. 代碼生成 (Code Generation )
3. 彙編( Assembling )
   1. 處理組合語言文件
   2. 生成目標代碼
   3. 符號解析和重定位
   4. 生成目標代碼文件
4. 鏈接 ( Linking )
   1. 符號解析 ( Symbol Resolution )
   2. 重定位 ( Relocation )
   3. 合併目標代碼
   4. 生成輸出文件
##  2. <a name='Cexecutable'></a>C executable
C 可執行檔 由 C 語言編譯而成，獨立於原始碼的二進位檔案，可以在支援相應架構和作業系統電腦上運行，換句話說，如果目標機台是不同作業系統，很有可能無法順利運作。

###  2.1. <a name='Depolytoothermachines'></a>Depoly to other machines
* 確認目標平台：確認目標機台的作業系統和架構
* 交叉編譯：在開發機上編譯於目標機台的執行檔
* 測試和除錯。

##  3. <a name='terminal'></a>terminal
terminal 有兩種輸入模式，*canonical input processing*、*noncanonical input processing* 兩種。
   * Canonical mode: 終端機以行 (line) 作為單位來觸發輸入動作，即使用者按下 Enter 鍵後產生表示行尾的特殊字元 ('\n') 後開始進行輸入。
   * Noncanonical mode: 終端機則是每一字元就觸發輸入動作，無須緩衝。
  
##  4. <a name='Languagefeatures'></a>Language features
###  4.1. <a name='bitflag'></a>bitflag
`ECHO` 是 `termios` 屬性 `c_lflag` 中的一組 flag，決定是否將輸入字元回聲到終端機。假設 `c_lflag` 是 `111`，ECHO 是 `001`，要關閉 `ECHO` 可使用 `c_lflag &= ~ECHO` 指令，將會讓c_lflag 變成 `110`。
以下是關閉 `ECHO` 的完整的範例

    struct termios term;
    
    // Get the current terminal attributes
    tcgetattr(STDIN_FILENO, &term);
    
    // Turn off the ECHO flag
    term.c_lflag &= ~ECHO;
    
    // Set the modified terminal attributes
    tcsetattr(STDIN_FILENO, TCSANOW, &term);
    
    // Now input characters won't be echoed back to the terminal