<!-- vscode-markdown-toc -->
* 1. [Data Types](#DataTypes)
	* 1.1. [Strings](#Strings)
* 2. [Operation](#Operation)
	* 2.1. [bitflag operation](#bitflagoperation)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

# C Language Features

##  1. <a name='DataTypes'></a>Data Types
###  1.1. <a name='Strings'></a>Strings
C語言中的字串就是字元的集合，以空字符（null character，`'\0'`）结尾。

    char str[] = "Hello, world!"; // 字符串以空字符结尾
    printf("%s\n", str); // 輸出字串

如果字串是動態分配的，可以使用 `strlen` 獲取字串長度，並在分配記憶體時多分配一個 byte 來儲存空字符。

    char *str = malloc(strlen("Hello, world!") + 1); 
    strcpy(str, "Hello, world!"); 
    printf("%s\n", str); 
    free(str);

##  2. <a name='Operation'></a>Operation
###  2.1. <a name='bitflagoperation'></a>bitflag operation
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