##前言
  数学建模使用到过，当时只知道可以用来求解优化问题，最近对人工智能甚有好感，学习过程中又一次见面，准备做一些与人工智能相关的js网页，演示人工智能的威力。一切从遗传算法开始！！！

##遗传算法（参考http://www.ai-junkie.com/ga/intro/gat2.html ）
  为了使用遗传算法解决一个问题，
  
  第一步是对问题的解进行编码（类比染色体），通常编码成01信息  010001010101...
  
  第二步是随机产生一大批“染色体”
  
  第三步是定义一个适应函数（fitness score），用来判断染色体解决问题的适合程度
  
  然后重复以下步骤：
  
    1.从所有染色体中选出两个，每条染色体被选中的概率取决于适应函数的值
    2.根据交叉概率（crossover rate）（一般取0.7）交叉选中的两条染色体中的bit信息
    3.根据突变概率（mutation rate）（通常取很小，不如0.001）改变染色体中bit信息
    重复以上步骤直到产生一群新的染色体
    

##注：
  crossover过程：随机取染色体中一个位置，交换该位置之后的信息
  
  mutation过程：比特信息flip一下（0变1,1变0）

##例子：

用"0-9,+,-,*,/" 这些算符表示某个数。运算规则是从左向右，忽略算符的优先级
  
比如：23 = 6 + 5 * 4 / 2; 75.5 = 5 /2 + 9 * 7 - 5. 

####第一步：编码

0:         0000
1:         0001
2:         0010
3:         0011
4:         0100
5:         0101
6:         0110
7:         0111
8:         1000
9:         1001
+:         1010
-:         1011
*:         1100
/:         1101

比如：
0110 1010 0101 1100 0100 1101 0010 1010 0001 代表
 
6        +        5        *        4         /        2        +       1

如果遇到1110和1111（没用到的），忽略之。

如果遇到

0010 0010 1010 1110 1011 0111 0010
 
2        2        +        n/a     -        7        2

这种情况，忽略不符合规则的部分，规则为：数字->算符->数字->算符->...
因此，以上信息转化为：

  2 + 7
  
####第二步：构造适应函数（fitness function）
这里用信息解码出来，计算得到的值与目标值得差的倒数作为适应函数。因为差距越小适应度越高
（当然，也可以用其他方式）

例如：011010100101110001001101001010100001
 
适应度为： 1/(42-23) 或者说 1/19.

当被除数为0时，说明我们找到了结果。

###程序：construct_number.html



















