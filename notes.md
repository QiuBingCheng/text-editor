# 如何執行 C 程式？
執行 C 語言程式，需要先安裝 gcc 組件，並在 bash 環境中輸入以下指令

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

## 預處理 ( Preprocessing )
