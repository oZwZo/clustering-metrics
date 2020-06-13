# methods to determined the number of cluster

[知乎 (*ˉ︶ˉ*)](https://www.zhihu.com/question/59384549?sort=created)



## 1. Elbow method

## 2. Calinski-Harabasz Index

$$k=\arg \max_{k} CH_k$$

$$ CH = \frac{SS_B}{SS_W} \times \frac{N-k}{k-1} $$

in which,  
- $SS_B \text{ : between group variance}$   

- $SS_W \text{ : within group variance}$

### Is it in sklearn ?
YES!!
```python
from sklearn.metrics import calinski_harabaz_score
# usage:
CH = calinski_harabaz_score(data,label)
```
## 3. Silhouette Coefficient 轮廓系数

$$ S_i = \frac{\beta_i - \alpha_i}{\max(\alpha_i,\beta_i)} $$

in which,$\alpha_i$ is the average distancce of sample $i$ to sample of the same class, $\beta_i$ is the that of different class.

the bigger, the better

### Is it in sklearn ?
YES!! 
```python
from sklearn.metrics import silhouettee_score
# usage:
CH = calinski_harabaz_score(X,label,metric='euclidean')
```

## 4. Jump method

$$ d_k = \frac{1}{p} \min E [(X-C_x)^T \Sigma^{-1} (X-C_x)] $$

$$ J_k = d_k - d_{k-1}$$
$$ k = \arg \max_k J_k$$

## 5. Gap statistics

Gap statistics is designed in the idea that the intra-class distribution of a bad clustering will be similar to a random uniform distribution.  

The background distribution $B$ is genrated and is used to compute the average distances to cluster center, which is denoted as $W_{kb}$. After having $W_{kb}$, we compute the average distance of real data to each cluster ceneter ,$W_k$. 

$$ Gap(k)=\frac{1}{B} \sum_{b=1}^B \log(W_{kb}^*) - \log(W_k) $$ 
*note: the cluster center of random datas should be determined by itself with k-means

$$ w' = \frac{1}{B} \sum_{b=1}^B \log(W_{kb}^*) $$

$$ sd(k) = \sqrt{ \frac{1}{B} \sum_{b} (\log(W_{kb}^*) - w')^2} $$

$$ s_k = \sqrt{\frac{1+B}{B} sd(k)} $$

$$ k = \min k $$
$$s.t.   Gap(k) >= Gap(k+1) +s_{k+1}$$

## 6. Davies-Bouldin index



<font size=4>
$$ DB = \frac{1}{k} \sum_{k=1}^k R_i$$
$$ R_i = \max_{j=1...k,i \neq j} R_{ij}$$
$$ R_{ij} = \frac{s_i + s_j}{d_{ij}} $$
$$ d_{ij} = d(v_i,v_j)$$</font>
where $v_i$ is the cluster center for class $i$  
<font size=4>
$$ s_i = \frac{1}{||c_i||} \sum_{x \in c_i} d(x,v_i)$$ </font>
*note $||c_i||$ is scale by the size of class $i$  

in sklearn ? yes !
&nbsp;  
&nbsp;  
## 7. Krzanowski & Lai 
$$ DIFF(k) = (k-1)^{2/p}W_{k-1} - k^{2/p}W_k$$  
&nbsp;
$$ KL(k) = |\frac{DIFF(k)}{DIFF(k+1} |$$
&nbsp;  
&nbsp;  

## Hartigan method
$$H(k) = (\frac{W_k}{W_{k+1}} -1)(n-k-1)$$

&nbsp;  
&nbsp;   