# From dotcsv
las redes estan adaptadas para los diferentes tipos de datos que usamos

redes convolucionales son para entender datos espaciales como imágenes
redes recurrentes para entender datos secuenciales como texto

para poder entender que tipo de mejoras nos ofrece un modelo como los transformers, primero tenemos que entender con qué herramientasz contábamos antes para procesamiento de lenguaje natural nlp.  

La pregunta es: 
si yo tengo una frase cualquiera, cómo la analizo? 

dada la naturaleza secuencial de una frase, donde cada palabra ocupa una posicion en el tiempo una tras otra, la estrategia que se ha venido utilizando en el campo del deep learning es la siguiente 

Tomamos una red neuronal normal, y le damos como input la primera palabra.

![[Pasted image 20221001193519.png]]
dotcsv



Interamente esta palabra se procesará multiplicándose capa tras capa con los parámetros aprendidos de la red. 

![[Pasted image 20221001193719.png]]
![[Pasted image 20221001193653.png]]

Esto es lo tipico de siempre, la novedad viene ahora y es que la informacion que ha sido procesada por la red ahora sera agregada a la nueva informacion que introduciremos en el siguiente paso de nuestra secuencia a la siguiente palabra. 
![[Pasted image 20221001193905.png]]

![[Pasted image 20221001194954.png]]
Conectar el output anterior con el input del procesamiento actual es lo que le da el nombre a este tipo de redes: las RNN

esto permite procesar palabras teniendo en cuenta el contexto de lo que vino antes 

El problema de las RNN es vanishing gradients y ... 
Es decir, que cuando se hace este proceso de nutrir el input con el output anterior muchas muchas veces, el peso que tienen durante el entrenamiento las primeras palabras respecto a las ultimas que hemos agregado es menor a efectos practicos. Esto es el equivalente a la red olvidando cuales eran las primeras palabras de nuestra frase y en consecuencia perdiendo informacion relevante. 

![[Pasted image 20221001195803.png]]

Este problema se soluciona con los mecanismos de atención. 

Recuerden que las palabras vienen representadas como vectores numéricos y multidimensionales que capturan gran parte de la información semántica y sintáctica de la palabra que representan y con los que podemos ademas operar matematicamente. 

Vectores cuya dirección en este espaciomultidimensional sea muy parecida, representan conceptos cuyas palabras tambien sean parecidas y se alejaran de aquellas palabras que poco tengan que ver. 

![[Pasted image 20221001200626.png]]


![[Pasted image 20221001200714.png]]


Matematicamente podriamos calcular este angulo para asi estudiar cual es la similitud entre palabras, frases o documentos. 

![[Pasted image 20221001200747.png]]

Nuestro objetivo es buscar una solución a este problema de falta de memoria que esta presente en las RNN, es decir esa falta de conexion que parece que existe entre palabras que estan muy distanciadas, que no nos permiten estudiar cuales son sus relaciones. 

Nuestro objetivo sera que cada una de las palabras de nuestra frase, no importa la distancia que hay entre ellas, pueda estudiar cual es su relacion con cada una de las otras palabras de la frase. 
Estamos buscando cual es la relacion de todas las palabras con todas las palabras. 


que tipo de relaciones esta buscando la red neuronal?
relaciones semanticas, etc... 

la pregunta es como podemos automatizar este proceso de busqueda de relaciones?? la idea es que si esas relaciones existen tendran que ser redes neuronales las que aprendan a encontrarlas. 

Para ello, lo que vamos a hacer sera entrenar a dos redes neuronales diferentes par que con estas palabras dadas como input (mismo input a cada red), aprendan a generar dos vectores distintos. 

![[Pasted image 20221001204635.png]]

Una de las redes generara un vector que servira para identificar las propiedades interesantes que caracterizan a dicha palabra. 
La otra red neuronal generara un vector que servira para describir aquellas propiedades interesantes que esta palabra esta buscando. 

Podemos usar la metafora de una llave y una cerradura. Podriamos decir que con cada palabra de nuestra secuencia, estas dos redes neuronales se van a encargar se van a encargar de aprender a generar una llave y una cerradura, llaves que podran interactuar con el resto de las cerraduras de las otras palabras. 

![[Pasted image 20221001205031.png]]

![[Pasted image 20221001205107.png]]
![[Pasted image 20221001205134.png]]

Tenemos que entender que estas llaves aqui son diferentes a las que solemos utilizar en la vida real, y es que aqui cada llave puede funcionar en distintas cerraduras con mejor o peor resultado. Pero en realidad con las redes neuronales no estamos trabajando ni con llaves ni con cerraduras, sino que con vectores. Tenemos un vector llave y un vector cerradura. 

![[Pasted image 20221001205344.png]]
Y por ser vectores (los llave y los cerradura) podemos opera 









# From hugging face course
## What is NLP?

NLP is a field of linguistics and machine learning focused on understanding everything related to human language. The aim of NLP tasks is not only to understand single words individually, but to be able to understand the context of those words.

The following is a list of common NLP tasks, with some examples of each:

-   **Classifying whole sentences**: Getting the sentiment of a review, detecting if an email is spam, determining if a sentence is grammatically correct or whether two sentences are logically related or not
-   **Classifying each word in a sentence**: Identifying the grammatical components of a sentence (noun, verb, adjective), or the named entities (person, location, organization)
-   **Generating text content**: Completing a prompt with auto-generated text, filling in the blanks in a text with masked words
-   **Extracting an answer from a text**: Given a question and a context, extracting the answer to the question based on the information provided in the context
-   **Generating a new sentence from an input text**: Translating a text into another language, summarizing a text

NLP isn’t limited to written text though. It also tackles complex challenges in speech recognition and computer vision, such as generating a transcript of an audio sample or a description of an image.


Transformer models are used to solve all kinds of NLP tasks

The [🤗 Transformers library](https://github.com/huggingface/transformers) provides the functionality to create and use those shared models. The [Model Hub](https://huggingface.co/models) contains thousands of pretrained models that anyone can download and use. You can also upload your own models to the Hub!

The most basic object in the 🤗 Transformers library is the `pipeline()` function. It connects a model with its necessary preprocessing and postprocessing steps, allowing us to directly input any text and get an intelligible answer:

By default, this pipeline selects a particular pretrained model that has been fine-tuned for sentiment analysis in English. The model is downloaded and cached when you create the `classifier` object. If you rerun the command, the cached model will be used instead and there is no need to download the model again.

There are three main steps involved when you pass some text to a pipeline:

1.  The text is preprocessed into a format the model can understand.
2.  The preprocessed inputs are passed to the model.
3.  The predictions of the model are post-processed, so you can make sense of them.

Some of the currently [available pipelines](https://huggingface.co/transformers/main_classes/pipelines.html) are:

-   `feature-extraction` (get the vector representation of a text)
-   `fill-mask`
-   `ner` (named entity recognition)
-   `question-answering`
-   `sentiment-analysis`
-   `summarization`
-   `text-generation`
-   `translation`
-   `zero-shot-classification`

Let’s have a look at a few of these!

...


##### A bit of Transformer history

Here are some reference points in the (short) history of Transformer models:
![[Pasted image 20221007201055.png]]

The [Transformer architecture](https://arxiv.org/abs/1706.03762) was introduced in June 2017. The focus of the original research was on translation tasks. This was followed by the introduction of several influential models, including:

-   **June 2018**: [GPT](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf), the first pretrained Transformer model, used for fine-tuning on various NLP tasks and obtained state-of-the-art results
    
-   **October 2018**: [BERT](https://arxiv.org/abs/1810.04805), another large pretrained model, this one designed to produce better summaries of sentences (more on this in the next chapter!)
    
-   **February 2019**: [GPT-2](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf), an improved (and bigger) version of GPT that was not immediately publicly released due to ethical concerns
    
-   **October 2019**: [DistilBERT](https://arxiv.org/abs/1910.01108), a distilled version of BERT that is 60% faster, 40% lighter in memory, and still retains 97% of BERT’s performance
    
-   **October 2019**: [BART](https://arxiv.org/abs/1910.13461) and [T5](https://arxiv.org/abs/1910.10683), two large pretrained models using the same architecture as the original Transformer model (the first to do so)
    
-   **May 2020**, [GPT-3](https://arxiv.org/abs/2005.14165), an even bigger version of GPT-2 that is able to perform well on a variety of tasks without the need for fine-tuning (called _zero-shot learning_)
    

This list is far from comprehensive, and is just meant to highlight a few of the different kinds of Transformer models. Broadly, they can be grouped into three categories:

-   GPT-like (also called _auto-regressive_ Transformer models)
-   BERT-like (also called _auto-encoding_ Transformer models)
-   BART/T5-like (also called _sequence-to-sequence_ Transformer models)

We will dive into these families in more depth later on.


## Transformers are language models

All the Transformer models mentioned above (GPT, BERT, BART, T5, etc.) have been trained as _language models_. This means they have been trained on large amounts of raw text in a self-supervised fashion. Self-supervised learning is a type of training in which the objective is automatically computed from the inputs of the model. That means that humans are not needed to label the data!

This type of model develops a statistical understanding of the language it has been trained on, but it’s not very useful for specific practical tasks. Because of this, the general pretrained model then goes through a process called _transfer learning_. During this process, the model is fine-tuned in a supervised way — that is, using human-annotated labels — on a given task.

An example of a task is predicting the next word in a sentence having read the _n_ previous words. This is called _causal language modeling_ because the output depends on the past and present inputs, but not the future ones.


## Transformers are big models

Apart from a few outliers (like DistilBERT), the general strategy to achieve better performance is by increasing the models’ sizes as well as the amount of data they are pretrained on.

![[Pasted image 20221007202227.png]]


Unfortunately, training a model, especially a large one, requires a large amount of data. This becomes very costly in terms of time and compute resources.


## Transfer Learning
_Pretraining_ is the act of training a model from scratch: the weights are randomly initialized, and the training starts without any prior knowledge.
![[Pasted image 20220914191019.png]]

_Fine-tuning_, on the other hand, is the training done **after** a model has been pretrained. To perform fine-tuning, you first acquire a pretrained language model, then perform additional training with a dataset specific to your task. Wait — why not simply train directly for the final task? There are a couple of reasons:

-   The pretrained model was already trained on a dataset that has some similarities with the fine-tuning dataset. The fine-tuning process is thus able to take advantage of knowledge acquired by the initial model during pretraining (for instance, with NLP problems, the pretrained model will have some kind of statistical understanding of the language you are using for your task).
-   Since the pretrained model was already trained on lots of data, the fine-tuning requires way less data to get decent results.
-   For the same reason, the amount of time and resources needed to get good results are much lower.

For example, one could leverage a pretrained model trained on the English language and then fine-tune it on an arXiv corpus, resulting in a science/research-based model. The fine-tuning will only require a limited amount of data: the knowledge the pretrained model has acquired is “transferred,” hence the term _transfer learning_.

![[Pasted image 20220914191251.png]]

Fine-tuning a model therefore has lower time, data, financial, and environmental costs. It is also quicker and easier to iterate over different fine-tuning schemes, as the training is less constraining than a full pretraining.

This process will also achieve better results than training from scratch (unless you have lots of data), which is why you should always try to leverage a pretrained model — one as close as possible to the task you have at hand — and fine-tune it.

## General architecture

### Introduction

The model is primarily composed of two blocks:

-   **Encoder (left)**: The encoder receives an input and builds a representation of it (its features). This means that the model is optimized to acquire understanding from the input.
-   **Decoder (right)**: The decoder uses the encoder’s representation (features) along with other inputs to generate a target sequence. This means that the model is optimized for generating outputs.

![[Pasted image 20220914191823.png]]

**Each of these parts can be used independently**, depending on the task:

-   **Encoder-only models**: Good for tasks that require understanding of the input, such as sentence classification and named entity recognition.
-   **Decoder-only models**: Good for generative tasks such as text generation.
-   **Encoder-decoder models** or **sequence-to-sequence models**: Good for generative tasks that require an input, such as translation or summarization.

## Attention layers

A key feature of Transformer models is that they are built with special layers called _attention layers_. In fact, the title of the paper introducing the Transformer architecture was [“Attention Is All You Need”](https://arxiv.org/abs/1706.03762)! We will explore the details of attention layers later in the course; for now, all you need to know is that this layer will tell the model to pay specific attention to certain words in the sentence you passed it (and more or less ignore the others) when dealing with the representation of each word.

## The original architecture

The Transformer architecture was originally designed for translation. During training, the encoder receives inputs (sentences) in a certain language, while the decoder receives the same sentences in the desired target language. In the encoder, the attention layers can use all the words in a sentence (since, as we just saw, the translation of a given word can be dependent on what is after as well as before it in the sentence). **The decoder, however, works sequentially and can only pay attention to the words in the sentence that it has already translated (so, only the words before the word currently being generated)**. For example, when we have predicted the first three words of the translated target, we give them to the decoder which then uses all the inputs of the encoder to try to predict the fourth word.

To speed things up during training (when the model has access to target sentences), the decoder is fed the whole target, but it is not allowed to use future words (if it had access to the word at position 2 when trying to predict the word at position 2, the problem would not be very hard!). For instance, when trying to predict the fourth word, the attention layer will only have access to the words in positions 1 to 3.

![[Pasted image 20220914192754.png]]

**Note that the first attention layer in a decoder block pays attention to all (past) inputs to the decoder, but the second attention layer uses the output of the encoder. It can thus access the whole input sentence to best predict the current word. This is very useful as different languages can have grammatical rules that put the words in different orders, or some context provided later in the sentence may be helpful to determine the best translation of a given word.**

**The _attention mask_ can also be used in the encoder/decoder to prevent the model from paying attention to some special words — for instance, the special padding word used to make all the inputs the same length when batching together sentences.**

## Architectures vs. checkpoints

As we dive into Transformer models in this course, you’ll see mentions of _architectures_ and _checkpoints_ as well as _models_. These terms all have slightly different meanings:

-   **Architecture**: This is the skeleton of the model — the definition of each layer and each operation that happens within the model.
-   **Checkpoints**: These are the weights that will be loaded in a given architecture.
-   **Model**: This is an umbrella term that isn’t as precise as “architecture” or “checkpoint”: it can mean both. This course will specify _architecture_ or _checkpoint_ when it matters to reduce ambiguity.

For example, BERT is an architecture while `bert-base-cased`, a set of weights trained by the Google team for the first release of BERT, is a checkpoint. However, one can say “the BERT model” and “the `bert-base-cased` model.”

# Encoder models

Encoder models use only the encoder of a Transformer model. At each stage, the attention layers can access all the words in the initial sentence. These models are often characterized as having “bi-directional” attention, and are often called _auto-encoding models_.

The pretraining of these models usually revolves around somehow corrupting a given sentence (for instance, by masking random words in it) and tasking the model with finding or reconstructing the initial sentence.

Encoder models are best suited for tasks requiring an understanding of the full sentence, such as sentence classification, named entity recognition (and more generally word classification), and extractive question answering.

Representatives of this family of models include:

-   [ALBERT](https://huggingface.co/transformers/model_doc/albert.html)
-   [BERT](https://huggingface.co/transformers/model_doc/bert.html)
-   [DistilBERT](https://huggingface.co/transformers/model_doc/distilbert.html)
-   [ELECTRA](https://huggingface.co/transformers/model_doc/electra.html)
-   [RoBERTa](https://huggingface.co/transformers/model_doc/roberta.html)

# Decoder models
Decoder models use only the decoder of a Transformer model. At each stage, for a given word the attention layers can only access the words positioned before it in the sentence. These models are often called _auto-regressive models_.

The pretraining of decoder models usually revolves around predicting the next word in the sentence.

These models are best suited for tasks involving text generation.

Representatives of this family of models include:

-   [CTRL](https://huggingface.co/transformers/model_doc/ctrl.html)
-   [GPT](https://huggingface.co/transformers/model_doc/gpt.html)
-   [GPT-2](https://huggingface.co/transformers/model_doc/gpt2.html)
-   [Transformer XL](https://huggingface.co/transformers/model_doc/transfo-xl.html)

# Sequence-to-sequence models

Encoder-decoder models (also called _sequence-to-sequence models_) use both parts of the Transformer architecture. At each stage, the attention layers of the encoder can access all the words in the initial sentence, whereas the attention layers of the decoder can only access the words positioned before a given word in the input.

The pretraining of these models can be done using the objectives of encoder or decoder models, but usually involves something a bit more complex. For instance, [T5](https://huggingface.co/t5-base) is pretrained by replacing random spans of text (that can contain several words) with a single mask special word, and the objective is then to predict the text that this mask word replaces.

Sequence-to-sequence models are best suited for tasks revolving around generating new sentences depending on a given input, such as summarization, translation, or generative question answering.

Representatives of this family of models include:

-   [BART](https://huggingface.co/transformers/model_doc/bart.html)
-   [mBART](https://huggingface.co/transformers/model_doc/mbart.html)
-   [Marian](https://huggingface.co/transformers/model_doc/marian.html)
-   [T5](https://huggingface.co/transformers/model_doc/t5.html)


# Bias and limitations

If your intent is to use a pretrained model or a fine-tuned version in production, please be aware that, while these models are powerful tools, they come with limitations. The biggest of these is that, to enable pretraining on large amounts of data, researchers often scrape all the content they can find, taking the best as well as the worst of what is available on the internet.
...

When you use these tools, you therefore need to keep in the back of your mind that the original model you are using could very easily generate sexist, racist, or homophobic content. Fine-tuning the model on your data won’t make this intrinsic bias disappear.


# Behind the pipeline
As we saw in [Chapter 1](https://huggingface.co/course/chapter1), this pipeline groups together three steps: preprocessing, passing the inputs through the model, and postprocessing:

![[Pasted image 20220914214900.png]]

## Preprocessing with a tokenizer

Like other neural networks, Transformer models can’t process raw text directly, so the first step of our pipeline is to convert the text inputs into numbers that the model can make sense of. To do this we use a _tokenizer_, which will be responsible for:

-   Splitting the input into words, subwords, or symbols (like punctuation) that are called _tokens_
-   Mapping each token to an integer
-   Adding additional inputs that may be useful to the model

All this preprocessing needs to be done in exactly the same way as when the model was pretrained, so we first need to download that information from the [Model Hub](https://huggingface.co/models). To do this, we use the `AutoTokenizer` class and its `from_pretrained()` method. Using the checkpoint name of our model, it will automatically fetch the data associated with the model’s tokenizer and cache it (so it’s only downloaded the first time you run the code below).

Once we have the tokenizer, we can directly pass our sentences to it and we’ll get back a dictionary that’s ready to feed to our model! The only thing left to do is to convert the list of input IDs to tensors.

You can use 🤗 Transformers without having to worry about which ML framework is used as a backend; it might be PyTorch or TensorFlow, or Flax for some models. However, Transformer models only accept _tensors_ as input. If this is your first time hearing about tensors, you can think of them as NumPy arrays instead. A NumPy array can be a scalar (0D), a vector (1D), a matrix (2D), or have more dimensions. It’s effectively a tensor; other ML frameworks’ tensors behave similarly, and are usually as simple to instantiate as NumPy arrays.

This architecture contains only the base Transformer module: given some inputs, it outputs what we’ll call _hidden states_, also known as _features_. For each model input, we’ll retrieve a high-dimensional vector representing the **contextual understanding of that input by the Transformer model**.

**While these hidden states can be useful on their own, they’re usually inputs to another part of the model, known as the _head_. In [Chapter 1](https://huggingface.co/course/chapter1), the different tasks could have been performed with the same architecture, but each of these tasks will have a different head associated with it.**

# Behind the pipeline

## Preprocessing with a tokenizer
Like other neural networks, Transformer models can’t process raw text directly, so the first step of our pipeline is to convert the text inputs into numbers that the model can make sense of. To do this we use a _tokenizer_, which will be responsible for:

-   Splitting the input into words, subwords, or symbols (like punctuation) that are called _tokens_
-   Mapping each token to an integer
-   Adding additional inputs that may be useful to the model

...

**Once we have the tokenizer, we can directly pass our sentences to it and we’ll get back a dictionary that’s ready to feed to our model! The only thing left to do is to convert the list of input IDs to tensors.**

Transformer models only accept _tensors_ as input. If this is your first time hearing about tensors, you can think of them as NumPy arrays instead. A NumPy array can be a scalar (0D), a vector (1D), a matrix (2D), or have more dimensions. It’s effectively a tensor; other ML frameworks’ tensors behave similarly, and are usually as simple to instantiate as NumPy arrays.

### Model heads: Making sense out of numbers

The model heads take the high-dimensional vector of hidden states as input and project them onto a different dimension. They are usually composed of one or a few linear layers:

![[Pasted image 20221009072108.png]]

The output of the Transformer model is sent directly to the model head to be processed.

In this diagram, the model is represented by its embeddings layer and the subsequent layers. The embeddings layer converts each input ID in the tokenized input into a vector that represents the associated token. The subsequent layers manipulate those vectors using the attention mechanism to produce the final representation of the sentences.

There are many different architectures available in 🤗 Transformers, with each one designed around tackling a specific task. Here is a non-exhaustive list:

-   `*Model` (retrieve the hidden states)
-   `*ForCausalLM`
-   `*ForMaskedLM`
-   `*ForMultipleChoice`
-   `*ForQuestionAnswering`
-   `*ForSequenceClassification`
-   `*ForTokenClassification`
-   and others 🤗




# Models

If you take a look at the _config.json_ file, you’ll recognize the attributes necessary to build the model architecture. This file also contains some metadata, such as where the checkpoint originated and what 🤗 Transformers version you were using when you last saved the checkpoint.

The _pytorch_model.bin_ file is known as the _state dictionary_; it contains all your model’s weights. The two files go hand in hand; the configuration is necessary to know your model’s architecture, while the model weights are your model’s parameters.

## Using a Transformer model for inference

Transformer models can only process numbers — numbers that the tokenizer generates.

Tokenizers can take care of casting the inputs to the appropriate framework’s tensors

Let’s say we have a couple of sequences:

sequences = ["Hello!", "Cool.", "Nice!"]

The tokenizer converts these to vocabulary indices which are typically called _input IDs_. Each sequence is now a list of numbers! The resulting output is:

encoded_sequences = [
    [101, 7592, 999, 102],
    [101, 4658, 1012, 102],
    [101, 3835, 999, 102],
]

This is a list of encoded sequences: a list of lists. Tensors only accept rectangular shapes (think matrices). This “array” is already of rectangular shape, so converting it to a tensor is easy:

import torch

model_inputs = torch.tensor(encoded_sequences)

### Using the tensors as inputs to the model

Making use of the tensors with the model is extremely simple — we just call the model with the inputs:

output = model(model_inputs)

While the model accepts a lot of different arguments, only the input IDs are necessary.

# Tokenizers

Tokenizers are one of the core components of the NLP pipeline. They serve one purpose: to translate text into data that can be processed by the model. Models can only process numbers, so tokenizers need to convert our text inputs to numerical data.

In NLP tasks, the data that is generally processed is raw text.
However, models can only process numbers, so we need to find a way to convert the raw text to numbers. That’s what the tokenizers do, and there are a lot of ways to go about this. The goal is to find the most meaningful representation — that is, the one that makes the most sense to the model — and, if possible, the smallest representation.

## Word-based

The first type of tokenizer that comes to mind is _word-based_. It’s generally very easy to set up and use with only a few rules, and **it often yields decent results.** For example, in the image below, the goal is to split the raw text into words and find a numerical representation for each of them:

![An example of word-based tokenization.](https://huggingface.co/datasets/huggingface-course/documentation-images/resolve/main/en/chapter2/word_based_tokenization-dark.svg)


There are different ways to split the text. For example, we could could use whitespace to tokenize the text into words by applying Python’s `split()` function

There are also variations of word tokenizers that have extra rules for punctuation. With this kind of tokenizer, we can end up with some pretty large “vocabularies,” where a vocabulary is defined by the total number of independent tokens that we have in our corpus.

Each word gets assigned an ID, starting from 0 and going up to the size of the vocabulary. The model uses these IDs to identify each word.

If we want to completely cover a language with a word-based tokenizer, we’ll need to have an identifier for each word in the language, which will generate a huge amount of tokens. For example, there are over 500,000 words in the English language, so to build a map from each word to an input ID we’d need to keep track of that many IDs. Furthermore, words like “dog” are represented differently from words like “dogs”, and the model will initially have no way of knowing that “dog” and “dogs” are similar: it will identify the two words as unrelated. The same applies to other similar words, like “run” and “running”, which the model will not see as being similar initially.

**Finally, we need a custom token to represent words that are not in our vocabulary. This is known as the “unknown” token, often represented as ”[UNK]” or ””. It’s generally a bad sign if you see that the tokenizer is producing a lot of these tokens, as it wasn’t able to retrieve a sensible representation of a word and you’re losing information along the way. The goal when crafting the vocabulary is to do it in such a way that the tokenizer tokenizes as few words as possible into the unknown token.**

**One way to reduce the amount of unknown tokens is to go one level deeper, using a _character-based_ tokenizer.**

## Character-based

Character-based tokenizers split the text into characters, rather than words. This has two primary benefits:

-   The vocabulary is much smaller.
-   There are much fewer out-of-vocabulary (unknown) tokens, since every word can be built from characters.

But here too some questions arise concerning spaces and punctuation

This approach isn’t perfect either. Since the representation is now based on characters rather than words, one could argue that, intuitively, it’s less meaningful: each character doesn’t mean a lot on its own, whereas that is the case with words.

Another thing to consider is that we’ll end up with a very large amount of tokens to be processed by our model: whereas a word would only be a single token with a word-based tokenizer, it can easily turn into 10 or more tokens when converted into characters.

**To get the best of both worlds, we can use a third technique that combines the two approaches: _subword tokenization_.**

## Subword tokenization

Subword tokenization algorithms rely on the principle that frequently used words should not be split into smaller subwords, but rare words should be decomposed into meaningful subwords.

For instance, “annoyingly” might be considered a rare word and could be decomposed into “annoying” and “ly”. These are both likely to appear more frequently as standalone subwords, while at the same time the meaning of “annoyingly” is kept by the composite meaning of “annoying” and “ly”.

Here is an example showing how a subword tokenization algorithm would tokenize the sequence “Let’s do tokenization!“:

![A subword tokenization algorithm.](https://huggingface.co/datasets/huggingface-course/documentation-images/resolve/main/en/chapter2/bpe_subword-dark.svg)

These subwords end up providing a lot of semantic meaning: for instance, in the example above “tokenization” was split into “token” and “ization”, two tokens that have a semantic meaning while being space-efficient (only two tokens are needed to represent a long word). This allows us to have relatively good coverage with small vocabularies, and close to no unknown tokens.

### And more!

Unsurprisingly, there are many more techniques out there. To name a few:

-   Byte-level BPE, as used in GPT-2
-   WordPiece, as used in BERT
-   SentencePiece or Unigram, as used in several multilingual models

You should now have sufficient knowledge of how tokenizers work to get started with the API.

## Loading and saving



## Encoding

Translating text to numbers is known as _encoding_. Encoding is done in a two-step process: the tokenization, followed by the conversion to input IDs.

As we’ve seen, the first step is to split the text into words (or parts of words, punctuation symbols, etc.), usually called _tokens_. There are multiple rules that can govern that process, which is why we need to instantiate the tokenizer using the name of the model, to make sure we use the same rules that were used when the model was pretrained.

**The second step is to convert those tokens into numbers, so we can build a tensor out of them and feed them to the model. To do this, the tokenizer has a _vocabulary_, which is the part we download when we instantiate it with the `from_pretrained()` method. Again, we need to use the same vocabulary used when the model was pretrained.**

## Decoding

_Decoding_ is going the other way around: from vocabulary indices, we want to get a string. This can be done with the `decode()` method as follows:

Note that the `decode` method not only converts the indices back to tokens, but also groups together the tokens that were part of the same words to produce a readable sentence. This behavior will be extremely useful when we use models that predict new text (either text generated from a prompt, or for sequence-to-sequence problems like translation or summarization).

# Handling multiple sequences
_Attention masks_ are tensors with the exact same shape as the input IDs tensor, filled with 0s and 1s: 1s indicate the corresponding tokens should be attended to, and 0s indicate the corresponding tokens should not be attended to (i.e., they should be ignored by the attention layers of the model).

## Longer sequences

With Transformer models, there is a limit to the lengths of the sequences we can pass the models. Most models handle sequences of up to 512 or 1024 tokens, and will crash when asked to process longer sequences. There are two solutions to this problem:

-   Use a model with a longer supported sequence length.
-   Truncate your sequences.

Models have different supported sequence lengths, and some specialize in handling very long sequences. [Longformer](https://huggingface.co/transformers/model_doc/longformer.html) is one example, and another is [LED](https://huggingface.co/transformers/model_doc/led.html). If you’re working on a task that requires very long sequences, we recommend you take a look at those models.

Otherwise, we recommend you truncate your sequences by specifying the `max_sequence_length` parameter:

sequence = sequence[:max_sequence_length]

## Special tokens
The tokenizer added the special word `[CLS]` at the beginning and the special word `[SEP]` at the end. This is because the model was pretrained with those, so to get the same results for inference we need to add them as well. Note that some models don’t add special words, or add different ones; models may also add these special words only at the beginning, or only at the end. In any case, the tokenizer knows which ones are expected and will deal with this for you.

