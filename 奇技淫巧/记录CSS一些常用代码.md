* CSS控制超出文本显示省略号

```CSS
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 2; // 这边表示超出2行部分显示省略号
```