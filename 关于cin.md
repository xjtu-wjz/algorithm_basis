#快速cin

正常情况下由于C++对输入输出有限制流，cin 的速度较scanf慢，可加入以下语句加速。

```
std::ios::sync_with_stdio(false);
```

然后再使用cin则不会读入超时。

或者与0同步绑定：
cin.tie(0)；
同样的，cout也可以和0捆绑，从而加速输出。

#自动判断输入的数据类型 
在此例如判断是否输入的是char还是int

>int i; 
>char c;
>cin>>i;
>if(cin)        //判断输入是否合法，不合法则进行之后的操作
>{
>......             //后续的对i的操作
>}
>else
>{
>	cin.clear();
>	cin>>c;
>	......       //之后的对c的操作
>}

