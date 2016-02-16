
# What is Text Similarity Simple Wrapper?

This is a simple Java Wrapper for [RxNLP's Text Similarity API](http://www.rxnlp.com/api-reference/text-similarity-api-reference/). 


# What is Text Similarity Simple Wrapper?

```java
targetUrl = new URL("https://rxnlp-core.p.mashape.com/computeSimilarity");
			
			//First set the headers
			HttpURLConnection httpConnection = (HttpURLConnection) targetUrl.openConnection();
			httpConnection.setDoOutput(true);
			httpConnection.setRequestMethod("POST");
			httpConnection.setRequestProperty("Content-Type", "application/json");
			httpConnection.setRequestProperty("X-Mashape-Key", "<GET_YOUR_MASHAPE_KEY>");
```
