# 1 Bias 和 variance 的tradeoff  

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
### `overfit`則是模型太複雜，完全黏上要模擬的f。不知變通，太過依賴training set。  

## variance = 變異率

* training set 又小又少，讓model可以完全黏上
* 但卻無法反映更廣泛的data，稱為large variance
* 例如：training set很小筆、而且 剛好是「全數略高於平均」的房價，那train出來的model就會黏太死，遇到真正廣泛的資料就慘掉。
* e.g. polynomial 就有large variance  

> 因此，bias和variance需要tradeoff...。

# 2 進入learning theory  

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

## Hypothesis class H  

* class = 一個function set，裡面有一堆functions
* the set of all classifiers considered by a learning alg.
* 一個set of all classifiers over X，他的decision 邊界是linear，這個H如何表示？  
*empirical risk minimization，又可以進一步想成 從這個function H（是alg. 用來挑classifiers的set）組成的class之中，選出最小的h。

