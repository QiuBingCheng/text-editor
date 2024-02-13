<!-- vscode-markdown-toc -->
* 1. [termios](#termios)
	* 1.1. [c_iflag](#c_iflag)
	* 1.2. [c_lflag](#c_lflag)
* 2. [Canonical mode vs Noncanonical mode (raw mode)](#CanonicalmodevsNoncanonicalmoderawmode)
	* 2.1. [Escape caracter、Escape sequence](#EscapecaracterEscapesequence)
	* 2.2. [Signal](#Signal)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# Terminal learning notes

##  1. <a name='termios'></a>termios
`termios` 是 POSIX 標準中的一部分，是用於在 UNIX 系統中控制終端 (terminal) 設備特性的資料結構。

`termios`成員變數包括以下：
* `c_iflag`：用於設置終端輸入模式的標誌。
* `c_oflag`：用於設置終端輸出模式的標誌
* `c_cflag`：用於設置終端控制特性的標誌，例如波特率、數據位、停止位。
* `c_lflag`：用於設置終端行為的標誌，例如啟用規範模式、啟用回顯。
* `c_cc`： 用於設置特殊控制字符的數組，例如終止字符、擦除字符。
以下僅列舉出本次專案中有使用到的 `c_iflag` 和 `c_lflag` 兩種成員變數，以及其相關控制標誌。

###  1.1. <a name='c_iflag'></a>c_iflag
`termios`的其中一個成員變數，用於設置終端**輸入模式**的標誌。
* `ICRNL`：將輸入中的回車符映射為換行符
* `IXON`：啟用軟件流控制 ([XON/XOFF流控制](https://en.wikipedia.org/wiki/Software_flow_control))
###  1.2. <a name='c_lflag'></a>c_lflag
是 `struct termios` 的一個變數，存儲了一系列標誌位 (bitflag)，用於控制終端行為。常見的 bitflag 如下：

* `ECHO`：控制是否在終端上回顯輸入字符。
* `ICANON`：控制終端是否處於規範模式，即是否按行進行輸入處理。
* `ISIG`：控制是否允許處理終端產生的信號字符。若關閉，則標示會將 `Ctrl+C` 等特信號字符視為普通的輸入字符。
* `IEXTEN`：控制是否啟用特定的輸入處理擴展。在某些系統上，如果輸入`Ctrl-V`後，再輸入另一個字元 `Ctrl-C`，系統將視為普通的輸入字符。
  
##  2. <a name='CanonicalmodevsNoncanonicalmoderawmode'></a>Canonical mode vs Noncanonical mode (raw mode)
terminal 有兩種輸入模式，*canonical input processing*、*noncanonical input processing* 兩種。
   * Canonical mode: 終端機以行 (line) 作為單位來觸發輸入動作，即使用者按下 Enter 鍵後產生表示行尾的特殊字元 (`\n`) 後開始進行輸入。
   * Noncanonical mode (raw mode): 終端機則是每一字元就觸發輸入動作，無須緩衝。

###  2.1. <a name='EscapecaracterEscapesequence'></a>Escape caracter、Escape sequence
* Arrow keys, `Page Up`, `Page Down`, `Home`, 和 `End` 都會輸入 3 或 4 bytes 到終端。`27`,`[`，後面接續 1-2 個字元，例如`Page Up` 是 `27`,`[`,`5`,`~`。這些被稱為 跳脫序列 (escape sequence)。
* `Backspace` 是 byte 127。`Delete` 是 4 byte 的跳脫序列。
* `Enter` 是 byte 10。換行字元 (`'\n'`)

###  2.2. <a name='Signal'></a>Signal
* `Ctrl-S` 會觸發[XON/XOFF流控制](https://en.wikipedia.org/wiki/Software_flow_control)而停止輸出。`Ctrl-Q`恢復輸出。
* `Ctrl-C` 觸發 `SIGINT` signal 到當前 process，導致終止程序。
* `Ctrl-Z` 觸發 `SIGTSTP` signal 到當前 process，導致暫停程序。