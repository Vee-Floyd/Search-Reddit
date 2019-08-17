!pip install praw
import praw
import pandas as pd
pd.set_option("display.max_colwidth",-1)
from datetime import datetime as dt

#input reddit credentials here
reddit = praw.Reddit(client_id='INPUT CLIENT ID HERE',
                     client_secret='INPUT CLIENT SECRET HERE',
                     password='INPUT PASSWORD HERE',
                     user_agent="INPUT USER AGENT HERE",
                     username='INPUT USERNAME HERE')

#The below code verifies the user you are log in as
print(reddit.user.me())

#input search query below using a simple keyword or complex boolean search, see boolean capabiliies here: https://www.reddit.com/wiki/search
#recommend writing query as its own variable for readability ie:query="title:gluten"
#input how far back you'd like to search. Options are "all","day","hour","month","week","year" with all being the default
#input subreddit you'd like to query (default is all of reddit aka "all")

def search_reddit(query,time_parameter="all",subreddit_name="all"):
  posts=[]
  for submission in reddit.subreddit(subreddit).search(query,time_filter=time_parameter):
      date=dt.utcfromtimestamp(submission.created_utc).strftime('%m/%d/%y')
      hour=dt.utcfromtimestamp(submission.created_utc).strftime('%H:%M')
      author=submission.author 
      title=submission.title
      score=submission.score
      url="reddit.com/"+submission.permalink
      post_info=[date,hour,title,author,score,url]
      posts.append(post_info)
  reddit_df=pd.DataFrame(posts, columns =["date","time","title","author","score","url"] )
  reddit_df=reddit_df.sort_values(by=["score"], ascending=False)
  return reddit_df
