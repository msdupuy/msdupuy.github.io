+++
title = "Research"
hascode = true
date = Date(2021, 4, 18)
rss = "Short description of the main research results"
+++
@def tags = ["syntax", "code"]
@def maxtoclevel=2


\tableofcontents

# Research interests 

My research work focuses on the numerical and theoretical analysis of numerical models and methods in quantum chemistry, whether they come from solid state physics or molecular chemistry. More precisely, they aim to estimate the errors that have several possible origins
1. modeling errors: the equations which govern quantum chemistry are known - the Schrödinger equation is a high-dimensional linear PDE - which can only be solved for systems reduced to a few electrons. The models (Hartree-Fock or Kohn-Sham) reduce the problem to solving a nonlinear system of PDEs in 3D.
1. discretization errors: for a given model, this error depends on the numerical scheme considered (plane waves, finite elements or finite differences).
1. algorithmic errors: at a fixed model and scheme, the chosen algorithm introduces an error which may be difficult to assess. The nonlinear PDEs in quantum chemistry are solved by fixed point methods. The underlying problem being in the vast majority of cases non-convex, the convergence with respect to a numerical tolerance is unclear.

## Tensor Networks

Tensor Networks (TN) have seen rapid and emerging interests. They aim to give a sparse representation of high-dimensional functions. The first instance of TN was _Matrix Product States_ (MPS) or _Tensor Trains_ that were introduced in the late 90s/early 2000s in physics as _DMRG_ (Density Matrix Renormalization Group) to find the ground-state of statistical models (one-dimensional Hubbard or Heisenberg models). MPS has been used for the $N$-body electronic Schrödinger problem where the question of the optimal topology (or best ordering) is not clear. 

In the contribution, we investigate the behaviour of the singular values of reshapes of a particular class of functions (Slater determinants). The decay of these singular values drives the approximability of the function by an MPS. For this class of functions, if we denote by $(\sigma_j)$ the singular values of the reshaped tensor $\Psi_{\mu_1 \dots \mu_{L/2}}^{\mu_{L/2+1}\dots \mu_L}$, then we show that there are $2^N$ positive singular values, where $N$ is the number of particles and they satisfy
$$
\sigma_1 \sigma_{2^N} = \sigma_2 \sigma_{2^N-1} = \sigma_3 \sigma_{2^N-2} = \cdots = \mathrm{Const}.
$$
The constant is moreover explicit and depends on the ordering of the modes of the tensor. This provides a natural criterion to optimze a TT approximation of the state. 

\figenv{Singular values of the reshaped tensor for different ordering schemes}{slater-std.png}{width:80%;align:center}

### Publication

* Mi-Song Dupuy, Gero Friesecke, [Inversion symmetry of singular values and a new orbital ordering method in tensor train approximations for quantum chemistry](https://epubs.siam.org/doi/10.1137/20M1320122), _SIAM Journal on Scientific Computing_, 2021.


## Solid state physics

In solid-state physics, the periodic boundary conditions motivate a plane-wave discretisation. However because of the Coulomb singularities at the nuclei, the eigenfunctions of the Hamiltonian $-\Delta + V$ have cusps which impedes the convergence. Pseudopotential methods are widely used, where the Coulomb singularities are smoothened. In the PAW method (Projector Augmented-Wave), introduced by Blöchl, the pseudopotential is introduced using an invertible operator acting locally around the nuclei. The PAW equations involve infinitely many terms that are truncated in the numerical treatment which causes a modelling error. This modelling error has been analysed for the one-dimensional model $-\frac{\mathrm{d}^2}{\mathrm{d}x^2} - Z_0 \sum_{k \in \mathbb{Z}} \delta_k - Z_a\sum_{k \in \mathbb{Z}} \delta_{a+k}$ for which explicit formulas of the eigenpairs are available.

Another approach consists in introducing an invertible operator $T$ acting locally around the nuclei. This operator is defined such that it maps smooth functions to functions with cusps satisfying the Kato cusp condition. This operator acts as a preconditonner for a plane-wave discretisation. This method is called the _Variational Projector Augmented-Wave_ and has been analysed for one-dimensional and three-dimensional Hamiltonians.

\figenv{Comparison between a direct discretization and the VPAW method for $-\Delta - \frac{1}{|x-R|}-\frac{1}{|x+R|}$ with periodic boundary conditions}{VPAW_vs_direct.png}{width:80%}

### Publications

* Xavier Blanc, Eric Cancès, Mi-Song Dupuy, [Variational projector augmented-wave method : theoretical analysis and preliminary numerical results](https://link.springer.com/article/10.1007/s00211-019-01082-2), _Numerische Mathematik_, 2019.
* Mi-Song Dupuy, [Projector augmented-wave method: analysis in a one-dimensional setting](https://doi.org/10.1051/m2an/2019017), _ESAIM: M2AN_, 2020.
* Mi-Song Dupuy, [Variational projector-augmented wave method: a full-potential approach for electronic structure calculations in solid-state physics](https://arxiv.org/abs/2002.00512), _Journal of Computational Physics_, 2021.



## Anderson acceleration

Anderson acceleration, also known as DIIS (Direct Inversion of the Iterative Space) in quantum chemistry, aims to accelerate the convergence of fixed-point iteration $x_{k+1} = g(x_k)$. Such fixed-point problems are ubiquitous, and in quantum chemistry come from the Hartree-Fock or Kohn-Sham equations. DIIS is an extrapolation method where the next iterate is built using the knowledge of previous iterates. The DIIS sequence is given by
$$
  (c^{(k)}_i)_{0 \leq i \leq m}  =  \argmin_{\sum c_i = 1} \left\|\sum\limits_{i=0}^m c_i f(x_{k-i})\right\|_2 \quad \text{and} \quad 
  x_{k+1} = g\left(\sum_{i=0}^m c^{(k)}_i x_{k-i}\right),
$$
where $f$ is an _error_ function that locally vanishes only at the solution of the fixed-point problem. A usual choice is $f(x) = x-g(x)$. 

An important parameter in the efficiency of the method is the width $m$ of the history/number of iterates kept. Two variants are considered in our publication:
* one where the history increases until the least-square problem is ill-conditioned. 
* another where teh size of the history is controlled by the ratio of the residuals $\frac{\|f(x_i)\|}{\|f(x_j)\|}$ for $k-m\leq i,j \leq k$. The heuristic behind this variant is to keep the iterates that are the most relevant to build the next one.

For both variants, we prove local linear convergence and superlinear convergence by tuning the DIIS numerical parameters.

\figenv{Comparison between the DIIS variants with fixed depth (FD-DIIS), with restarts (R-DIIS) and adaptive depth (AD-DIIS)}{galactRHFgeneral.png}{width:80%}

### Publication

* Maxime Chupin, Mi-Song Dupuy, Guillaume Legendre, Eric Séré, [Convergence analysis of adaptive DIIS algorithms with application to electronic ground state calculations](https://hal.archives-ouvertes.fr/hal-02492983/document), _ESIAM: M2AN_, (2021).

## Linear response in quantum chemistry

Properties of a molecule in its ground-state perturbed by a time-dependent potential can be approximated in the linear regime (assuming that the perturbation is small) using the Kubo formula. To be more precise, if $\psi_0$ is the ground-state of $H = -\Delta + V$ an operator acting on $L^2(\mathbb{R}^d)$, for some observable $V_\mathcal{O}$ and $\psi(t)$ solution to 
$$
    i\partial_{t} \psi = H \psi + \varepsilon f(t) V_{\mathcal P} \psi , \quad \psi(0) = \psi_{0},
$$
the linear response function $K$ defined by
$$
    \langle  \psi(t), V_{\mathcal O} \psi(t) \rangle = \Big\langle \psi_{0}, V_{\mathcal O}  \psi_{0}\Big\rangle + \varepsilon (K \ast f)(t) + \mathcal{O}(\varepsilon^2),
$$
is given by the Kubo formula
$$
  K(\tau) = -i \theta(\tau) \Big\langle V_{\mathcal O} \psi_{0},  e^{-i (H-E_{0}) \tau} V_{\mathcal P} \psi_{0}\Big\rangle + {\rm c.c.}.
$$
The Fourier transform of $K$ is then
$$
  \widehat K(\omega) = \lim_{\eta \to 0^{+}} \Big\langle \psi_{0}, V_{\mathcal O} \Big(\omega +i\eta - (H-E_0)\Big)^{-1} V_{\mathcal P} \psi_{0}\Big\rangle - \Big\langle \psi_{0},V_{\mathcal P} \Big(\omega +i\eta + (H-E_0)\Big)^{-1} V_{\mathcal O} \psi_{0}\Big\rangle.
$$
The above formula is in practice approximated by taking a positive $\eta$  _and_ by truncating the space to a finite region $(-L,L)^d$. This necessarily yields a singular approximation of the linear response function $\widehat{K}$. In the paper, the regularity of the response function $\widehat{K}$ is determined, depending on the decay of the potential $V$. Moreover, the relationship between $\eta$ and $L$ guaranteeing the convergence of the approximation is shown, supported by numerical experiments.

### Publication

* Mi-Song Dupuy, Antoine Levitt, [Finite-size effects in response functions of molecular systems](https://hal.archives-ouvertes.fr/hal-03145143), 2021.
