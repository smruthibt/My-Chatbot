# My-Chatbot
***A seq2seq chatbot built with basic knowledge of LSTM's, RNN's, and tensorflow.***

**Part-1:**
Pandas, tensorflow, time and re library (used to replace the characters by some other characters and also to simplify the conversations).
  
**Part-2:**
Two essential tasks of NLP,
1.tokenization
2.filtering the non frequent words are performed.

I have created two dictionaries, one to map each word of all the questions to a unique integer and another dictionary to map all the words of all the answers to a unique integers.If the number of occurences of the word is below a certain threshold, then we would not include that word in the dictionary.(and the last 5% of it is filtered).

<EOS> token is added at the end of each answer of the seq2seq model.All the questions and answers are translated into integers.All the words that were filtered out are replaced by <OUT>.During training, we'll need to feed our examples to the network in batches.The inputs in these batches must all be of the same width for the network to do it's calculation.Since all inputs are however not of the same length, we have to pad shorter inputs to bring them to the same width of the batch.
  
**Part-3:**
*Training the Seq2Seq model*
 
Since in tensorflow,all variables are used as tensors, I have created a tensorflow placeholder,that will contain the target data, the target data is comprised of encoded integers,that encodes the words of the answers. Also created two more tensorflow placeholders, the learning rate which is a hyper parameter and also keep prob which is used to control the dropout rate. Dropout rate refers to the neurons we choose to overwrite during on iteration.
 
*Preprocessing the targets*
 The decoder will only accept a certain format of the targets.
 1. The targets must be in the form of batches, the decoder of the RNN will not accept single answers
 2. Each of the answers of the batch of targets must start with the <SOS> token.
  
*Encoded RNN layer*
I have using the BasicLSTMCell class by tensorflow, apart from that Bidirectional dynamic RNN. Bidirectional encoding designates one or more RNN cells to read the sequence forward and one or more RNN cells to read the seqquence backward.The results are concatenated before sending them on to the decoder.It eliminates the need of input reversal,also makes the order of padding irrelevant. Context vector is going to be returned by the encoder and was used as the first element of the decoding.For the encoder we only need the final encoder state and not the encoder output, for the decoder we need the decoder output only and not the final state or the final context state. We are going to assemble the encoder that returns the encoder state, and the decoder that returns the training predictions and the test predictions.

*Setting up the hyper-parameters*
An object for the interactive session is defined using the tf.InteractiveSession() , also by resetting the tensorflow graph we make it ready for training.
Dropout regularisation is to remove over-fitting and improve efficiency. Dropping out 20% of the input units and 50% of the hidden units was often found to be optional. Loss error is weighted cross-entopy function, Adam optimiser is best for stochastic gradient descent and then we apply gradient clipping on it.

**Part-3:**
*Testing and tuning the Seq2Seq model*

checkpoint = "chatbot_weights.ckpt"
The run method is called to initialise all the global variables. There are two for loops,one for each epoch and each epoch for the batches.One epoch is completed when all the batches go back and forth thhe double RNN.We get the total_training_loss_error and compute the averages over 100 batches.

The questions are converted from strings to a list of encoding integers.And finally we replace all the EOS tokens by dots.
 
 
