# Neural-Machine-Translation

Machine translation or MT translates one natural language into another language automatically.
The best thing about machine translation is that it can translate large swatches of text in a very short time. Most of us were inaugurated to machine translation when google arose with the service. 

### What is Neural Machine Translation?
Neural machine translation, or NMT for short, is the use of neural network models to learn a statistical model for machine translation.

The key benefit to the approach is that a single system can be trained directly on source and target text, no longer requiring the pipeline of specialized systems used in statistical machine learning.

### Encoder-Decoder Model
Multilayer Perceptron neural network models can be used for machine translation, although the models are limited by a fixed-length input sequence where the output must be the same length.

These early models have been greatly improved upon recently through the use of recurrent neural networks organized into an encoder-decoder architecture that allow for variable length input and output sequences.

<img src="https://miro.medium.com/max/550/1*BbF4o_uKCRKerXpZiJBlpg.png" alt="encoder-decoder">

Key to the encoder-decoder architecture is the ability of the model to encode the source text into an internal fixed-length representation called the context vector. Interestingly, once encoded, different decoding systems could be used, in principle, to translate the context into different languages.

### Encoder-Decoders with Attention     
Although effective, the Encoder-Decoder architecture has problems with long sequences of text to be translated.

The problem stems from the fixed-length internal representation that must be used to decode each word in the output sequence.

The solution is the use of an attention mechanism that allows the model to learn where to place attention on the input sequence as each word of the output sequence is decoded.

<img src="https://miro.medium.com/max/2000/1*Gv5Im9HOh8yLA9yhxuhM9A.png" alt="attention model">

The encoder-decoder recurrent neural network architecture with attention is currently the state-of-the-art on some benchmark problems for machine translation. And this architecture is used in the heart of the Google Neural Machine Translation system, or GNMT, used in their Google Translate service.
https://translate.google.com

Although effective, the neural machine translation systems still suffer some issues, such as scaling to larger vocabularies of words and the slow speed of training the models. There are the current areas of focus for large production neural translation systems, such as the Google system.
