# Metasearch-Engine

## Introduction: 
Meta search engine is a search engine which is built on top of a few existing search engines. It has a search interface which could accept queries from users. Upon receiving queries, it will send them in parallel to the underlying search engines and get the results back, and the next step is to use a combination or aggregation algorithm to combine all the results into a single ranked list and return it to users. For example, if a meta search engine is built based on Google and Bing, when it receives a query from a user, it will send this query to both Google and Bing in parallel, then combine the results from both search engines into one single result list and return to the user. Mamma or Dogpile is such an example. One of the rank aggregation algorithms use is Borda Fuse. 

## Installation
**Requirements:**
Make sure Python 2.7 (not 3.0) is installed, Internet connection, Windows OS

**Modules Required:** 
- Google API Client module
- Requests module
- JSON module

JSON module should be included when you download and install latest version of Python 2.7. JSON is used to convert response from search engine into a readable format. The other two modules are not included and have to be downloaded and installed.

Google API Client module installs the Google’s API to be used for search in Google Custom Search Engine. Requests module is used for sending a request to the search engines and getting the response back from it. 

**Installing/Uninstalling Required Modules:**

1. Check to make sure pip.exe is in folder C:\Python27\Scripts. Your folder location may be different. Pip.exe will be used to install modules. Then you have to check that the path where pip.exe is in is listed in the system environmental variable called “Path”. If it is not in it then it has to  be added  it in.
  
  a. Right-click “Computer” from windows start menu and select “Properties”

  b.	Find and click “Change settings” near the bottom of the window. A window named “System Properties” will pop up
  
  c.	Click on tab named “Advanced”
  
  d.	Find and click “Environmental Variables…” near the bottom of the window.
  
  e.	In the “System variables” box near the bottom, find variable named “Path”
  
  f.	Select “Path” and click “Edit…”. A window will pop up
  
  g.	In the textbox named “Variable value”, add your pip.exe path on the end of the textbox. NOTE: if you have something in this textbox (most likely), you will have to add a semicolon “ ; ” in the textbox before you add your pip.exe path. Like this “;C:\Python27\Scripts”. Your path may be different.
  
  h.	After adding in the path, click “OK” then click “OK” again and click “OK” once more.
  
2.	Open command prompt from windows start menu or type “cmd.exe” in windows start menu search bar.
	
3.	Type this command in command prompt window and press enter: pip
If this does not give any errors, you can go to the next step. Otherwise, you may have entered pip.exe path incorrectly in Step 1. Fix it before going to next step.

4.	Type this command in command prompt window and press enter: 
pip install -U google-api-python-client
This will install Google API Client module. A message will pop up saying it is successfully installed. 
To uninstall type this command: 
pip uninstall -U google-api-python-client

5.	Type this command in command prompt window and press enter:
pip install requests 
This will install Requests module. A message will pop up saying it is successfully installed.
To uninstall type this command:
	pip uninstall requests

6.	You have successfully installed the required modules.

## Executing Python Program
**Files required:** meta2.py

**Running the Program:** 

1. Open meta2.py file in Python 2.7 IDLE
2. Click “Run” from top menu and click “Run Module” or just press F5

## Google Custom Search Engine(CSE) & Bing Search API
**Results Differences:**
Google Web Search API is deprecated so Google CSE is used instead. Bing Search API is used in the program. The results returned by both will be different than the actual google.com or bing.com. Google CSE and Bing Search API results returned will be slightly different than google.com/bing.com search results. For more information about this issue, follow this link:   
https://support.google.com/customsearch/answer/2633385?hl=en

**Request/Query Limits:** 
There are limits to the number of requests you can send in 1 day in Google CSE and 1 month in Bing Search API. There is a limit of 100 requests/day for the free Google CSE. Since Google CSE can only get 1 page of (10) results every request, to get the next page (next 10) results, another request will be used. There is a limit of 5000 requests/month which is approximately 165 requests/day for the free Bing Search API. 

## meta2.py Design & Details
meta2.py will ask for a query and the number of results you want to get from Google and Bing. A custom query URL for Google CSE and Bing Search API is created and is requested. The response is saved in JSON formatting. JSON converts the response into a human readable text. The titles and links for Google and Bing are then located in their responses and are stored in separate arrays. After this, the rank aggregation algorithm, Borda Fuse(Count), is then used to combine both results from Google and Bing.   

**Algorithm Used:** 
Rank aggregation algorithm, Borda Fuse(Count)

This algorithm used to combine both results from Google and Bing is Borda Fuse(Count). The algorithm first looks at results from Google. It will then assign a score to each result. The first result will have a score of N. N is the total number of results returned. The second result will have a score of N-1. And the next is N-2 and so on. Let’s called this score, X. If the result is also in Bing’s results then X will be added with Bing’s score. Bing’s result score calculation is the same as Google’s result score calculation. Bing’s first result score is n, n is the total results returned from Bing. The second result score will be n-1 and then n-2 and so on. Let’s called this score Y. So the total score of the result will be X+Y if the result is in both Google and Bing. If the result is not in Bing, then the score of the result will be just X. The scores are then stored in a scores array. After looking at Google’s results, the algorithm will look at Bing’s results and find the ones that are not in Google’s results. The score for these results will be just Y. These scores are stored in the same scores array. 

The results are then printed out to the user by using an algorithm that prints out the highest score to the lowest score. User will then see the title and URL of the combined Google and Bing results in a ranked order.




