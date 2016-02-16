
## TextSimilaritySimpleWrapper.java

This is a simple Java Wrapper for [RxNLP's Text Similarity API](http://www.rxnlp.com/api-reference/text-similarity-api-reference/) which computes the similarity between two pieces of text (text can be arbitrarily long). The API computes dice, jaccard and cosine similarity between texts and also produces the average scores. Note that the API can also clean the text prior to computing the similarity scores.


## Explanation of Code

### Making connection to the API

Note that using plain vanilla HTTP Request is much faster than using the Unirest library. The X-Mashape-Key is the API key that you would need to obtain from Mashape in order to use the API. 

```java
targetUrl = new URL("https://rxnlp-core.p.mashape.com/computeSimilarity");
			
			//First set the headers
			HttpURLConnection httpConnection = (HttpURLConnection) targetUrl.openConnection();
			httpConnection.setDoOutput(true);
			httpConnection.setRequestMethod("POST");
			httpConnection.setRequestProperty("Content-Type", "application/json");
			httpConnection.setRequestProperty("X-Mashape-Key", "<GET_YOUR_MASHAPE_KEY>");
```
### Send JSON request

Here we create a  JSON request based on two strings for similarity comparison and then we send it to the server. Note that the strings can be pretty long as the request does not exceed 1MB. For details on the parameters, [refer to this documentation](http://www.rxnlp.com/api-reference/text-similarity-api-reference/#request)

```java
String str1="This is the first string.  It can be quite long.";
String str2="This is the second string.  It can be quite long.";
			//Then set input
			String input = "{\"text1\":\""+str1
							 +"\",\"text2\":\""+str2
							 +"\",\"clean\":\"true\"}"; 

			//Next, process output
			OutputStream outputStream = httpConnection.getOutputStream();
			outputStream.write(input.getBytes());
			outputStream.flush();```
```

### Read JSON response from server

Here we read the JSON response and print the raw JSON line by line. You can parse the raw JSON to obtain the cosine, jaccard and dice similarities.

```java
BufferedReader responseBuffer = new BufferedReader(new InputStreamReader((httpConnection.getInputStream())));

			//Printing output from server (you can use a json parser here instead)
			String output;
			System.out.println("Output from Server:\n");
			while ((output = responseBuffer.readLine()) != null) {
				System.out.println(output);
			}
			
```			
### Example Input

```json
 {
 "text1": "iphone 4s black new", #this is text1
 "text2": "iphone 4s black old", # this is text 2
 "clean":"true" #clean the text or not?
 }
``` 

### Example Input
```json
{
 "cosine": "0.750",
 "jaccard": "0.600",
 "dice": "0.750",
 "average":"0.700"
}
```
