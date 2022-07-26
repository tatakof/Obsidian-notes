### Convergence

By definition, a Markov chain generates samples from the target distribution only after it has converged to equilibrium (i.e., equilibrium is defined as being achieved when p(θ(n))

is the target density). The following point cannot be expressed strongly enough:

-   In theory, _convergence is only guaranteed asymptotically_ as the number of draws grows without bound.
    
-   In practice, _diagnostics must be applied to monitor convergence_ for the finite number of draws actually available.