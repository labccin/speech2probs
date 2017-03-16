# speech2probs
Pronunciation Assessment System Made with Uniform Language Model using Kaldi. 

# Speech2Prob: HMM Posterior Probability Estimator Built with Kaldi


## What it Does:
For each frame being decoded, instead of outputting the single most-likely phoneme candidate (what ASR does), this system returns all the candidates and their respective probabilities. 

## What this means:

1) A '**broken**' Lexicon

* The conventional lexicon (word-pronunciation mapping; shown below) shouldn't apply, as you don't want the system to output real words. Speech2prob doesn't know which sequence of phoneme form real words.

		가공의	k0 aa k0 oo ng xi	
		가기	k0 aa k0 ii
		가기도	k0 aa k0 ii t0 oo
		가까운	k0 aa kk aa uu nf
		.
		.
		.

* So the 'lexicon' in this case should just map itself to itself. **In the new lexicon, each phoneme is regarded as a word.** This is just like the lexicon in the well-known TIMIT recipe. 

		aa	aa
		c0	c0
		cc	cc
		ch	ch
		  .
		  .
		  .

2) A '**null**' G.fst

G.fst in Kaldi restrains the output word sequence by the sequences that are more likely according to the ngram counts in the text data you provide. A G.fst with extensive coverage about real world word sequences works like charm. This is how Google's ASR turns out so great. The more informed your G.fst is about the real world word sequences, the more readily it will fix the 'unlikely word' sequences your acoustic model & lexicon will output.
 
However, if your end goal is not in returning the most sensible, likely string of words, you don't want all these real world data. For your purpose of capturing the sound of your speech, you will have to make a **null/uniform/dumb/fake** G.fst: the G, in other words, that can only tell you that *every word is as likely* to appear after another! 

## What you need:

### To Build the Dictionary:  



### To Build the Acoustic Model: 
1) wav.scp 

2) utt2spk

3) text*

4) segments (optional)
 
### To Build the Language Model:  
1) JSGF grammar-based G.fst - PIC 

2) 

