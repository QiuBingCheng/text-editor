# 如何執行 C 程式？

## GCC (GNU Compiler Collection) 基本介紹
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
   
## terminal
terminal 有兩種輸入模式，*canonical input processing*、*noncanonical input processing* 兩種。
   * Canonical mode: 終端機以行 (line) 作為單位來觸發輸入動作，即使用者按下 Enter 鍵後產生表示行尾的特殊字元 ('\n') 後開始進行輸入。
   * Noncanonical mode: 終端機則是每一字元就觸發輸入動作，無須緩衝。
