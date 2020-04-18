# 基本去随机化技术

## 枚举

如果总是能缩减随机算法的随机bit到O(log(n))个，那么存在确定性算法，能够把随机算法在几乎相同的性能下去随机化
（去随机化算法的最坏时间复杂度为去随机化之前的多项式倍）。

## Nonconstructive/Nonuniform Derandomization

只要随机算法的失误率小于 2^n，那么总存在固定的序列r(n)，使得其能在多项式时间内运行。 这个方法比枚举好的地方在于：只要固定了rn，那么就有多项式时间算法，问题在于找到rn不知道需要多少时间。

## Nondeterminism

P=NP -> P=BPP，所以NP更厉害些；非确定性可以实现去随机化

## 条件期望

以上3个方法虽然通用，但是是否存在有效的多项式时间算法实现是一个问题

对于所有的用了m(n)个随机位的算法，其随机的过程都可以看作为一个 深度为m(n)的二叉树，每一条路径表示一个结果，在随机化算法中，我们知道大多数路径都能给定好的结果

等价地，我们试图找出逐位的不错的随机序列，给定序列（r1,r2...rn），那么P(r1,r2...rn):=

通过平均，我们总有P(r1,r2...rn,rn+1)≥P(r1,r2...rn) 通过最大化rn+1，由此P(r1,r2,...,rm) ≥ P(r1,r2,...,rm−1) ≥ ··· ≥ P(r1) ≥ P(Λ) ≥ 2/3

要实现这个方法，我们需要 确定性地计算P(r1,r2...ri)，这个可能不可行

## Pairwise Independence

###  Pairwise Independent Hash Functions

Some applications require pairwise independent random variables that take values from a larger range.

比如我们想要 N=2^n 个随机变量，其中每一个随机变量都是均匀分布在{0,1}^m,M=2^m，那么朴素的做法是重复上述说法，每个随机变量m次，那么就用到了随机位 mn=log Mlog N个

如果M不是关于N的常数，那么这个就不是log N的时间复杂度，我们知道这样的序列等价于在 [M]^n中选取样本，或者等价地，是一个hash映射f:[N]->[M]

我们可以通过构造一个这样的映射实现去随机化：

构造一族映射f:[N]->[M]

随机取一个映射，如果这样的映射：

1. 映射的结果彼此独立

2. 不同的元的映射不同

上述两条件等价于，任取[N]中两个不同的元，任取一个映射，其映射到[M]上的任意两个元的概率是 1/M^2 （两两独立性质）

这样的hash函数族被称为 explicit 如果任取[N]中一个元和一个函数h，有h(x)可以在polt(log M,log N)中计算，这个函数族也称为strongly 2-universal hash functions

构造 ：
### pairwise independent hash functions from linear maps

对于有限域F，若函数族 H = {h_{a,b}:F->F}，其中h_{a,b}=ax+b

这样构造的函数族是两两独立的，此构造用了 2log |F| 个random bit， 

定理：对于一个显示的两两独立的映射族，从{0,1}^N到{0,1}^M的随机选取的映射H_{n,m}，找到其的所需要的random bit 为 max{m,n} + m个

使用Hash Tables可以对于于这样的构造，在许多情况下，两两独立或者k-wise独立够用了，完全随机则需要不切实际的存储空间


假设我们有一个BPP算法，其失误的概率为常数，我们想要削弱其犯错概率到2^(-k)， 通过切比雪夫不等式，我们知道用O(k)个随机位可以做到，如果算法本身用了m个随机位

那么为了削弱失误概率我们需要O(mk)个随机位
                                    Repetitions       Random Bits
Independent Repetitions                 O(k)              O(km)
Pairwise Independent Repetitions        O(2k)             O(m + k)

刚刚提到的来两两独立的构造自然地可以拓展到k-wise独立

函数族的定义类似延拓，两两独立的构造：一个线性函数，在k-wise独立的情景下就是一个k-1次多项式

choose a random function from H takes k · max{n,m} random bit





