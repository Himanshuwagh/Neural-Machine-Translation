## Neural Machine Translation Using Sequence to Sequence Model

Machine translation is one of earliest and challenging task of computers due to fluidity of human language. It is simply an automatic translation of text from one language to another.

The Encoder-Decoder LSTM is a recurrent neural network designed to address sequence-to-sequence problems, sometimes called seq2seq.

Sequence-to-sequence prediction problems are challenging because the number of items in the input and output sequences can vary. For example, text translation and learning to execute programs are examples of seq2seq problems.

<img src="https://humboldt-wi.github.io/blog/img/seminar/is1920_group9/encdec_1.png" alt="Enocder-Decoder Model">

#### Encoder:-        
Encoders can be any network like Recurrent Neural Network, LSTM, GRU or Convolutional neural net but we are using this seq2seq model for language translation so both encoder and decoder should be models which can handle sequential input. We will use LSTM.
Encoder takes input learns patterns in them, so we just take what it learned which is its hidden states[h, c](brown rectangle in above animation) and pass this as initial state for decoder. We don’t take output from each time step.

#### Decoder:-
Decoder with encoder’s state as it’s initial state will predicts one word at time. Here important part to understand is unlike encoder decoder works differently during training and testing.

<img src="https://cdn.analyticsvidhya.com/wp-content/uploads/2019/06/seq2seq.gif" alt="gif">

Dataset:-        
- We have 41028 sentences of English and their respective Marathi translations. I got this data from manythings.org. you can get dataset for translation of many more languages.
Preprocessing:-
- First we need to understand what we need for translation.
- We need sentences of one language and respective sentence for other language.
- Their might be some contractions of English words which can confuse our model it will see words like “can’t” and “can not ” differently so we will expand all contractions.
- Characters like coma and dot is not useful in translation so we’ll drop all of them.
- Digits are also not needed.

Preparing data for encoder decoder:-                 
Here is how we are going to prepare data for encoder decoder model
- Add SOS and EOS tokes in Marathi sentences.
- Get all unique words of English and Marathi and create respective vocabulary and sort them.
- Using our sorted words list we can give each word number and form dictionary which is very helpful to convert words into numbers. We have to convert words into numbers because neural nets don’t accept text as input.
- And lastly split data into train and test.

Data Generator:-                  
- This is very important, why we need data generator?
- As given in keras tutorial we have to convert data into 3D tensor of shape=[Batch size, Timesteps, Features]. Now in our case batch size, timestep and features are number of sentences, max-length-sentence, and number of unique words respectively.
- Using this, for Marathi input tensor array becomes [41028, 37,13720] this will consume lot of memory.

#### Build Encoder-Decoder LSTM :-
Before we get to coding part we have to understand few things-
#### Embedding:-
- We are going to pass our input of both encoder and decoder in embedding layer first and then in LSTM layer.
- This layer take numbers as input and converts them into given number of dimensions, But why we need to do so? → Answer is, using this we can preserve semantic information of words means similar words will be closer to each other.
- Example: Word ‘man’ will be closer to ‘women’, ‘ dog’ will be closer to ‘cat’ . It simply means vectors of man word will have similar numbers with women than dog and cat.

Training:-              
Train our model with some callbacks for 30 epochs. And don’t forget to save weights of model.

Inference Model:-           
- We use this model to predict output sequences by using weights of pre-trained model.
- Here we can not just apply model.predict() as other ML and DL models because in our case encoder model learns features in input sentences and decoder simply takes encoders states and predicts word by word using decoder inputs. So for prediction we have to do same process.

Predictions:-                   
One last thing to discuss, model will predict vector of number and one word at time so we have to create function to create sentences from predicted numbers.

**Application of encoder-decoder model**

- Machine Translation, e.g. English to French translation of phrases.
- Learning to Execute, e.g. calculate the outcome of small programs.
- Image Captioning, e.g. generating a text description for images.
