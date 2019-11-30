## 练习 1
扫雷    
编写一个拥有三个参数(M, N, p) 的程序：并生成一个M行N列的布尔类型数组，依
据概率p填入“地雷”。在扫雷游戏中，已被占有的一格为“地雷”，未被占有的
一格为“安全”格。用星号“*”表示“地雷”，用半角句号“.”表示“安全”
格，打印出此数组。然后，使用邻近（上、下、左、右及对角线）地雷的数量来
替换安全格的句号并打印结果。

<img src=images/ch02/mine.jpg>

程序接收三个参数，M，N和p，然后生成一个M * N的矩阵，然后每一个cell有p的概率是地雷。生成矩阵后，再计算出每一个cell周围地雷的数量。

 
    #题解：边界条件比较难解决，所以生成n+2的矩阵，多一圈边界。生成随机数和p比较大小。如果产生-1就表示雷

    import random

    def minesweeper(m, n, p):
        borad = [[None] * (n+2) for i in range(m+2)]
        #生成棋盘
        for i in range(1, m+1):
            r = random.random()
            board[i][j] = -1 if r < p else 0 
        #画棋盘
        for i in range(1, m+1):
            for j in range(1, n+1):
                print("*", end=" ") if board[i][j] == -1 else print(".", end=" ")
        #计算格子内的值
        for i in range(1, m+1):
            for j in range(1, n+1):
                if (board[i][j] != -1):
                    for ii in range(i-1, i+2):
                        for jj in range(j-1, j+2):
                            if (board[ii][jj] == -1):
                                board[i][j] += 1
        print()
        for i in range(1, m+1):
            for j in range(1, n+1):
                print("*", end=" ") if board[i][j] == -1 else print(board[i][j], end=" ")
            print()

    minesweeper(5, 10, 0.2)


## 练习2
矩阵中的“0” • 试写一个算法：在一个M行N列的矩阵中，如果查找到一个元素为“0”，将其所在的行和列的元素都设置为“0”。

幻方(Magic Square)
编写一个程序：从命令行读取一个奇数N，打印出N行N列的幻方。   
幻方包含从1到N2的所有数字，每个数字只用一次。幻方的各个行之和、列之和以及对角线之和都相等。       

给一个m×n的矩阵，如果有一个元素为0，则把该元素对应的行与列所有元素全部变成0。
    
    #解题：创建两个1维数组，分别记录行列里出现的0，并记为1。然后俩数组里的1位置 在原数组里置换为0就行。
    空间复杂度为O（m+n）

    # O(m+n) space complexity
    def zero(matrix):
        m = [None] * len(matrix)
        n = [None] * len(matrix[0])
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if (matrix[i][j] == 0):
                    m[i] = 1
                    n[j] = 1
                    
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if (m[i] == 1 or n[j] == 1):
                    matrix[i][j] = 0
    
    matrix = [  [ 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 ],
            [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
            [ 1, 1, 0, 1, 1, 1, 1, 1, 1, 1 ],
            [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
            [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ] ]
    
    zero(matrix)
    for x in matrix:
        print(x, sep=" ")

## 练习3 九宫格
每行每列，对角线加和相等    
<img src=images/ch02/magicsquare.jpg>   

    def s(n):
        for i in range(2, n*n+1):
            ty_now = (r)

    def magic_square(n):
        magic = [[0] * (n) for i in range(n)]
        row = n - 1
        col = n // 2
        magic[row][col] = 1

        for i in range(2, n*n+1):
        #防止越界，余0放到第0排，余1放到第1排
            try_now = (row + 1) % n
            try_col = (col + 1) % n

            if (magic[try_row][try_col] == 0):
                row = try_cow
                col = try_col
            else:
                row = (row-1+n) % n

            magic[row][col] = i
        
        for x in magic:
            print(x, sep=" ")


 ## 练习4 数独
 给个填好的数独，验证是否正确   
<img src="images/ch02/sudoku.jpg" width="200"/> 

   
    matrix = [
        [5,3,4,6,7,8,9,1,2],
        [6,7,2,1,9,5,3,4,8],
        [1,9,8,3,4,2,5,6,7],
        [8,5,9,7,6,1,4,2,3],
        [4,2,6,8,5,3,7,9,1],
        [7,1,3,9,2,4,8,5,6],
        [9,6,1,5,3,7,2,8,4],
        [2,8,7,4,1,9,6,3,5],
        [3,4,5,2,8,6,1,7,9]
    ]

    def sudoku(matrix):
        n = len(matrix)
        result_row = result_col = result_blk = 0

        for i in range(n):
            result_row = result_col = result_blk = 0
            for j in range(n):
                ## check row
                tmp = matrix[i][j]
                if ((result_row & (1 << (tmp-1))) == 0):
                    result_row = result_row | (1 << (tmp-1))
                else:
                    print("row:",i,j )
                    return False
            
                ## check column
                tmp = matrix[j][i]
                if ((result_col & (1 << (tmp-1))) == 0):
                    result_col = result_col | (1<<(tmp-1))
                else:
                    print("col: ", j, i)
                    return False

                ## check block
                idx_row = (i//3) * 3 + j//3
                idx_col = (i%3)  * 3 + j%3
                tmp = matrix[idx_row][idx_col]
                if ((result_blk & (1 << (tmp-1))) == 0):
                    result_blk = result_blk | (1<<(tmp-1))
                else:
                    print("block: ", idx_row, idx_col)
                    return False
        
        return True


## Ex5：旋转数组
给一个n×n的数组，旋转90度。

    def rotate(matrix):
        n = len(matrix)
        result = [[0] * (n) for i in range(n)]
        
        for i in range(n):
            for j in range(n):
                result[j][n-1-i] = matrix[i][j]
        
        for x in result:
            print(x, sep=" ")
    
    matrix = [[i*5+j for j in range(5)] for i in range(5)]
    rotate(matrix)

第二种方法 in-place

    def rotate_in_place(matrix):
        n = len(matrix)
        for layer in range(n//2):
            first = layer
            last = n - 1 - layer
            for i in range(first, last):
                offset = i - first
                top = matrix[first][i]  # save top

                ## left->top
                matrix[first][i] = matrix[last-offset][first]

                ##bottom -> left
                matrix[last-offset][first] = matrix[last][last - offset];

                # right -> bottom
                matrix[last][last - offset] = matrix[i][last];

                # top -> right
                matrix[i][last] = top;  # right <- saved top

        for x in matrix:
            print(x, sep=" ")
    
    matrix = [[i*5+j for j in range(5)] for i in range(5)]
    rotate(matrix)

## EX6 反转字符串
hello  ->  olleh

    # 1
    def reverse(s):
        return s[::-1]

    # 2
    s = "hello"
    r = reverse(s) # O(n)

    # 3
    def reverse2(s):
        l = list(s)
        for i in range(len(l)//2):
            l[i], l[len(s)-1-i] = l[len(s)-1-i], l[i]
        return ''.join(l)

    #4
    def reverse2(s):
        l = list(s)
        begin, end = 0, len(l) - 1
        while begin <= end
            l[begin], l[end] = l[end], l[i]
        return ''.join(l)

## EX7 最长连续子串
给一个只包含0和1的数组，找出最长全是1 的子数组      
Example：
Input：[1,1,0,1,1,1]
Output:3

    def find_consecutive_ones(nums):
        local = maximum = 0
        for i in nums:
            local = local + 1 if i == 1 else 0
            maximum = max(maximum,local)
        return maximum

    nums = [1,1,0,1,1,1,1,0,0,0,0,0,1,1,1,0,0,1]
    result = find_consecutive_ones(nums)

## EX8  最大数
给定一个数组，数组里有一个数组有且只有一个最大数，判断这个最大数是否是其他数的两倍或更大。如果存在这个数，则返回其index，否则返回-1。

    # O(n) time
    # O(1) space
    def largest_twice(nums):
        maximum = second = idx = 0
        for i in range(len(nums)):
            if (maximum < nums[i]):
                second = maximum
                maximum = nums[i]
                idx = i
            elif second < nums[i]:
                second = nums[i]
        return idx if (maximum >= second * 2) else -1


## EX9 查找数组中消失的所有数字
给定一个整数数组，其中1≤a [i]≤n（n =数组大小），一些元素出现两次，另一些元素出现一次。查找未出现在此数组中的[1，n]包含的所有元素。  
Input: [4,3,2,7,8,2,3,1] 

Output: [5,6] 

    # O(n^2)
    def findDisappearedNumbers1(nums):
        result = []
        for i in range(1, len(nums) + 1):
            if (i not in nums):
                result.append(i)
        return result


    # O(n)
    def findDisappearedNumbers2(nums):
        # For each number i in nums,
        # we mark the number that i points as negative.
        # Then we filter the list, get all the indexes
        # who points to a positive number
        for i in range(len(nums)):
            index = abs(nums[i]) - 1
            nums[index] = - abs(nums[index])

        return [i + 1 for i in range(len(nums)) if nums[i] > 0]
##  EX10 加一
给定一个表示为非空数字数组的非负整数，加上一个整数。    
可以假定该整数不包含任何前导零，但数字0本身除外。存储这些数字，以便最高有效数字位于列表的开头。

    def plusOne(digits):
        if len(digits)==0:
            return False
        addCarry=1
        for i in range(len(digits)-1,-1,-1):
            digits[i]+=addCarry
            if digits[i]==10:
                digits[i] = 0
                if i==0:
                    digits.insert(0,1)
            else:
                break
        return digits

### 作业1：寻找枢纽序号
+ 给定一个整数数组，写一个函数返回此数组的枢纽序号。
+ 枢纽序号的定义为：此元素左边元素所有的元素之和与此元素右边所有元素之和相等的元素序号。~
+ 若不存在满足此条件的元素，返回-1。如果有多个元素满足此条件，返回数列最左的枢纽元素的序号。

### 作业2：检验回文结构 
+ 给定一个字符串，检测其是否为回文结构。 
+ 只考虑字母和数字字符，不考虑大小写。
+ 例如：”A	man,	a	plan,	a	canal:	Panama”是回文结构，而”race	a	car”不是回文结构。

