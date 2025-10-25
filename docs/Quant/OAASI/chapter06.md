# CHAPTER 6 Ratio Call Writing

Ratio writing is a combination of two basic types of call writing: covered call writing, in which one owns the underlying stock and sells a call; and naked call writing.

## 6.1 THE RATIO WRITE

There is a ratio of calls written to stock owned. The most common ratio is the 2:1 ratio, whereby one owns 100 shares of the underlying stock and sells 2 calls.

*Example*: A ratio write is established by buying 100 shares of XYZ at 49 and selling two XYZ October 50 calls at 6 points each.

Table 6-1 and Figure 6-1 summarize the profit and loss potential of this example at October expiration.

TABLE 6-1. Profit and loss at October expiration.

|XYZ Price at Expiration|Stock Profit|Call Price|Profit on Calls|Total Profit|
|--|--|--|--|--|
|30|-$1,900|0|+$1,200|-$700|
|37|-1,200|0|+1,200|0|
|45|-400|0|+1,200|+800|
|50|+100|0|+1,200|+1,300|
|55|+600|5|+200|+800|
|63|+1,400|13|-1,400|0|
|70|+2,100|20|-2,800|-700|

![FIGURE 6-1](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-6-1.png?raw=true)

## 6.4 THE VARIABLE RATIO WRITE (SYNTHETIC SHORT STRANGLE)

Strategist can sometimes write one in-the-money call and one out-of-the-money call against each 100 shares of common. This strategy is called a synthetic short straddle (合成跨式空头), although it is also known by the names variable ratio write (卖出变量比率) or trapezoidal hedge (梯形对冲).

Example: Given the following prices: XYZ common, 65; XYZ October 60 call, 8; and XYZ October 70 call, 3.

A more neutral position can be established by buying 100 XYZ and selling one October 60 and one October 70.

Table 6-5 and Figure 6-3 depict the results from this synthetic short strangle at expiration.

TABLE 6-5. Results at expiration of variable hedge.

|XYZ Price at Expiration|XYZ Profit|October 60 Profit|October 70 Profit|Total Profit|
|--|--|--|--|--|
|45|-$2,000|+$800|+$300|-$900
|50|-1,500|+800|+$300|-400|
|54|-1,100|+800|+300|0|
|60|-500|+800|+300|+600|
|65|0|+300|+300|+600|
|70|+500|-200|+300|+600|
|76|+1,100|-800|-300|0|
|80|+1,500|-$1,200|-700|-400|
|85|+2,000|-1,700|-1,200|-900|

![FIGURE 6-3](https://github.com/iknowledges/BlogImage/blob/main/Option/Figure-6-3.png?raw=true)
