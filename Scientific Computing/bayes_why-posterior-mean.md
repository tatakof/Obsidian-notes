### 3.2.2 Making Decisions

The posterior distribution also provides a formal means for the robust decision making that originally motivated our foray into statistical inference.

As we saw in [Section 1.3.3](https://betanalpha.github.io/assets/case_studies/modeling_and_inference.html#sec:model_based_calibration) a model-based utility function

$$
\begin{alignat*}{6}
U:\; &A \times \Theta& &\rightarrow& \; &\mathbb{R}^{+}&
\\
&(a, \theta)& &\mapsto& &U(a, \theta)&.
\end{alignat*}
$$

isn’t immediately applicable for informing decisions because of the dependence on the unknown model configuration. In a Bayesian analysis, however, the posterior distribution quantifies the relevance of each possible model configuration. Consequently we can compute _expected utilities_ as posterior expectation values,

$$
\overline{U}(a, \tilde{y}) = 
\mathbb{E}_{ \pi_{\mathcal{S}}(\theta \mid \tilde{y}) } [ U(a, \theta) ]
=
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
U(a, \theta).
$$
Note the implicit dependence on the observation due to its influence on the posterior distribution.

The optimal decision _in the context of the available information_ is then given by taking the action that maximizes these expected utilities. This defines the _Bayesian decision making process_
$$
a^{*}(\tilde{y}) = \underset{a \in A}{\text{argmax}} U(a, \tilde{y}).
$$
Mathematically Bayesian decision theory is straightforward and a natural consequence of using probability theory to quantify information. At the same time it can be a conceptual paradigm shift for many because of its explicit consideration of the _uncertainty_ inherent in our inferences. Indeed many common fallacies arise from ignoring inferential uncertainty, or presuming models that poorly approximate the true data generating process. Going through the steps of developing a Bayesian model and computing expected utilities is a powerful way of avoiding common mistakes and facilitating more robust decisions.

For example, let’s say that our goal is to report a point summary of the posterior distribution, θ^, and we want that summary to minimize the squared difference to the best model configuration. In that case the utility function would take the form

$$
U(\hat{\theta}, \theta)
=
- (\hat{\theta} - \theta)^{2}.
$$
and the expected utility would become
$$
\begin{align*}
\overline{U}(\hat{\theta}, \tilde{y}) 
&= 
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
U(\hat{\theta}, \theta)
\\
&= -
\int \mathrm{d} \theta \, \pi_{\mathcal{S}}(\theta \mid \tilde{y}) \,
(\bar{\theta} - \theta)^{2}
\\
&=
- (\hat{\theta} - \mathbb{m}(\tilde{y}))^{2}
- \mathbb{V}{\tilde{y}},
\end{align*}
$$
where m(y~) is the posterior mean and V(y~) is the posterior standard deviation. This expected utility is maximized when we report the posterior mean, which defines the optimal point summary,
$$
\hat{\theta}^{*} = \mathbb{m}(\tilde{y}).
$$
