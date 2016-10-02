# 1. Bias 和 variance 的tradeoff  

* 5th 多項式無法traing出好model
* 跳脫training set以外的資料，也無法確保（sampling bias的概念，太過於依賴training set）  

## Generalization error of H  

* 無法舉一反三
* 遇到training set以外的資料，無法推出對的y
* The G. err of H is its expected error on examples not necessarily in the training set.  
* 有兩種原因：large bias 或 large variance  

## bias = expected generalization error

* 而且是假設在training dataset達到無限筆時，model仍然固有的G. error，才叫做bias
* e.g. linear model 就有large bias
### 會出現`underfit`，就是模型太簡單、根本沒有黏上要模擬的那條f。   
`overfit`則是模型太複雜，完全黏上要模擬的f。不知變通，太過依賴training set。  

## variance = 變異率

* training set 又小又少，讓model可以完全黏上
* 但卻無法反映更廣泛的data，稱為large variance
* 例如：training set很小筆、而且 剛好是「全數略高於平均」的房價，那train出來的model就會黏太死，遇到真正廣泛的資料就慘掉。
* e.g. polynomial 就有large variance  

> 因此，bias和variance需要tradeoff...。

# 2. 進入learning theory  

* First, can we make formal the bias/variance tradeoff that was just discussed?  

* Can we relate error on the training set to generalization error?

* Are there conditions under which we can actually prove that learning algorithms will work well?  

## union bound

## Hoeffding inequality (又稱Chernoff bound)
統計的結果。可以用來大概估出、在r.v.的總數m很多時，擲到正面的機率約是多少。   

## 開始證明一些results in learning theory   

* 考慮binary classification
* label y只有0, 1兩種   

### training error of h的定義  
* 在m筆training examples中，h 錯分類的比例。
* 又稱empirical risk/error   
* 針對training set S的話，會有個下標  

### generalization error的定義  
* this is the probability that, if we now draw a new example (x,y) from the distribution D, h will misclassify it.
* 如果從分佈D的資料中，抽一個example(x,y)，h錯分類的機率  

### PAC 假設  


* Def:  the assumption of training and testing on the same distribution, and the assumption of the independently drawn training examples.
* assumed that the training data was drawn from the same distribution D with which we’re going to evaluate our hypotheses  
* 假設這堆training data是從分佈D之中抽出的，而我們也恰是從這堆分佈D之中估計H  

## ERM 是什麼

* 一個過程，先令h(x) = 1，然後試著minimize training err，並且挑theta
* 經過這過程後，h hat(x) = h theta hat(x)
* 邏輯迴歸，就是一種approximations to empirical risk minimization
* statistical learning用來找alg.的performance bound

## agnostic learning

* the risk e(h) cannot be computed because the distribution P(x,y) is unknown to the learning algorithm
* 若分佈P(x, y)不知長怎樣、則training error無法求出，此情形稱之


## Hypothesis class H  

* class = 一個function set，裡面有一堆functions
* the set of all classifiers considered by a learning alg.
* 一個set of all classifiers over X，他的decision 邊界是linear，這個H如何表示？  
*empirical risk minimization，又可以進一步想成 從這個function H（which is alg. 用來挑classifiers的set）組成的class之中，選出最小的h。

# 3. finite H的情形  

* H is a set of k func. mapping from X to {0 , 1}
* ERM過程，讓h hat被assign 成某個hk，which has 最小的empirical risk
* 希望找G.error of h hat 的 upper bound，也就是 e(h hat)的upper bound。

> e(h) 是 training error
> e hat(h) 是 G.error  

## 如何把G.error和Hoeffding結合？  

### 前置  
* 任挑個hi 屬於 H, 挑個 bernoulli r.v. 為Z，抽一個sample(x,y) ~ D分佈。
* Z代表hi(x) 是否等於 y。
* x vec中，挑一筆input xj，會吐出output yj。
* 因為iid, 所以Zj 和 Z同分佈。
### 觀察  
* 分類錯誤的機率，e(h)，定義剛好就是Z(hj)的期望值。（機率的期望值定義 恰等於 training error的定義）（不會變）
* e hat(h)會變，因為是r.v.的sum然後取mean
* 帶入Hoeffding
* 因為目前只是任挑的那個hi符合，所以利用`Union bound`變成 for all h 屬於 H都符合

### Uniform Convergence  

* 若機率 P >= 1−2k exp(−2γ^2m), we have that e(h) 將會 within γ of eˆ(h) for all h ∈ H

## Sample Complexity

* m, 就是training set的size
* training error will be within γ of generalization error，需要多大的m?

### G.error 跟最好hypothesis的差距

* Define h* = min e(h) to be the best possible hypothesis in H
* define h hat = generalization error
* h hat 至多會比h* 差了 （2 lambda）

## 全部併在一起，求得 G.error 的upper bound

# if H 無限大呢？（set為無限個h）

## shatter

* H shatters S if H can realize any labeling on S.

## VC Dim

* C(H), to be the size of the largest set that is shattered by H

## 怎麼算VC(H)?

* Given the set H of linear classifiers in two dimensions (h(x) = 1{θ0 +θ1x1+ θ2x2 ≥ 0}) 

* 考慮圖上那個 set of three points，（"存在"一個set）
* 發現2^3=8種label標記方式都能找到一條線分隔出來
* 則我們稱 H 可以 shatter size d = 3的set
* 只要size d=3，存在一個 完全可以shatter的 set存在就好。
* d = 4就會不行，會發現「不存在一個d = 4的set，能夠被h(x) shatter」