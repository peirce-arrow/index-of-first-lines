# index-of-first-lines
Test repo for final project reorganizing the first lines of shakespeare's sonnets


Project Title

"Index of First Lines" 

Project Description

This project seeks to automate the production of a poetic text constructed entirely from the first lines of Shakespeare's sonnets. 

Shakespeare published 154 sonnets. One-hundred and fifty-four divided by fourteen (the line length of a Shakespearean sonnet), equals eleven.
That means we can use all of the first lines of the sonnets to construct eleven sonnets. 

Rationale Statement
expresses the motivations behind the project

Workflow
identifies libraries used and explains the important steps being taken in the code.
(This below is for the file 'shakespeare_firstlines')
- Using requests, scrape the text of the entire sonnet sequence from the Folger Library's website.
- Using re, find all first lines, prepend each line with a number, from 0 to 153 (for ease of processing), and clean up any html tags leftover from scraping and any odd characters (such as the half-square brackets used on the site to denote an emendation by editors).
- Using string methods and list methods, create a list that pairs the line number with the end word, stripping any punctuation.
- Using if loops and string methods, normalize archaic spellings (such as 'blest', 'play'st', etc.).
- Using requests, pronouncing, re, and string methods, find rhymes for end words...


Further Uses
in what ways might someone build on this work or re-use your code.

Files List
a list of files relevant to the project (python notebooks, csv files, etc) and a brief description of what each file contains


