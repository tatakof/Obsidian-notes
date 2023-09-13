
### Word embedding
As computers are only capable of understanding numerical values, a data transformation process that converts alphabetical values (textual data) into numerical values must be applied first at the beginning of most transformer models. In the deep learning world, this process is called word embedding. Word embeddings will represent each word in the form of a real-valued vector that encodes the word's meaning such that the words closer in the vector space are expected to be similar in meaning.


### Frozen parameters
In a NN, parameters that don't compute gradients are usually called **frozen parameters**. It is useful to "freeze" par of your model if you know in advance that you won't need the gradients of those parameters (this offers some performance benefits byreducing autograd computations)

In finetuning, we freeze most of the model and typically only modify the classifier layers to make predictions on new labels. 


### Inductive bias (also known as learning bias)
The inductive bias of a learning algorithm is the set of assumptions that the learner uses to predict outputs of given inputs that it has not encountered. 

In ML, one aims to construct algorithms that are able to learn to predict a certain target output. To achieve this, the learning algorithm is presented some training examples that demonstrate the intended relation of input and output values. Then the learner is suppoosed to approximate the correct output, even for examples that have not been shown during training. Without any additional assumptions, this problem cannot be solved since unseen situations might have an arbitrary output value. The kind of necessary assumptions about the nature of the target function are subsumed in the phrase *inductive bias*. 

A classical example of an is Occam's razor, assuming that the simplest consistent hypothesis about the target function is actually the best. Here *consistent* means that the hypothesis of the learner yields correct output for all of the examples that have been given to the algorithm.



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


### Tokenizer
Like other neural networks, Transformer models can’t process raw text directly, so the first step of our pipeline is to convert the text inputs into numbers that the model can make sense of. To do this we use a **_tokenizer_**, which will be responsible for:

-   Splitting the input into words, subwords, or symbols (like punctuation) that are called _tokens_
-   Mapping each token to an integer
-   Adding additional inputs that may be useful to the model

Once we have the tokenizer, we can directly pass our sentences to it and we’ll get back a dictionary that’s ready to feed to our model! The only thing left to do is to convert the list of input IDs to tensors.


### Encoding

Translating text to numbers is known as _encoding_. Encoding is done in a two-step process: the tokenization, followed by the conversion to input IDs.

### Tokens

As we’ve seen, the first step is to split the text into words (or parts of words, punctuation symbols, etc.), usually called _tokens_. There are multiple rules that can govern that process, which is why we need to instantiate the tokenizer using the name of the model, to make sure we use the same rules that were used when the model was pretrained.

