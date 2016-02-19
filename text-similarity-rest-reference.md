# RxNLP Text Similarity API REST Reference

## What is Text Similarity API?

[<img src="https://d1g84eaw0qjo7s.cloudfront.net/images/badges/badge-icon-light-9e8eba63.png" alt="Mashape" width="143" height="38" />][1]

<p style="text-align: justify;">
  The Text Similarity API computes surface similarity between two pieces of text (long or short) using well known measures namely Jaccard, Dice and Cosine. Determining similarity between texts is crucial to many applications such as <em>clustering, duplicate removal, merging similar topics or themes, text retrieval and etc</em>. Let's say we have the following two product listings on eBay:
</p>

<pre style="text-align: justify;">"text1": "iphone 4s black new",
 "text2": "iphone 4s black old"</pre>

<p style="text-align: justify;">
  How can you tell that these two listings are almost the same? You can use text similarity measures for this. The results from the Text Similarity API shows how close these two texts are using different measures:
</p>

<pre>{
 "cosine": "0.750",
 "jaccard": "0.600",
 "dice": "0.750",
 "average":"0.700"
}
</pre>

<p style="text-align: justify;">
  In text mining applications, you can heuristically set a similarity threshold. Meaning, if the similarity score between two pieces of text is greater than a value, say 0.5,<sub> </sub>then you can consider these two units as being similar.  Threshold levels are dependent on the application need. Here are some recommendations:
</p>

- For strict similarity, use a threshold of 0.5 and above
- For a more liberal similarity,  use a score lesser than 0.5
- In some cases, you can avoid thresholds by ranking texts by similarity scores and using only the top N most similar texts.

* * *

# Integrate Text Similarity with Code

To use this api, you would essentially have to set 3 parameters:

*   **text1**: your first unit of text or text tokens
*   **text2**: your second unit of text or text tokens
*   **clean:** perform cleaning on your text before similarity computation?

<div style="box-sizing: border-box;">
<p class="rtejustify" style="text-align: justify;">
You can have fairly lengthy units of texts (e.g. two plain text documents) but the maximum payload size is 1MB per request. The text that you provide can be plain words, words with Part of Speech Annotations (POS) (e.g.the/dt cow/nn jumps/vb) or combined tokens such as n-grams (e.g. this_cat cat_is is_cute).
  </p>
</div>

* * *

## First Steps: Get your API Key

<p class="rtejustify">
  Before you start, please ensure that you have a <a href="http://www.rxnlp.com/api-key">valid API key</a>.
</p>

* * *

## Request

The TextSimilarity endpoint accepts a **JSON request via POST.** It takes in 3 parameters:

<table style="width: 1201px; height: 88px;" border="0" cellspacing="1" cellpadding="1" align="left">
  <thead>
    <tr>
      <th scope="col">
        <strong>Parameter name</strong>
      </th>
      
      <th class="rtecenter" scope="col">
        <strong>Type</strong>
      </th>
      
      <th class="rtecenter" scope="col">
        <strong>Required?</strong>
      </th>
      
      <th class="rtecenter" scope="col">
        Description
      </th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
        text1
      </td>
      
      <td class="rtecenter">
        text
      </td>
      
      <td class="rtecenter">
        Yes
      </td>
      
      <td class="rtecenter">
        first text
      </td>
    </tr>
    
    <tr>
      <td>
        text2
      </td>
      
      <td class="rtecenter">
        text
      </td>
      
      <td class="rtecenter">
        Yes
      </td>
      
      <td class="rtecenter">
        second text
      </td>
    </tr>
    
    <tr>
      <td>
        clean
      </td>
      
      <td class="rtecenter">
        text
      </td>
      
      <td class="rtecenter">
        No (Default=true)
      </td>
      
      <td class="rtecenter">
        lowercase, remove punctuation and numbers?
      </td>
    </tr>
  </tbody>
</table>

<span style="color: #ff0000;"><strong>Points to note:</strong></span> 

- There is **no maximum length** for the text, but a 1MB maximum payload per request. 
- The text can be in **any language** - The text that you provide can be: 
  - plain text, (e.g. the cow jumps over the moon) 
  - text with POS annotations (e.g. *the/dt cow/nn jumps/vb*) 
  - manipulated texts such as n-grams (e.g. *thiscat catis iscute*). 
- Since this is a json request, your text has to be properly escaped and encoded in UTF-8
  
Requests can be sent in any language as long as it is formatted according to the expected JSON format. There is a library called the [unirest][2] library that handles http request and response in several languages including Java, Python, Ruby, Node.js, PHP and more. Here is an example, using the Java Unirest library:

    // These code snippets use an open-source library. http://unirest.io/java 
    HttpResponse response = Unirest.post("https://rxnlp-core.p.mashape.com/<strong>computeSimilarity</strong>") 
    .header("X-Mashape-Key", "<your_api_key>") 
    .header("Content-Type", "application/json") 
    .header("Accept", "application/json") 
    .body("{'text1':'this is test 1','text2':'this is test 2!', 'clean':'false'}") .asJson();
    

*   'text1' and 'text2' are the two texts that you want to compute similarity over and are both **mandatory**.
*   'clean' indicates if you want your text to be cleaned up prior to computing text similarity and this is **optional**
*   Content type with application/json is **mandatory** to indicate the type of request being sent
*   X-Mashape-Key is **mandatory** and it is the key that allows you access to the API Here is a simple <a href="https://github.com/RxNLP/sdk-and-resources/blob/master/java/TextSimilaritySimpleWrapper" target="_blank">wrapper</a> for the text similarity API in Java using HttpURLConnection

* * *

## Response

<p style="text-align: justify;">
  Text Similarity returns a <strong>JSON response</strong>. It returns the <strong>Cosine</strong>, <strong>Jaccard </strong>and <strong>Dice</strong> similarity scores along with the <strong>average</strong> based on these 3 scores. Here is an example request and response output:
</p>

**Request:**

<pre>{
 "text1":"this is test 2",
 "text2":"this is test 2!", 
 "clean":"true"
}
</pre>

**Response:**

<pre>{
 "cosine": "1.000",
 "jaccard": "1.000",
 "dice": "1.000",
 "average": "1.000"
 }</pre>

**Request:**

<pre>{
"text1":"this is test 2",
"text2":"this is test 2!", 
"clean":"false"
}</pre>

**Response:** 

<pre><code>
{ 
  cosine :0.750 , 
  jaccard: 0.600, 
  dice: 0.750, 
  average:0.700
}
</code></pre>

<p style="text-align: justify;">
  Since you have access to different similarity measures, you can choose to use one of these measures at all times or all of it at once. You can also use the average scores.
</p>

* * *

# Which Similarity Measure to Use?

<p class="rtejustify" style="text-align: justify;">
  If you have very short texts and want a strict measure that ensures only phrases that are very similar get high scores, then <strong>Jaccard </strong>would be ideal. However, if your text is more than 5 words long, Cosine or Dice may be more appropriate since these measures tend not to over-penalize non-overlapping terms. You can also average all three scores. In either case, please do some experimentation before you decide which measure(s) to use.
</p>

* * *

# Improving Similarity Measures

<p class="rtejustify" style="text-align: justify;">
  There are several ways to improve similarity (meaning finding more overlaps). Here are some ideas to improve reliability in the similarity measures:
</p>

*   Stem the text units before computing similarity
*   Remove determiners (e.g. the, an, a) [<a href="http://dictionary.cambridge.org/us/grammar/british-grammar/determiners-the-my-some-this" target="_blank">see list</a>]
*   Remove stop words [<a href="https://github.com/RxNLP/text-mining/blob/master/terrier-stop-word-list.txt" target="_blank">full stop word list</a>] [<a href="https://github.com/RxNLP/text-mining/blob/master/minimal-stop-word-list.txt" target="_blank">minimal stop list</a>] [<a href="http://www.ranks.nl/stopwords" target="_blank">stop words in other languages</a>]

* * *

# Languages Supported

Text Similarity is <span style="text-decoration: underline; color: #ff0000;">language-neutral</span> and would thus work for all languages.

 [1]: https://www.mashape.com/rxnlp/text-mining-and-nlp?&utm_campaign=mashape5-embed&utm_medium=button&utm_source=text-mining-and-nlp&utm_content=anchorlink&utm_term=icon-light
 [2]: http://unirest.io/
