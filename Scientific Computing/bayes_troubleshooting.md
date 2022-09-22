## 2.2 Computer, Enhance
**If our initial model proves adequate then we have no need of going further. In the more realistic situation where our initial model proves to be inadequate, then we have to address the revealed inadequacies one way or another. This can mean improving our model, but it could also mean changing the experiment or our inferential goals entirely.**

### Issues with Question One: Domain Expertise Consistency

If we learn that our model is not consistent with our domain expertise then we have to modify the aspects of our model in conflict. This often requires more careful consideration of the prior model, but occasionally it can require modifying the observational model as well. For example an observational model violating known constraints often enough might have to changed to explicitly enforce those constraints.

The identification of exactly where to change our model is facilitated by well-chosen summary functions in prior pushforward and prior predictive checks. **Investment in the design of these summary functions rarely goes unrewarded, if not in the current analysis then in future analyses.**

### Issues with Question Two: Computational Faithfulness
Insufficient computational tools can be more challenging to address.

If we are proficient in the current algorithms being used then we can consider more sophisticated configurations and implementations of that algorithm. Alternatively we can reparameterize our model configuration space to implicitly reconfigure the algorithm [[10](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#ref-Betancourt:2019)]. At some point we might have to consider new algorithms entirely.

**By investigating the posterior fits to many simulated observations we might be able to identify the structure of the data, and hence the structure of the simulated true model configuration, that frustrates the current algorithm.** **If, and only if, these model configurations are in conflict with our domain expertise then we can then consider suppressing the pathological behavior with a stronger prior model. We have to take care here, however, as we don't want to rationalize erroneous domain expertise just to ameliorate computational issues. The computational issues might trigger more precise domain expertise, but they shouldn't rationalize fantasies.**

Sometimes computational issues cannot be resolved and instead demonstrate that we are not equipped with the resources needed to tackle the presumed analysis. In that case we might have to consider less ambitious inferential goals, and the simpler, more-computationally-friendly models they require.

### Issues with Question Three: Inferential Adequacy
When model calibration indicates that we are unlikely to meet our inferential goals we need to consider ways to improve our inferences, or weaken the inferential goals entirely.

**Inferences underperform when they cannot exploit enough information about the system being analyzed**. **The only way we can improve our inferences, then, is to incorporate more information into our model**.

**One critical source of information is the domain expertise encoded in the prior model. By reevaluating our domain expertise we might be able to build a more precise prior model that captures more information**. **This is especially critical if we can use our calibrations to identify for what information our inferences are most starved to guide our prior refinement**.

**The other source of information is the observations as encoded in the realized likelihood functions. In particular we can always improve our inferences by considering more elaborate or more precise experimental probes, collecting more data or possibly different kinds of data to better inform the relevant aspects of the true data generating process.** **New data that complements an existing measurement can be particularly effective. For example measurements with the latent phenomena removed or suppressed can help to inform the behavior of the experimental probe or the latent environment, breaking degeneracies that limit how well we can resolve the latent phenomena in the full measurement.**

Finally we have to acknowledge that a better model is not always sufficient to obtain the desired inferences. **Sometimes our initial inferential goals are just too ambitious, and our experiments are too insensitive to the phenomena of interest.** In these cases we might have to use the calibration studies to suggest more realistic goals for the current experiment design.

### Issues with Question Four: Model Adequacy

Finally, if we learn that our model isn't capturing the relevant features of the true data generating process then **we need to _expand_ its boundaries in those relevant directions.**

**Model expansion gives us a sequence of _nested models_, or nested subsets in the space of all possible data generating processes,**
$$
\mathcal{S}_{1} \subset \mathcal{S}_{2} \subset \mathcal{S}_{3} \subset \mathcal{P},
$$
that hopefully move closer and closer to the true data generating process, at least in the relevant directions.

![[Pasted image 20220919111357.png]]

**This iterative model development can be compared to the basic scientific method where we operationalize the vague “compare hypothesis predictions to experiment" and "form new hypotheses" with posterior retrodictive checks identifying inconsistencies and our aspirational model motivating new hypotheses**. That said the proper implementation of the scientific method is a contentious subject spanning philosophy, science, and statistics...so maybe it's best to avoid such comparisons.

We don't want to add complexity arbitrarily, however, lest we end up with an unwieldy model that isn't even adequate for our inferential goals. Instead **we want to expand our model carefully, prioritizing the features that could alleviate the most extreme observed deviations**.

Fortunately the context of the aspirational model, and the summary statistics it motivates, helps to guide this prioritization and make it less overwhelming. **In particular posterior retrodictive checks based on interpretable summary statistics not only identify potential problems but also suggest the structure needed to resolve those problems. We can then focus on the summary statistics that reveal the strongest deviations, laying a deliberately path through the aspiration model that takes us from our initial model towards the true data generating process.**

**If deviations aren't strong enough to motivate an expansion we can also take a closer look by collecting more data or complementary data that induces more precise inferences. This allows us to not only better resolve the latent phenomenology but also any deficiencies of the current model, and hence motivate more principled improvements.**


### Fitting a model
With an algorithm locked and loaded we can proceed to _fit_, or estimate expectation values with respect to, the posterior distributions induced from each of our simulated observations,


$$
\pi_{\mathcal{S}}(\theta \mid \tilde{y}).
$$

### Step Ten: Algorithmic Calibration

By fitting the entire ensemble of posterior distributions we can probe the utility of our chosen algorithm and help answer [Question Two: Computational Faithfulness](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_two), at least within the context of the model assumptions.

For example if the designated computational method features self-diagnostics, such as R^ for Markov chain Monte Carlo in general and divergences for Hamiltonian Monte Carlo in particular, **then we can look for failed diagnostics across the distribution of posterior fits.** **Even if our chosen method doesn't have its own diagnostics we can evaluate its performance by performing simulation-based calibration**.

Failures indicate that we may need return to [Step Eight](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:config-algo) and improve the tuning or implementation the chosen computational method, or select another method altogether.

**We can also correlate failed fits with the corresponding simulated observations and model configurations.** **This can potentially identify poorly-identified likelihood functions that result in posterior distributions pathological to the computational method being used.** The propensity for such poor behavior can then be ameliorated by returning to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) and incorporating additional domain expertise or even returning to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) and considering new experimental designs that might result in more manageable likelihood functions.

**Requirements:** Statistical Expertise


### 3.0.1 Step Eleven: Inferential Calibration

Once we trust the faithfulness of our reconstructed posterior distributions we can consider the breadth of inferences they provide to help answer [Question Three: Inferential Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_three).

**In general we can always consider the distribution of posterior z-scores against posterior contractions to identify common pathologies in our inferences. If there are indications of undesired behavior, such as overfitting or non-identifiability, then our model may not be sufficient.**

**When an explicit decision-making process has been established we can also calibrate the performance of this process by constructing the distribution of utilities over our simulated Bayesian ensemble**. **For example if a discovery claim is to be made then we might compute the corresponding false discovery rates and true discovery rates within the context of our model.** If these utilities are not satisfactory then we have to consider a more informed model or maybe even a different decision-making process.

In either case we might have to return to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) to consider an improved experimental design or tempered scientific goals. Sometimes we may only need to return to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) to incorporate additional domain expertise to improve our inferences.

### Step Thirteen: Diagnose Posterior Fit

**We have to be careful, however, as the algorithmic calibration won't be relevant to the observed data if our model isn't close enough to the true data generating process.** Consequently we need to be careful to check any diagnostics of our computational method on the fit of the observed data as well.

**If any diagnostics indicate poor performance then not only is our computational method suspect but also our model might not be rich enough to capture the relevant details of the observed data. At the very least we should return to [Step Eight](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:config-algo) and enhance our computational method.**

### Step Fourteen: Posterior Retrodictive Checks

To really get a handle on [Question Four: Model Adequacy](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:question_four) we have to perform careful posterior retrodictive checks for each of our summary statistics.

**If there are indications of problems that we already suspected in our aspirational model then we can return to [Step Four](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:model-development) and augment the model to account for the observed deviant behavior.** **When the behavior is more surprising, however, then we really should go all the way back to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) and reconsider our conceptual analysis of the experiment to motivate principled model improvements. If the indications are weak then we can also return to [Step One](https://betanalpha.github.io/assets/case_studies/principled_bayesian_workflow.html#sec:conceptual) to consider expanding our observation to improve our inferences and better resolve the potential deviation.**

**In order to avoid biasing our model development by overfitting to the observed data we have to be careful with what information we take with us when we start a new iteration of the workflow**. **Specifically we want the _qualitative failure_ of a posterior retrodictive check to motivate model expansion, not the _quantiative features of the observed data itself_. In other words a posterior retrodictive check should serve only to trigger our domain expertise, and our domain expertise should then be solely responsible for the continued model development. The more disciplined we can be here the more less vulnerable our model development will be to overfitting.**
