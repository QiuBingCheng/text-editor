# Function Introduction
紀錄程式中使用到的函示。

## Table
| Function  | Library   | Fun Prototype                                                                 | Description                                              |
| --------- | --------- | ----------------------------------------------------------------------------- | -------------------------------------------------------- |
| iscntrl   | ctype.h   | int iscntrl(int n);                                                           | checks whether a character is a control character or not |
| perror    | stdio.h   | void perror(const char *str);                                                 | prints a descriptive error message to stderr             |
| tcsetattr | termios.h | int tcsetattr(int fd, int optional_actions, const struct termios *termios_p); | Changes the attributes associated with a terminal        |
| x         | x         | x                                                                             | x                                                        |
| x         | x         | x                                                                             | x                                                        |


## iscntrl
ASCII codes 0–31 and 127 are all control characters.
https://www.asciitable.com/
