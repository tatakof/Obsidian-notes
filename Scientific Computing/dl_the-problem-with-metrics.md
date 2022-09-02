https://www.fast.ai/2019/09/24/metrics/

(also check 
https://arxiv.org/abs/2002.08512)


Goodhart’s Law states that _“When a measure becomes a target, it ceases to be a good measure.”_ At their heart, what most current AI approaches do is to optimize metrics. The practice of optimizing metrics is not new nor unique to AI, yet AI can be particularly efficient (even _too_ efficient!) at doing so.

This an example of the common phenomenon of having to use proxies: You want to know what content users like, so you measure what they click on. You want to know which teachers are most effective, so you measure their students test scores. You want to know about crime, so you measure arrests. These things are not the same. Many things we _do_ care about can not be measured. Metrics can be helpful, but we can’t forget that they are just proxies.

