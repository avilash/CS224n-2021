#### A  
$y_w = 0 \text{ for all } w \text{ expect } w=o$

---

#### B  
$A_i =  u_i^Tv_c$  
$A = U^Tv_c$  
$P = softmax(A)$  
$L = -y*log(P)$  

[Derivative of softmax and cross entropy](https://deepnotes.io/softmax-crossentropy)  
$dP_i/dA_i = 
\begin{cases} 
    P_i(1-P_i) & \text{if }i=j, \\ 
    -P_i(P_j) & \text{if }i\not=j, \\ 
\end{cases} 
$

$dL/A_i = -\sum_k \frac{y_k}{P_k} * \frac{dP_k}{dA_k}$  
$dL/A_i = -y_i(1-P_i)-\sum_{k\not=i} y_kP_i$  
$dL/A_i = P_i - y_i$   
$dL/A = P - y$  
$dL/v_c = U(P - y)$ 

---

#### C  
$dL/du_i = dL/dA_i * dA_i/du_i$  
$dL/du_i = (P_i - y_i)v_C^T$  

---

#### D  
$dL/U = (dL/dA)^T v_c^T$  
$dL/U = (P - y) v_c^T$  

---

#### E  
$dσ(x)/dx = σ(x)(1-σ(x))$

---

#### F  
$A_i =  u_i^Tv_c$  
$L = -log(σ(A_o)) + \sum_k -log(σ(-A_k))$

$dL/dA_i =  -\frac{σ(A_i)(1-σ(A_i))}{σ(A_i)} = σ(A_i)-1$  

$dL/du_o = dL/dA_o*v_c^T = (σ(u_o^T v_c)-1)v_c^T$  
$dL/du_k = dL/d(-A_k)*v_c^T = (1-σ(-u_k^T v_c))v_c^T$  
$dL/v_c = dL/dA_o*u_o^T + \sum_k dL/d(-A_k)*u_k^T$  
$dL/v_c = (σ(u_o^T v_c)-1)u_o^T + \sum_k (1-σ(-u_k^T v_c))u_k^T$

---

#### G  
$count = \text{number of times } u_k \text{ appears in sampled window}$  
$dL/du_k = dL/d(-A_k)*v_c^T*count = (1-σ(-u_k^T v_c))v_c^T*count$ 

---

#### H  
$dL_{sg}(v_c, w_{t-m}, ... w_{t+m}, U)/dU = 
\sum_{\substack{-m \leq j \leq m \\ j \ne 0}} dL(v_c, w_{t+k}, U)/dU$  
$dL_{sg}(v_c, w_{t-m}, ... w_{t+m}, U)/dv_c = 
\sum_{\substack{-m \leq j \leq m \\ j \ne 0}} dL(v_c, w_{t+k}, U)/dv_c$  
$dL_{sg}(v_c, w_{t-m}, ... w_{t+m}, U)/dv_{w, w \neq c} = 0$

---