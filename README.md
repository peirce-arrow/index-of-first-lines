# index-of-first-lines
Test repo for final project reorganizing the first lines of shakespeare's sonnets

## Project Title

"Index of First Lines" 

## Project Description

This project seeks to automate the production of a poetic text constructed entirely from the first lines of Shakespeare's sonnets. 

Shakespeare published 154 sonnets. One-hundred and fifty-four divided by fourteen (the line length of a Shakespearean sonnet), equals eleven.

That means we can use all of the first lines of the sonnets to construct eleven sonnets. 

## Rationale Statement
I first conceived of this project around 2010, working by hand to construct the sonnets. I had some issues with repetition of lines (a problem I'm curiously still having with the code). The hope is that by using python and perplexity scoring from large-language models fine tuned on a Shakespearean corpus, I will be able to avoid careless mistakes and achieve a greater degree of semantic clarity in the final poems than I could by hand.

## Workflow
identifies libraries used and explains the important steps being taken in the code.
### For the script Main_Shakespeare_script
- Using **requests,** scrape the text of the entire sonnet sequence from the Folger Library's website.
- Using **re,** find all first lines, prepend each line with a number, from 0 to 153 (for ease of processing), and clean up any html tags leftover from scraping and any odd characters (such as the half-square brackets used on the site to denote an emendation by editors).
- Using **string methods** and **list methods,** create a list that pairs the line number with the end word, stripping any punctuation.
- Using **if loops** and **string methods,** normalize archaic spellings (such as 'blest', 'play'st', etc.).
- Using **requests, pronouncing, re,** and **string methods,** find rhymes for end words... at this point, the work came to a halt, owing to difficulties the solutions to which were not within the scope of the course.
  - For the beginnings of an attempt to use ARPAbet pronuncation to find rhymes, see *cmudict_test.ipynb*

### For the script SonnetLinePerplexityScorer01
- Pull in list of first lines from 'shakespeare_firstline' script, and clean up data to prepare for perplexity scoring
- For every possible permutation of two first lines (for 154 lines, that equals 23,562 pairs).
- Using **evaluate** and **sadia72/gpt2-shakespeare,** gpt2 fine tuned on an unspecified Shakespeare corpus, generate a perplexity score for each pair and store both in a csv. 
- Using **pandas**, sort pairs of lines by perplexity score, from lowest to highest.
- Using *'sonnet_perplexity_sorted.csv',* add perplexity scores for pairs of pairs to form quatrains (A,B,C,D) (Pair(A,B) score + Pair(C,D) score + Pair(B,C) score).
  - output: *'quatrains_with_fourline_score.csv'*
- Using **pandas**, sort quatrains by perplexity score from lowest to highest.
  - output: *'quatrains_scored_sorted.csv'*
- Returning to *'sonnet_perplexity_sorted.csv',* pick out the first 11 unique pairs to serve as final couplets for the final 11 sonnets. (There should be a better method for choosing these couplets, but for now, this arbitrary method works)
- Using *'quatrains_scored_sorted.csv',* extract all unique quatrains beginning with the lowest scores to the highest. (The problem with this method is that the quatrains rapidly increase in complexity as unique quatrains become less frequent)
- Create a list of all final quatrain lines paired with the first lines from all other quatrains, then find the perplexity scores of those pairs, in order to determine the best order to the quatrains. (This method is not ideal, and leads to the same issue of increasing perplexity for the sequence as a whole.)
- Add a couplet to the end of every third quatrain based on the perplexity score for the pair of last quatrain line and first couplet line. 
- Each quatrain and couplet is a list of line numbers, three quatrain lists and a couplet list are nested in a list which functions to delineate each individual sonnet.
- Write list to file. 
  - output: *'final_sonnets.txt'*

### Problems to be addressed
- Many issues will be resolved by the additional constraints of keeping the rhymes, particularly the arbitrariness of many of the line pairings.
- I'm having trouble generating enough unique quatrains to make 11 sonnets. So far, I've only had enough material to make a little over 7 sonnets. I'm not sure why this is happening, but my suspicion is that it has to do with how I generate the quatrains, iterating through the list of paired lines and their scores. But I'm not sure.
- I do not like that the lines increase in perplexity as the sonnets go on. 
- There needs to be a better way of coming up with final couplets. I've done some investigation, and there seem to be at least 11 lines the end either in periods, in question marks, or in semi-colons, which could serve as the second lines of the couplets and the final lines of the sonnets.
- I've also noticed that there are duplicated lines in the final sonnets, but I'm unclear why this is happeneing. 

## Further Uses
Once the rhyming problem is addressed, the code can be reused on the index of first lines of any sonnet sequence——though the number of lines would have to be reduced to a multiple of 14——and with minor adjustments, the code could be used with any index of first lines, with outcomes depending on the forms and meters of the poems in question.

## Files List

### Read Me
- README.md

### Production files
- Main_Shakespeare_script.ipynb
- SonnetLinePerplexityScorer01.ipynb
- cmudict_test.ipynb
	
### Output files
- final_sonnets.txt
- firstlines.csv
- quatrains_scored_sorted.csv
- quatrains_with_fourline_score.csv
- sonnet_perplexity.csv	
- sonnet_perplexity_sorted.csv