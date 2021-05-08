@def title = "Codes"
@def hascode = true
@def rss = "Publicly available codes by Mi-Song Dupuy"
@def rss_title = "Codes"
@def rss_pubdate = Date(2019, 5, 1)

@def tags = ["syntax", "code", "image"]

# Codes

## Tensor-Train-Julia 

[Tensor-Train-Julia](https://github.com/msdupuy/Tensor-Train-Julia) is a Julia package implementing the basic tensor train routines: TT decomposition, ALS/MALS algorithm to solve linear equation or eigenvalue problems. It is also possible to compute ground-states of operators of the form 
$$
H = \sum_{i,j} h_{ij} (a_i^\dagger a_j + \mathrm{c.c.}) + \sum_{i,j,k,l} V_{ijkl} (a_i^\dagger a_j^\dagger a_l a_k + \mathrm{c.c.}) 
$$
for given $h,V$. Different ordering schemes are implemented namely the Fiedler order and the best prefactor order. 

### References

1. Barcza, G., Legeza, Ö., Marti, K. H., & Reiher, M. (2011). Quantum-information analysis of electronic states of different molecular structures. Physical Review A, 83(1), 012508.
1. Dupuy, M. S., & Friesecke, G. (2021). [Inversion symmetry of singular values and a new orbital ordering method in tensor train approximations for quantum chemistry](https://arxiv.org/abs/2002.07459). SIAM Journal on Scientific Computing, 43(1), B108-B131.

## PAW-VPAW

[PAW-VPAW](https://github.com/msdupuy/paw-vpaw) is a Julia code to solve by a plane-wave discretisation linear eigenvalue problems of the form
$$
(-\Delta +V)\psi = E\psi, \quad \text{with periodic b.c.}
$$
where $V$ has Coulomb singularities. The PAW and VPAW methods are implemented to compare their performances against a direct discretisation. This code is not being maintained anymore.

### References
1. Blöchl, P. E. (1994). Projector augmented-wave method. Physical review B, 50(24), 17953.
1. Dupuy, M. S. (2020). [Variational projector-augmented wave method: a full-potential approach for electronic structure calculations in solid-state physics](https://arxiv.org/abs/2002.00512). arXiv preprint arXiv:2002.00512.