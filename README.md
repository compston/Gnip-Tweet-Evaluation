# Gnip-Tweet-Evaluation
This code provides audience and conversation insights, 
based on Tweet data from Gnip/Twitter APIs

# Installation
Clone the repo. From the base repo directory:

`$ python setup.py install`

This will install the package, and any dependencies, in your Python
interpreter's site-packages directory, and it will install the 
stand-alone executable files in an appropriate place

# Structure

The package has one stand-alone executable script: `evaluate_tweets.py`.
There are three modules: `analysis`,`output`,and `audience_api`. The
`analysis` module contains functions that return aggregate statistics for
the Tweet bodies (conversation) and the Tweet user bios (audience). The 
`output` module contains output-formatting functions. The `audience_api`
module contains the interfacte to Gnip's Audience API product. 

There is also a small test suite in `tests.py`. 

# Use

The command line interface uses `evaluate_tweets.py`, which should
be installed in your PATH. See the script's help options. For example:

`$ cat dummy_tweets.json | evaluate_tweets.py -n0 -c`

will display a conversation analysis of the Tweets in `dummy_tweets.json`. 

For package-level interface, simply import `gnip_tweet_evaluation`.
There is one primary function for evaluating data, which calls
two analysis-specific functions from the `analysis` module:

```python

from gnip_tweet_evaluation import run_analysis

conversation_results = {"unique_ID":"0"}
audience_results = {"unique_ID":"0"}
with open('dummy_tweets.json') as f:
    run_analysis(f,conversation_results,audience_results)
```

# Gnip Audience API use

Put your Gnip Audience API creds in `~/.audience_api_creds`:

```
username: yourUserName
consumer_key: xx
consumer_secret: yy
token_secret: zz
token: aa
url: https://data-api.twitter.com/insights/audience 
```

Presuming you have access to the service, the Audience API will will
be queried any time you request audience analysis ("-a") option and 
your input Tweet set contains more than the minimum number of unique users. 

