<!-- vscode-markdown-toc -->
* 1. [`termios`](#termios)
	* 1.1. [c_lflag](#c_lflag)
	* 1.2. [bitflag operation](#bitflagoperation)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# C Language Features

##  1. <a name='termios'></a>`termios`
控制 終端 (terminal) 特性的 [POSIX](references.md#POSIX) 標準的結構體。

###  1.1. <a name='c_lflag'></a>c_lflag
是 `struct termios` 的一個變數，存儲了一系列標誌位 (bitflag)，用於控制終端的本地模式。常見的 bitflag 如下：

* `ECHO`：控制是否在終端上回顯輸入字符。
* `ICANON`：控制終端是否處於規範模式，即是否按行進行輸入處理。
* `ISIG`：控制是否允許處理終端產生的信號字符。若關閉，則標示會將 `Ctrl+C` 等特信號字符視為普通的輸入字符。
* `IEXTEN`：控制是否啟用特定的輸入處理擴展。

###  1.2. <a name='bitflagoperation'></a>bitflag operation
`ECHO` 是 `c_lflag` 中的一組 flag，決定是否將輸入字元回聲到終端機。假設 `c_lflag` 是 `111`，ECHO 是 `001`，要關閉 `ECHO` 可使用 `c_lflag &= ~ECHO` 指令，將會讓c_lflag 變成 `110`。
以下是關閉 `ECHO` 的完整的範例

    struct termios term;
    
    // Get the current terminal attributes
    tcgetattr(STDIN_FILENO, &term);
    
    // Turn off the ECHO flag
    term.c_lflag &= ~ECHO;
    
    // Set the modified terminal attributes
    tcsetattr(STDIN_FILENO, TCSANOW, &term);
    
    // Now input characters won't be echoed back to the terminal