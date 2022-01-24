Here's the source for the algorithm 1 in our NeurIPS '21 paper

https://proceedings.neurips.cc/paper/2021/file/ebb71045453f38676c40deb9864f811d-Paper.pdf#page=6

```
%%%% Algorithm section 
\begin{algorithm}[h]
\SetAlgoLined
 \SetKwInOut{Input}{Input}
 \SetKwInOut{HyperParams}{HyperParams}
 \SetKwInOut{Output}{Output}
 \SetKwRepeat{Do}{do}{while}

\begin{table}[H]
\vspace{-3.5mm}
\begin{tabular}{ll}
 \makecell[l]{\textbf{Input:} \\ 
 $\vect{y}_\tau, \tau = 1 \ldots \mathcal{T}$: Time series observations \\ 
    $K$: Number of pure states \vspace{2mm} \\ 
    \textbf{Hyperparameters:} \\ 
    $n$: Window size, \hspace{3mm} $\delta$: Window stride \\
    $\lambda$: Weight on data-fit term \\
    $s$: Variance on prior for $\Thetamb$ \\
    $(\mu_0, \sigma_0)$: Mean, var. of $p(\Thetamb)$ reference dist. \\
    $\eta$: Convergence threshold 
 %\\
%    $(a,b)$: Beta distribution parameters for $p(\gammamb_t)$
    }
    &
    \makecell[l]{\textbf{Output:} \\ 
    $\Thetamb = \left\{\left\{ \mean_k, \cov_k \right\}_{k=1}^K \right\}$: Pure-state emission params \\  
    $\Gammamb= \left\{\xmb_0, \left\{ \vect{\gamma}_t\right\}_{t=1}^T \right\}$: Initial state and innovations  \\
    $\Xmb = \left\{\xmb_t\right\}_{t=1}^{T}$: Wasserstein barycentric state vector \\
    \hspace{28mm} (Computed from $\Gammamb$ via \eqref{eq:StateUpdate}) \\
    $\Hmb = \left\{\vect{w}, \amb_1, \bmb_1 \right\}$: Beta mixture parameters for\\
    \hspace{35mm}  transition dynamics 
    }
 
\end{tabular}
\end{table}

 \For{$t=1,...,T$ \textnormal{where} $T = \lfloor \frac{(\mathcal{T}-(2n+1))}{\delta}\rfloor + 1$} {  
    $\mean_t = \frac{1}{(2n+1)}\sum_{i=1}^{2n+1} \vect{y}_{\delta(t-1) + i}$ \tcp*{Preprocessing of windowed}
    $\cov_t  = \frac{1}{2n}\sum_{i=1}^{2n+1} (\vect{y}_{\delta (t-1)+i}-\mean_{t})(\vect{y}_{\delta (t-1) +i}-\mean_{t})^T$ \tcp*{empirical distributions~~} 
    $\hat{\rho}_t = \mathcal{N}(\mean_t, \cov_t)$ \\
 }
 $c^{(0)} = F\left(\Gammamb^{(0)},\Thetamb^{(0)}, \Hmb^{(0)}, \left\{\hat{\rho}_t\right\}_{t=1}^T \right)$ \tcp*{Cost function $F$ defined in \eqref{eq:Problem2}}
 \Do {$(c^{(n)}-c^{(n+1)}) > \eta$} {
    $\Gammamb^{(n+1)}, \Hmb^{(n+1)} = \argmin_{\Gammamb, \Hmb}  F \left(\Gammamb^{(n)},\Thetamb^{(n)}, \Hmb^{(n)},\left\{\hat{\rho}_t\right\}_{t=1}^T \right)$ \tcp*{Adam}
%    \For{t=1,...,T}  { 
%        $\xmb_t = \left(1- \frac{1}{K}\sum_{k=1}^K \vect{\gamma}_t[k] \right)\xmb_{t-1} + \frac{1}{K}\vect{\gamma}_t$  \tcp*{Computation of state-vector \eqref{eq:StateUpdate}}
%    }
    $\Thetamb^{(n+1)} = \argmin_{\Thetamb}  F\left(\Gammamb^{(n+1)},\Thetamb^{(n)}, \Hmb^{(n+1)},\left\{\hat{\rho}_t\right\}_{t=1}^T\right)$ \tcp*{Riemannian line search} 
    $c^{(n+1)} = F\left(\Gammamb^{(n+1)},\Thetamb^{(n+1)},\Hmb^{(n+1)},\left\{\hat{\rho}_t\right\}_{t=1}^T\right)$ 
 }
\caption{Dynamical Wasserstein Barycenter (DWB) Time-Series Estimation}\label{alg:algorithm}
\end{algorithm}
```
