# bot-rules
A JSON based ruleset for that subreddits can use to dictate what actions they wish to allow bots to perform. Similar to robots.txt

# Project Background
Often subreddit moderators wish to restrict the activity of bots on their subreddits, however, there is little that can be done, short of outright banning, to dictate what they can and can't do.

"bot-rules" solves this problem by providing a set of voluntary rules for bots to follow in the form of a JSON object located on the subreddit's wiki.

Similar to robots.txt, used in web development to put certain voluntary restrictions to web-crawlers, the rules that subreddit's lay down in their bot-rules document are not enforced, meaning that bots should voluntarily take steps to read and adhere to the document.

This project aims to first provide a consistent schema that can be used by both bots and moderators, and then provide tools for both to be able to easily integrate bot-rules into their subreddits and bots.
