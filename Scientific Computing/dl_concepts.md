### Zero shot learning

a model that's able to perform well on a variety of tasks without the need for fine-tuning (called _zero-shot learning_)


### Self supervised learning
All the Transformer models mentioned above (GPT, BERT, BART, T5, etc.) have been trained as _language models_. This means they have been trained on large amounts of raw text in a self-supervised fashion. Self-supervised learning is a type of training in which the objective is automatically computed from the inputs of the model. That means that humans are not needed to label the data!

This type of model develops a statistical understanding of the language it has been trained on, but it’s not very useful for specific practical tasks. Because of this, the general pretrained model then goes through a process called _transfer learning_. During this process, the model is fine-tuned in a supervised way — that is, using human-annotated labels — on a given task.


### Causal language modeling
This type of model develops a statistical understanding of the language it has been trained on, but it’s not very useful for specific practical tasks. Because of this, the general pretrained model then goes through a process called _transfer learning_. During this process, the model is fine-tuned in a supervised way — that is, using human-annotated labels — on a given task.


### Pretraining
_Pretraining_ is the act of training a model from scratch: the weights are randomly initialized, and the training starts without any prior knowledge.

![[Pasted image 20220914191018.png]]


### Fine tuning
_Fine-tuning_, on the other hand, is the training done **after** a model has been pretrained. To perform fine-tuning, you first acquire a pretrained language model, then perform additional training with a dataset specific to your task. Wait — why not simply train directly for the final task? There are a couple of reasons:

-   The pretrained model was already trained on a dataset that has some similarities with the fine-tuning dataset. The fine-tuning process is thus able to take advantage of knowledge acquired by the initial model during pretraining (for instance, with NLP problems, the pretrained model will have some kind of statistical understanding of the language you are using for your task).
-   Since the pretrained model was already trained on lots of data, the fine-tuning requires way less data to get decent results.
-   For the same reason, the amount of time and resources needed to get good results are much lower.


