# pythonData-Structures-and-Algorithms

# 一、算法复杂度    
O(1)、O(log n),O(n),O(n log n),O(n<sup>2</sup>),O(n<sup>3</sup>),O(n<sup>n</sup>)


## 计算规则 
1.基本循环程序：    
 + **基本操作**：复杂度O(1) ,如果是函数调用，将其时间复杂度代入，参与整体时间复杂度计算。   
 + **加法规则**（顺序复合）：两部分（多部分）的顺序复合，复杂度是两部分的加和。     
 T(n)=T<sub>1</sub>(n)+T<sub>2</sub>(n)=O(T<sub>1</sub>(n))+O(T<sub>2</sub>(n)) = O(max()T<sub>1</sub>(n),T<sub>2</sub>(n))

 + **乘法规则**（循环结构）：循环体执行T<sub>1</sub>(n)次，每次执行要T<sub>2</sub>(n)时间，那么：       
 T(n)=T<sub>1</sub>(n) * T<sub>2</sub>(n) = O(T<sub>1</sub>(n)) * O(T<sub>2</sub>(n)) = O(T<sub>1</sub>(n)*T<sub>2</sub>(n))

 + **取最大规则**（分支结构）： 如果算法是条件分支，两个分支的时间复杂性分别为 T<sub>1</sub>(n)和T<sub>2</sub>(n) ，那么：      
 T(n) = O(max()T<sub>1</sub>(n),T<sub>2</sub>(n))

    
## 2.python的计算代价       
+ 时间开销:     
     1. 基本算术运算和逻辑运算是常量时间运算,O(1)   
    2. 组合对象的操作:     
    复制和切片操作O(n),与长度有关   
    list,tuple元素访问和赋值，是O(1)    
    dict操作比较复杂
    3. 字符串看组合对象来定
    4. 创建对象余姚辅助空间和时间，代价都与对象大小有关
    5. 构造新结构，如list、tuple、set等包含n个元素，O(n)   
    6. dict平均复杂度O(1)，最坏情况O（n）

+ 空间开销：    
    1. 一般而言，创建n个元素的数据结构，为O(n)
    2. python中没有预设最大元素个数，会自动扩充存储空间。
    3. 注意python自动存储管理系统的影响


# 二、抽象数据类型ADT
 定义一个抽象数据类型，目的是要定义一类计算对象，它们具有某些特定功能，可以在计算中使用。   
    
 构造有理数抽象数据类型,如下
    
    ADT Rational:               #定义有理数抽象数据类型
    Rational(int num,int den)   #构造有理数num,den
    +(Rational r1, Rational r2)  #r1+r2
    -(Rational r1, Rational r2)  #r1-r2
    *(Rational r1, Rational r2)     #r1*r2
    /(Rational r1, Rational r2)     #r1/r2

日期抽象数据类型:

    ADT Date:
        Date(int year,int month,int day)    #定义年月日
        difference(Date d1,Date d2)         #求d1和d2的日期差
        plus(Date d,int n)                  #日期d后n天的日期
        num_date(int year,int n)            #计算year年第n天的日期

**ADT是一种思想**，也是一种组织程序的技术：     
1. 围绕一类数据定义程序模块
2. 模块的接口和实现分离
3. 在需要实现的时候，采用合理的技术，选择合适的机制，实现这种ADT功能，包括具体的数据表示和操作。

# 三、类
1. 类定义和使用：    

        class <类名>:
            <语句组>
    
    类对象支持两种操作：*属性访问*和*实例化*。

2. 实例对象：初始化和使用       
 使用`__init__`方法完成初始化，第一个参数`self`，其可以有更多的形式参数。

3. 几点说明：   
  + 使用`_`，避免方法名字冲突,比如`_num` 和 `num`
  + 如果在一个方法函数里需要调用在同类里的另一个方法函数，要使用`self.g(...)`，`g()`为 类的另一个函数  
  + 方法函数可以通过`global`和`nonlocal`声明来访问全局变量和函数.
  + 使用`isinstance(obj,cls)`检查类和对象的关系,检查`obj`对象是否是类`cls` 的实例

4. 解调方法和类方法：   
+ 在def行前加`@staticmethod`表示**静态方法**，不需要   `self`参数，通过类名或值为实例对象的变量，以属性引用的方式调用静态函数
+ 在def行前加`@classmethod`表示**类方法**，习惯用`cls`参数名

5. 类定义的作用于规则：
类定义的标识符具有局部作用域，只能在类里使用。外部通过类名字的属性引用方式来访问。

6. 私有变量
+ 用`_`一个下划线开头作为实例对象内部的东西，不应该在类以外访问他们.
+ 用`__`开头，但不结尾，在类外访问不到这个对象。
+ 此外，具有`__add__`的形式表示特殊的魔法方法

7. 继承
在class(object):括号里表示继承的父类，使用`issubclass（cls1，cls2）`来检查cls2是否为cls1 的基类

8.方法查找：
在派生类里查找方法，根据继承关系来找，直到Attribute
Error异常为止。

9.super（）
super.m1()表示调用父类的m1函数，而不是本类的m1.

# 四、线性表
list和tuple采用了顺序表的实现技术。
1. 基于下标的高效元素访问和更新，时间复杂度O(1)
2. 允许任意元素加入，表对象的标识(id值)不变
3. 要求操作为O（1），且保持顺序，只能采用*连续表技术*,表元素保存在一块连续存储区里。
4. 要求能容纳任意多的元素，且保持id不变，采用*分离式实现技术*

list实现策略：建立空表，分配容纳8个元素的存储区，如果区满换一块4倍大的存储区，如果表很大，改变策略，换存储区时容量加倍，目前值时5000。

操 作性质：     
+ len()是O(1)操作
+ 元素访问和赋值，尾端加入和尾端删除（尾端切片删除）为O(1),pop()
+ 一般位置的元素加入、切片替换、切片删除、表拼接（extend）是O(n）,pop(n)指定位置
+ list.reverse()反转操作,O（n）
list.clear()是O（1）去除元素的操作，两种方法
+ 将表的元素计数值设置为0，变为空表。
+ 另外分配一个空表用的存储空间，原存储区有python解释器的存储管理器自动回收。

# 五、字符串

## 1. python字符串相关概念：
 + 字符串的长度：长度为0成为空串，长度为1的字符串。
 + 字符在字符串励按顺序排列，和线性表一样。
 + 字符串相等，说明长度相等，且两串的对应位置的个字符两两相同。
 + 字典序：字符串的一种序关系。就是从左往右看两个穿中下标相同的各对字符，相比大小。
 + 字符串拼接：用+来表示字符串拼接
 + 字串关系：串s1与串s2中的一个连续片段相同，称s1是s2的字串。
 + 前缀和后缀是两种特殊字串

+ python字符串是不变数据类型，python没有字符类型
+ 统一Unicode编码字符集


## 2. 字符串匹配（字串查找）        
+ **朴素的传匹配算法**      
1. 从左往右逐个字符匹配
2. 发现不匹配，到目标穿下一个位置开始匹配
3. 算法复杂性O(m*n)
    
        def navie_matching(t,p):
            m,n = len(p),len(t)
            i,j = 0,0
            while i<m and j<n:
                if p[i] == t[j]:
                    i,j=i+1,j+1
                else:
                    i,j=0,j-i+1
            if i == m:
                return -1

+ **无回溯串匹配算法（KMP）**
详见博客 [KMP算法](https://blog.csdn.net/v_july_v/article/details/7041827)  
KMP时间复杂度:O(m+n)

## 3. 正则表达式
+ ## 元字符（特殊字符）:      
正则表达式包re14个元字符: `.  ^  $  *  +  ?  \  |  {  }  [ ] ( )` 

+ 主要操作：
1. 生成表达式对象: re.compile(pattern,flag=0)
2. 检索 : `re.search(pattern,string,flag=0)`在里检索pattern，返回一个match类型的对象，否则返回None。
3. 匹配: `re.match(pattern,string,flag=0)`检查string是否存在一个与pattern匹配的前缀。成功返回match对象，否则None。
4. 分割：`re.split(pattern,string,maxsplit=0,flasg=0)`以pattern作为分割串，maxsplit指明最大分割数，用0表示要求处理完整个string。返回一个列表。
5. 找出所有匹配串：`re.findall(pattern,string,flags=0)`返回一个表，表中按顺序给出string里与pattern匹配的各个字串
6. 完全匹配: `re.fullmatch(string[,pos,[,endpos]])`
7. 
+ ## 正则表达式构造
1. **字符组描述**：`[...]`与[]里的字符序列里的任意字符匹配。[abc]可以与字符a,b,c匹配。  
    + 区间形式:  [0-9a-zA-Z]
    + 特殊形式:  [^...],^表示对列出的字符组求补
2. **圆点字符(.)**：通配符，匹配所有字符,a..b表示以a开头b结尾的所有字符串       
    + `\d`:匹配十进制数字等价于[0-9]
    + `\D`：匹配所有非十进制数字[^0-9]
    + `\s`:匹配所有空白字符  [\t\v\n\f\r]
    + `\S`:匹配所有非空字符  [^ \t\v\n\f\r] 
    + `\w`:匹配字母数字  [0-9a-zA-Z]
    + `\W`:非字母数字   [^0-9a-zA-Z]
3. **重复**：       
    + 贪婪匹配:用 * 匹配0次或任意多次。

            re.split('[,]*',str)      

    + 非贪婪匹配 ： 用 + 匹配1次或任意多。`\d+`等价于`\d\d*`


4. **可选描述符**:  `?`     
 `a?`要求与a匹配的字符串的0或1次重复匹配

5. **重复次数描述符**: `{n}`        
a{n}与a匹配的串n次重复

6. **重复次数范围**  `{n,m}`
go{2,5}gle,匹配结构为：google,gooogle,goooogle,gooooogle.   
a{n}等价于a{n,n},a?等价于a{0,1}     
*、+、?、{m,n}都采取贪婪匹配规则

7. **非贪婪匹配描述符**:        
    *?,+?,??,{m,n}?表示非贪婪匹配策略，在后面加？
8. **选择**     
    + 选择描述符  `|`       
    表示两种或多种串匹配模式
9. 首位描述符:
    + 行首描述符：以`^`开头的
    + 行尾描述符: 以`$`符号结尾
    + 串首描述符: `\A`开头的
    + 串尾描述符: `\Z`结尾的

10. 单词边界        
`\b`描述单词边界，在实际单词边界位置匹配空串。单词是字母数字的任意连续序列，边界就是非字母数字的或者无字符.     
`\\`表示转义

11. **匹配对象(match对象)**     
mat表示通过匹配得到的一个match对象
+ 取得被匹配的子串:`mat.group()`
+ 在目标串里的匹配位置: `mat.start()`
+ 目标串里的被匹配子串的结束位置: `mat.end()`
+ 目标串里被匹配的区间:  `mat.span()`得到匹配开始位置和结束位置组成的二元组
+ 其他mat.re和mat.string（是数据与访问，不是函数）分别取得match对象的正则表达式和目标串。

12. **模式里的组（group）**     
被匹配的组。


# 六、栈和队列

存取关系:
+ 栈是保证元素后进先出(LIFO结构)
+ 队列先进先出(FIFO结构)

## 1.栈抽象数据类型

        ADT Stack：
            Stack(self)         #创建空栈
            is_empty(self)      #判断栈是否为空，空返回True否则False
            push(self,elem)     #将元素elem加入栈，也常称压入或推入
            pop(self)           #弹出
            top(self)           #取得最后压入栈的元素


python的list及其操作来实现栈：      
**顺序表技术实现栈类**
 + 建立空栈对应于创建空表[]
+ list使用动态顺序表技术（分离式），所以栈不会满
+ 压入元素对应于list.append()
+ 访问栈顶元素 :list[-1]
+ 弹出操作: list.pop()无参，默认弹出表尾元素

        class SStack():
            def __init__(self):
                self._elems= []
                
            def is_empty(self):
                return self._elems == []

            def top(self):
                if self._elems == []:
                    raise StackUnderflow('in SStack.top') 
                return self._elems[-1]

            def push(self,elem):
                drlf._elems.append()

            def pop(self):
                if self._elems == []
                    raise StackUnderflow('in SStack.pop')
                return self._elems.pop()
            
        st1 = SStack()
        st1.push(3)
        st1.push(2)
        while not st1.is_empty():
            print(st1.pop())


栈的链接表实现: 
所有栈操作都在一端进行，采用链接表技术，用表头作为栈顶，用表尾作为栈底。

    class LStak():
        def __init__(self):
            self._top=None

        def is_empty(self):
            return self._top is None
        
        def top(self):
            if self._top is None:
                raise StackUnderflow('in LStack.top')
            return self._top[-1]
        
        def push(self):
            self._top = LNode(elem,self._top)
        
        def pop(self):
            if self._top is None:
                 raise StackUnderflow('in LStack.pop')
            p = self._top
            self._top = p.next
            return p.elem

## 2.栈的应用:

1.括号匹配问题:
三种括号[],(),{}

    def check_parens(text):
        '''括号配对检查函数，text是被检查的正文串
        '''
        parens = "[](){}"
        open_parens="[({"
        
        def parenthese(text):
            """括号生成器，每次调用返回text的下一括号及其位置"""
            i,text_len=0,len(text) 
            while True:
                while i < text_len and text[i] not in parens:
                    i+=1
                if i>= text_len:
                    return
                yield text[i],i
                i+=1
        st = SStack()
        for pr,i in parentheses(text):
            if pr in open_parens:
                st.push(pr)
            elif st.pop() != opposite[pr]:
                print("Unmatching is found at",i,"for",pr)
                return False
        print("All parentheses are correctly matched.")
        return True

## 3.队列   
队列(queue),称为队，先进先出，队列没有位置的概念，只支持默认方式的元素存入和取出。

    ADT Queue:
        Queue(self)         #创建空队列
        is_empty(self)      #判断队列是否为空
        enqueue(self,elem)  #将elem加入队列，入队
        dequeue(self)       #出队
        peek(self)          #最早加入的元素，不删除


**队列类的list实现**    

    class SQueue():
        def __init__(self,init_len=8):
            self._len = init_len        #存储区元素长度
            self._elems = [0]*init_len  #元素存储
            self._head = 0              #表头元素下标
            self._num = 0               #元素个数
        
        def is_empty(self):
            return self._num == 0
        
        def peek(self):
            if self._num == 0:
                raise QueueUnderflow
            return self._elems[self._head]
        
        def dequeue(self):
            if self._num == 0:
                raise QueueUnderflow
            e = self._elems[self._head]
            self._head = (self._head+1) % self._len
            self._num -= 1
            return e
        
        def enqueue(self,e):
            if self._num == self._len:
                self.__extend()
            self._elems[(self._head+self._num) % self._len] = e
            self._num += 1

        def __extend(self):
            old_len = self._len
            self._len *= 2
            new_elems = [0]*self._len
            for i in range(old_then):
                new_elems[i] = self._elems[(self._head + i )% old_len]
            self._elems,self._head = new_elems,0 



# 七、二叉树和树
## 1.二叉树     
是节点的有穷集合。包含一个根节点，其余节点分属两颗不相交的二叉树，分别是根节点的左子树和右子树

+ 路径，数从根节点到任意一个节点都有路径，且唯一。
+ 二叉树是层次结构，树根看作做高层元素，规定跟层数为0。
+ 高度（深度）：根节点高度为0。

## 2.二叉树性质
1. 在非空二叉树第i层至多有 **2<sup>i</sup>** 个节点(i>=0)
2. 高度为h的二叉树至多有 **2<sup>h+1</sup>-1** 个节点(h>=0)
3. 对于任何非空二叉树T，其他节点个数为n<sub>0</sub>，度数为二的节点个数为n<sub>2</sub>，那么n<sub>0</sub> = n<sub>2</sub> +1

## 3.满二叉树，扩充二叉树
1. 满二叉树：二叉树中所有分支节点度数为2，满二叉树是一般二叉树的一个子集。    
满二叉树的节点比分支节点多一个

2. 扩充二叉树：对二叉树T，加入足够多的节点，使其变为满二叉树T2。T2称为T的扩充二叉树。

3.完全二叉树：对一个高度h的二叉树，第0到h-1层的节点都满，而最后一层不满，且节点在左边，空位在右边。     
性质：  
1.n个节点的完全二叉树高度**h=[log<sub>2</sub>n]**     
2.n个节点的完全二叉树，按照从上到下从左到右的顺序从0开始编号，对任意节点i(0<=i<=n-1)都有
+ 序号为0的是根
+ 对i>0，父节点编号为(i-1)/2
+ `2*i+1<n`,左子节点序号为2*i+1,否则无左子节点
+ `2*i+2<n`,右子节点序号为2*i+2，否则无右子节点


## 3.抽象数据类型

    ADT BinTree:
        BinTree(self,data,left,right)       #构造操作，创建二叉树
        is_empty(self)                      #判断是否为空
        num_nodes(self)                     #求二叉树节点个数
        data(self)                          #获取二叉树根存储的数据                     
        left(self)                          #左子树
        right(self)                         #右子树
        set_left(self,btree)                #用btree代替原左子树
        set_right(self,btree)               #用btree代替原右子树
        traversal(self)                     #遍历二叉树中个节点数据的迭代器
        forall(self,op)                     #对二叉树的每个节点进行op操作

## 4.遍历二叉树
+ 深度优先:顺着一条路尽可能往下走，必要时回溯

    + 先根序遍历(DLR顺序)
    + 中根序遍历(LDR)
    + 后根序遍历(LRD)
+ 宽度优先：按层次逐层访问树中各节点。

## 5.二叉树的list实现
二叉树是递归结构
+ 空树用None表示
+ 非空二叉树用包含三个元素的表[d,l,r]表示,d表示根节点元素，l和r两颗子树     
例如：

        ['A',
            ['B',None,None],
            ['C',
                ['D',['F',None,None],
                    ['G',None,None]],
                ['E',['H',None,None],
                    ['I',None,None]]
                ]
        ]


ptython二叉树实现       

    from graphviz import Digraph
    import uuid
    from random import sample

    # 二叉树类
    class BTree(object):
        # 初始化
        def __init__(self, data=None, left=None, right=None):
            self.data = data    # 数据域
            self.left = left    # 左子树
            self.right = right  # 右子树
            self.dot = Digraph(comment='Binary Tree')

        # 前序遍历
        def preorder(self):

            if self.data is not None:
                print(self.data, end=' ')
            if self.left is not None:
                self.left.preorder()
            if self.right is not None:
                self.right.preorder()

        # 中序遍历
        def inorder(self):

            if self.left is not None:
                self.left.inorder()
            if self.data is not None:
                print(self.data, end=' ')
            if self.right is not None:
                self.right.inorder()

        # 后序遍历
        def postorder(self):

            if self.left is not None:
                self.left.postorder()
            if self.right is not None:
                self.right.postorder()
            if self.data is not None:
                print(self.data, end=' ')

        # 层序遍历
        def levelorder(self):

            # 返回某个节点的左孩子
            def LChild_Of_Node(node):
                return node.left if node.left is not None else None
            # 返回某个节点的右孩子
            def RChild_Of_Node(node):
                return node.right if node.right is not None else None

            # 层序遍历列表
            level_order = []
            # 是否添加根节点中的数据
            if self.data is not None:
                level_order.append([self])

            # 二叉树的高度
            height = self.height()
            if height >= 1:
                # 对第二层及其以后的层数进行操作, 在level_order中添加节点而不是数据
                for _ in range(2, height + 1):
                    level = []  # 该层的节点
                    for node in level_order[-1]:
                        # 如果左孩子非空，则添加左孩子
                        if LChild_Of_Node(node):
                            level.append(LChild_Of_Node(node))
                        # 如果右孩子非空，则添加右孩子
                        if RChild_Of_Node(node):
                            level.append(RChild_Of_Node(node))
                    # 如果该层非空，则添加该层
                    if level:
                        level_order.append(level)

                # 取出每层中的数据
                for i in range(0, height):  # 层数
                    for index in range(len(level_order[i])):
                        level_order[i][index] = level_order[i][index].data

            return level_order

        # 二叉树的高度
        def height(self):
            # 空的树高度为0, 只有root节点的树高度为1
            if self.data is None:
                return 0
            elif self.left is None and self.right is None:
                return 1
            elif self.left is None and self.right is not None:
                return 1 + self.right.height()
            elif self.left is not None and self.right is None:
                return 1 + self.left.height()
            else:
                return 1 + max(self.left.height(), self.right.height())

        # 二叉树的叶子节点
        def leaves(self):

            if self.data is None:
                return None
            elif self.left is None and self.right is None:
                print(self.data, end=' ')
            elif self.left is None and self.right is not None:
                self.right.leaves()
            elif self.right is None and self.left is not None:
                self.left.leaves()
            else:
                self.left.leaves()
                self.right.leaves()

        # 利用Graphviz实现二叉树的可视化
        def print_tree(self, save_path='./Binary_Tree.gv', label=False):

            # colors for labels of nodes
            colors = ['skyblue', 'tomato', 'orange', 'purple', 'green', 'yellow', 'pink', 'red']

            # 绘制以某个节点为根节点的二叉树
            def print_node(node, node_tag):
                # 节点颜色
                color = sample(colors,1)[0]
                if node.left is not None:
                    left_tag = str(uuid.uuid1())            # 左节点的数据
                    self.dot.node(left_tag, str(node.left.data), style='filled', color=color)    # 左节点
                    label_string = 'L' if label else ''    # 是否在连接线上写上标签，表明为左子树
                    self.dot.edge(node_tag, left_tag, label=label_string)   # 左节点与其父节点的连线
                    print_node(node.left, left_tag)

                if node.right is not None:
                    right_tag = str(uuid.uuid1())
                    self.dot.node(right_tag, str(node.right.data), style='filled', color=color)
                    label_string = 'R' if label else ''  # 是否在连接线上写上标签，表明为右子树
                    self.dot.edge(node_tag, right_tag, label=label_string)
                    print_node(node.right, right_tag)

            # 如果树非空
            if self.data is not None:
                root_tag = str(uuid.uuid1())                # 根节点标签
                self.dot.node(root_tag, str(self.data), style='filled', color=sample(colors,1)[0])     # 创建根节点
                print_node(self, root_tag)

            self.dot.render(save_path)                              # 保存文件为指定文件


## 6. 优先队列
优先队列存入的每项数据都有附加的数值，表示由优先程度。任何时候的访问和弹出都按照优先级最高的顺序。

list实现优先队列：
    
    class PrioQue:
        def __init__(self,elist=[]):
            self._elems = list(elist)
            self._elems.sort(reverse=True)   #从大到小排列
        
        def enqueue(self,e):
            i = len(self._elems) - 1
            while i>=0:
                if self._elems[i] <=e:
                    i -= 1
                else:
                    break
            self._elems.insert(i+1,e)
        
        def is_empty(self):
            return not self._elems

        def peek(self):
            if self.is_empty():
                raise PrioQueueError("in top)
            return self._elems[-1]

        def dequeue(self):
            if self.is_empty():
                raise PrioQueueError("in pop)
            return self._elems.pop()

## 7.采用树形结构实现优先队列的一种有效技术为堆。
+ 在一个堆中从树根到任何一个叶节点的路径上，节点里存的数据按照优先关系递减。
+ 堆中最优元素必定位于二叉树根节点
+ 位于数不同路径上的元素不必关系优先级

如果是最小元素优先，称为*小顶堆*，反之称为*大顶堆*

**基于堆的优先队列类**

    class PrioQueue:
        def __init__(self,elist=[]):
            self._elems = list(elist)
            if elist:
                self.buildheap()
        def is_empty(self):
            return not self._elems
        
        def peek(self):
            if self.is_empty():
                raise PrioQueueError('in peek')
            return self._elems[0]
        
        #入队操作，主要由siftup完成
        def enqueue(self,e):
            self._elems.append(None)
            self.siftup(e,len(self._elems)-1)

        def siftup(self,e,last):
            elems,i,j = self._elems,last,(last-1)//2
            while i>0 and e < elems[j]:
                elems[i] = elems[j]
                i,j=j,(j-1)//2
            elems[i] = e
        
        def dequeue(self):
            if self.is_empty():
                raise PrioQueueError('in dequeue')
            elems = self._elems
            e0 = elems[0]
            e = elems.pop()
            if len(elems) > 0 :
                self.siftdown(e,0,len(elems))
            return e0

        def dequeue(self,e,begin,end):
            elems,i,j = self._elems,begin,begin*2+1
            while j< end:
                if j+1 < end and elems[j+1] < elems[j]:         
                #elems[j]不大于其他兄弟节点的数据
                    j +=1
                if e< elems[j]:
                    break
                elems[i] = elems[j]
                i,j = j,2*j+1
            elems[i] = e

        def buildheap(self):
            end = len(self._elems)
            for i in range(end//2,-1,-1):
                self.siftdown(self._elems[i],i,end)

堆构造复杂度为O（n），插入弹出操作为O(logn)，最坏情况O(n),其他操作O(1)。


# 八、字典和集合

# 九、排序算法
## 1. 插入排序
平均复杂度O(n<sup>2</sup>)  ,稳定

    def insert_sort(lst):
        for i in range(1,len(lst)):     #开始时片段[0:1]已排序
            x = lst[i]
            j = i
            while j>0 and lst[j-1].key >x.key:
                lst[j] = lst[j-1]       #反序逐个后移元素，确定插入排序
                j -= 1
            lst[j] = x

## 2. 选择排序

    def select_sort(lst):
        for i in range(len(lst)-1):   #只需循环len(lst)-1次
            k=i                         #k是已知最小元素位置
            for j in range(i,len(lst)): 
                if lst[j].key < lst[k].key:
                    k=j
                if i != k:          #lst[k]确定最小的元素，检查是否需要交换
                    lst[i],lst[k] = lst[k],lst[i]

## 3.起泡排序

    def bubble_sort(lst=[]):
        for i in rane(len(lst):
            found = False
            for j in range(1,len(lst)-i):
                if lst[j-1].key > lst[j].key :
                lst[j-1],lst[j] = lst[j],lst[j-1]
                found = True
            if not found:
                break

## 快速排序

    def quick_sort(lst):
        qsort_rec(lst,0,len(lst-1))

    def qsort_rec(lst,1,r):
        if 1 >= r:
            return          #分段无记录或只有一个记录
        i=1
        j=r
        pivot = lst[i]      #lst[i]是初始空位
        while i<j:          #找pivot的最终位置
            while i<j and lst[j].key >= pivot.key:      #用j向左扫描小于pivot的记录
                j-=1
            if i<j:
                lst[i] = lst[j]
                i+=1        #小记录移到右边
            while i<j and lst[i].key <= pivot.key:
                i+=1        #用i向右扫描找大于pivot的记录
            if i<j:
                lst[j] = lst[i]
                j-=1        #大记录移到右边
            lst[i] = pivot  #将pivot存入其最终位置
            qsort_rec(lst,1,i-1)    #递归处理左半区
            qsort_rec(lst,i+1,r)    #递归处理右半区

