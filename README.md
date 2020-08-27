# My-Chatbot
A seq2seq chatbot built with basic knowledge of LSTM's, RNN's, and tensorflow.

Part-1:
  pandas, tensorflow, time and re library (used to replace the characters by some other characters and also to simplify the conversations)
  
Part-2:
  Two essential tasks of NLP,
  
    1.tokenization
    2.filtering the non frequent words are performed.
I have created two dictionaries, one to map each word of all the questions to a unique integer and another dictionary to map all the words of all the answers to a unique integers.If the number of occurences of the word is below a certain threshold, then we would not include that word in the dictionary.(and the last 5% of it is filtered)
  
