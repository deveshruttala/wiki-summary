# wikipeida -summary
* Wikipedia article summarizer and translator 

In this project, we will implement a summarization task using contents from Wikipedia pages online. We will be summarizing one of the longest articles on Wikipedia into 10 sentences!  We will employ natural language processing and deal with extracting summaries from this article.
The task of reducing the size of an article is not a major problem. The challenge will be to still retain the contextual meaning. To do this we follow a pipeline where each word and sentence are given weights and considered based on this.


<br> <p  align = "center" >  <img src="nlp asset.png" width="600" height = "250" align = "center" /> </p>



## Introduction
Document Summarization has become a vital task for various individuals and businesses that require a way of cutting down complexities involved with bulky documents. Summarization reduces a piece of document to a rendition less lengthy. This reduces the time complexity and effort initially required to consume that text. This is done such that the original message in the document is retained.

Natural Language Processing (NLP) is the activity of making machines understand and make meaning out of human languages. It is the processing of text involving cleaning and preparing data and using it as input to the computer. Preprocessing is an important activity for preparing the data for any machine learning model and NLP is not exempted.

There are a number of steps considered in NLP depending on the overall goal. This may be removing stop words, tokenization, attaching value to words, weighing them, etc. We will consider a number of them in this project as we progress.


## Documentation 

How does NLP work?<br>
Just as in any field in data science, NLP also requires data. This data will be the chunk of text in the document it will process. Since this text is not in a tabular form like in CSV or an image which is more structured, but rather as a bunch of random words, we consider it as unstructured data. But we will not consume it as it is.
<br>
We will first find a way to assign some structure to it. Since we are targeting the human user, we simply consider this text from a human perspective. For instance, in the English language, some words have the same meaning in any context they appear and have very little worth except to join other important words.
<br>
These are words called “STOP WORDS”. In processing we respect that they have little value in real life so we see them as noise and remove them. These are the various kind of considerations in NLP. We will see this practice in this project.
<br><br>
Application Areas<br>
Document summarization has been employed in a variety of tasks including:<br>
Chatbots: chatbots require their interactions to be as precise as possible. But most users fail to meet this requirement and end up not using the bot to its best performance. Summarizing bulky input texts can help the bot focus better and fix this problem.
<br>
Patent research: You may need to search and read the full text of patents from different sources to find prior work or literature. Manually going through thousands of documents could become very tedious and slow. Document Summarization could help you summarize and extract the most salient claims across patents.
<br>
Emailing: People easily face huge chunks of emails. Summarization can present smaller content and save time via skimming faster.
<br>
Online Marketing: Most online platform users like social media, and blogs, prefer less bulky ad content. The same content made for one platform may not fit another. Document summarization reduces content to fit into platforms like Twitter.
<br><br>

<br><br>
Project Pipeline:<br>
1. Import Dependencies<br>
2. Fetch Articles from Wikipedia<br>
3. Preprocess the Data<br>
4. Text Tokenization/Text to Sentence<br>
5. Weight the Frequency of Words<br>
6. Score Sentences<br>
7. Extract the Summary<br>
<br>
Like regular Python projects, we start first by bringing in the required libraries. Python does not automatically import libraries else our script will have over 137,000 packages when we need far less than that. This could reach a whopping 4.2 GB! Our Python script gains access to the code in another module by the procedure of importing it.
<br><br>
We will be using a number of library dependencies. Let us look at the major ones:
<br>
1. nltk: It is an NLP core library. It is developed for natural language processing in a variety of languages and contains tools for diverse tasks in the field. We will use it to process the data and set parameters.<br>
2. beautifulsoup4: This is the most powerful web scraping library. We will use libraries here to read the article from Wikipedia as we want.<br>
3. lxml: a standard for reading webpages such as HTML or XML. It ensures the loaded page is easily handled and extracted.

<br><br>
* Fetching Articles from Wikipedia<br>

Before we start to load the data into the project, it is essential to understand a few points. Document summarization can be done in different depending on the overall objective. Let us see them and clearly understand the one we are doing.
<br>

Firstly, we have single-document summarization and multi-document summarization:

Single-document summarization, which is the most common use case, is used on one document at a time. This document is imported and summarized as an entity.

Multi-document summarization will be the task of congregating a compilation of different documents and summarizing them into one summary. This is less common but is also done. This could be used when they are multiple documents or queries on the same topic. The most prevalent context becomes the output.
<br><br>

Secondly, we consider the approach employed in the task. This could be extractive or abstractive summarization:

Extractive summarization does not modify the sentences but simply brings the most important lines as the summary. The only major task is rearranging the document so that it still makes meaning while reading.

Abstractive summarization: This is more like a paraphraser. It modifies the sentences to a new form while also retaining meaning.

For this project, we will be employing a single document and the extractive summarization approach.


<br>

* Preprocessing of the Data<br>
The next vital thing is to remove unwanted content and ensure the article is as meaningly as possible. This will be our data processing stage.
After scraping the data from the web using beautifulsoup. We then pass the page content to be readable as HTML or XML. Since it is now understood well as HTML, we locate all the paragraph tags and then read the content in them into a new variable called paragraphs lastly this step is to neatly read these contents into a new complete document by iterating and concatenating the paragraphs. Let’s view what we have:<br>
Even though we have concatenated the paragraph contents, there are still characters that are still in between the words. Like inline references, slashes, etc. We replace them with spaces to allow contextual flow.


* Performing Text Tokenization <br>
The data is ripened enough to be considered more seriously. We can now look at our article as smaller chunks. We look at the sentences. This is called tokenization. We will divide the article into sentences using full stops. Since in the English language, full stops are used to end and start sentences, we will divide by full stops. We have two variables containing our articles. We will use thearticle_text since it still has symbols including full stops. Hence, the formatted_article_text does not contain symbols or any punctuation. <br>What is tokenization?: Tokenization, is commonly applied for a variety of reasons like data security, but in general, it is the process of replacing the original data form with a version more useable that represents it completely. This new equivalent is referred to as a token

* Weighting the Frequency of Words <br>
How summarization work is by generating by identifying the most frequent words. A sentence is judged by how much of frequent words it has. To do this, we only need words and not symbols. The variable that does this for us is the formatted_article_text variable.It is vital to note that we do not want to consider words that have the same meaning across contexts. This is words such as “the”, “and”, “is”, etc. The steps are to first remove these words. This is the advantage of using nltk library. These words have been gathered for us in various languages including German, French, Spanish, etc. You can even create one for your local language and contribute to the library.The stop words are escaped or not included in the words we want to give weight to. For instance, “the” is always the most frequent word yet it has one meaning. This will shift the average of the overall word frequency. A good practice is to drop all similar words.


* Finding the Score of Sentences <br>
We are now ready to go a bit higher by dealing with the sentences. This will be done based on the occurrence of valuable words. Since we now know the weight and frequencies of all the words, we can calculate the scores for the sentences. This is pure Maths. We just add up all the weights of the words in the sentence and then score the sentence.




<br>




* Extracting the Article Summary
Finally, the most exciting point. We have computed the scores for each sentence in the article. This is how we decide finally on the summary. We can decide how many sentences we would want to have. We will make the summary contain only 10 sentences. This is the top ten highest score. This is seen below.

## NOTES:
Normally, in Jupyter Notebooks, you may prefer to give a fixed URL, change the URL when you need it and not ask for user input. But I wanted to see from which articles I can get a better summary and when the NLTK does "so so": That's why, I ask for user input and give different Wikipedia articles in English language. Also, this way, code is more flexible.
<br>
user link = input("Which Wikipedia article would you want me to summarize: ") #with user input version, a bit more flexible
<br>
#If you prefer a fixed URL in the code or if you encounter an error in Jupyter, then you can also change the code with a pre-given URL and change it accordingly later in Jupyter Notebook.
<br>
Since I like F-Secure and wish to attend their training, I search for them and wrote this simple Wikipedia Article summarizer to practise NLP and Python, meanwhile learning more about F-Secure, its history, culture, etc.
<br>
<br>


Full capabilities of wikiscrape package include:<br>
Able to search in multiple languages<br>
Give suggestions on search terms if the search is ambiguous<br>
Gives a short summary (2 paragraphs) of the article if it is retrieved successfully<br>
Retrieve full text or exact number of paragraphs in string output for data pipeline<br>
var.HELP() for the full list of functions available<br>
Basic error handling, including checking data type of arguments and reverting to defaults if errorneous args are given<br>
Apply local stoplist by directly editing the dictionary, and also applying NLTK stoplist for multiple languages<br>
Lemmatizing the article before using the text analytics functions<br><br>
Text Analytics capabilities include:<br>
A frequency counter on the most common words in the Wikipedia article (after omitting common English words, or stoplist from NLTK for foreign languages). <br>Can also find the Nth % of most common words, where 0 =< N =< 100.<br>
A graph plot of the most common words in the Wikipedia article, and save the graph as an image<br>
A graph plot on the most frequent Years mentioned in the article, to understand the Years of interest of the article, and save the graph as an image
A summary on the total number of words and total number of unique words after implementing the stoplist & lemmatization of common words.<br>
Analytics functions available in wikiscrape object are commonwords, commonwordspct, plotwords, plotyear, totalwords, summary, gettext.<br>



* to implement git clone the repo and follow the notebook instructions. <br>
``` git clone  https://github.com/deveshruttala/wiki-summary.git```


### Conclusion and credits
In this project, we have tried to explain the task of text summarization using Python NLTK and other helper libraries. We summarized the Wikipedia article into 10 sentences. Document summarization can be used in diverse scenarios. You can adjust the project to various use cases. Two things to adjust are simply the input point of the data and the output point where you specify the number of sentences.<br>
and i reachout to my thanks for medium blog "wiki summarization in 10 sentences" for inspiring me  and 
<a href="https://medium.com/@abhinaya08/data-scientists-guide-to-summarization-dde46b30b4c3"> to know in detail about the aritcle summarization techniques follow this blog </a>
