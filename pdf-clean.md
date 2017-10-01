# How it works

## About enchant:
```
import enchant
dictionary = enchant.Dict("en_US”)
```

Use the dictionary to check whether a token in a sentence is word:
`dictionary.check(wordString)`

## The algorithm works as follows:
check the the ith word and (i+1)word in a sentence, if both words are not in the dictionary and the concatenation of ith and (i+1)th word is in the dictionary, then we merge them. 

## handle broken words

You only need to use this function in your program

	@param: sentences is a list of sentences (strings)
	@return: merged_sentences: a list of sentences (strings) 
	def merge_words(sentences):
	    dictionary = enchant.Dict("en_US")
	    merged_sentences = []
	
	    for sent in sentences:
	        sent = sent.split()
	        i = 0
	        newsent = []
	        while i < len(sent)-1:
	            if (not dictionary.check(sent[i]) or not dictionary.check(sent[i+1])) and (dictionary.check(sent[i]+sent[i+1].lower()) or dictionary.check(sent[i]+sent[i+1].lower()[:-1])):
	                newword = sent[i]+sent[i+1].lower()
	                newsent.append(newword)
	                i += 2
	            else:
	                newsent.append(sent[i])
	                i += 1
	        lastword = sent[len(sent)-1]
	        if dictionary.check(lastword):
	            newsent.append(lastword)
	        merged_sentences.append(' '.join(newsent))
	    return merged_sentences
