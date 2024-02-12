<!-- vscode-markdown-toc -->
* 1. [Raw mode](#Rawmode)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

# Terminal learning notes

terminal 有兩種輸入模式，*canonical input processing*、*noncanonical input processing* 兩種。
   * Canonical mode: 終端機以行 (line) 作為單位來觸發輸入動作，即使用者按下 Enter 鍵後產生表示行尾的特殊字元 (`\n`) 後開始進行輸入。
   * Noncanonical mode (raw mode): 終端機則是每一字元就觸發輸入動作，無須緩衝。
##  1. <a name='Rawmode'></a>Raw mode
* Arrow keys, `Page Up`, `Page Down`, `Home`, 和 `End` 都會輸入 3 或 4 bytes 到終端。`27`,`[`，後面接續 1-2 個字元，例如`Page Up` 是 `27`,`[`,`5`,`~`。這些被稱為 跳脫序列 (escape sequence)。
* `Backspace` 是 byte 127。`Delete` 是 4 byte 的跳脫序列。
* `Enter` 是 byte 10。換行字元 (`'\n'`)
* `Ctrl-S` 會觸發[XON/XOFF流控制](https://en.wikipedia.org/wiki/Software_flow_control)而停止輸出。`Ctrl-Q`恢復輸出。
