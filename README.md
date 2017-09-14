# bot-rules
A JSON based ruleset for that subreddits can use to dictate what actions they wish to allow bots to perform. Similar to robots.txt

# Project Background
Often subreddit moderators wish to restrict the activity of bots on their subreddits, however, there is little that can be done, short of outright banning, to dictate what they can and can't do.

"bot-rules" solves this problem by providing a set of voluntary rules for bots to follow in the form of a JSON object located on the subreddit's wiki.

Similar to robots.txt, used in web development to put certain voluntary restrictions to web-crawlers, the rules that subreddit's lay down in their bot-rules document are not enforced, meaning that bots should voluntarily take steps to read and adhere to the document.

This project aims to first provide a consistent schema that can be used by both bots and moderators, and then provide tools for both to be able to easily integrate bot-rules into their subreddits and bots.


# Format
##### Example
The standard format of a bot-rules file is as follows
```json
{
  "bots": {
    "read": { "allow": (boolean) },
    "write": {
      "comments": {
        "allow": true,
        "rate-limiting": [{
          "amount": (int),
          "period": "minute"|"hour"|"day"|"month"|"year"
        }]
      },
      "submissions": {
        "allow": false
        "rate-limiting": [{
          "amount": (int),
          "period": "minute"|"hour"|"day"|"month"|"year"
        }]
      }
    }
  }
}
```
##### Keys
###### `bots` 
The root key of the bot-rules object




---
###### `read`
The root for all reading based permissions

###### `read.allow [type: boolean]` 
Indicates whether compliant bots are allowed to read content on the specified subreddit. This includes comments as well as submissions.

`true`: Bots are allowed to read submissions and comments unrestricted.

`false`: Bots are **not** permitted to read any submissions or threads.




---
###### `write`
The root for all write based permissions

###### `write.comments`
The root for write based permissions for comments within a subreddit

###### `write.comments.allow [type: boolean]`
Indicates whether compliant bots are allowed to write comments on threads within a specified subreddit.

`true`: Bots are allowed to write comments on any non-locked thread within the subreddit.

`false`: Bots are **not** permitted to post comments on any threads in this subreddit.

###### `write.comments.allow.rate-limiting`*Optional*
See `rate-limiting`. Has no affect if `write.comments.allow` is `false`.


###### `write.submissions`
The root for write based permissions for submissions within a subreddit

###### `write.submissions.allow [type: boolean]`
Indicates whether compliant bots are allowed to post submissions within a specified subreddit.

`true`: Bots are allowed to post submissions on the subreddit.

`false`: Bots are **not** permitted to post any threads in this subreddit.

###### `write.submissions.allow.rate-limiting`*Optional*
See `rate-limiting`. Has no affect if `write.submissions.allow` is `false`.






---
###### `rate-limiting [type: array]`
An array of rules used to restrict how frequently a bot can write to a subreddit. When multiple rate limiting rules
are specified, bots must ensure they do not violate any of them.

###### `rate-limiting.amount [type: int]`
The amount of times the action can be performed within the specified period

###### `rate-limiting.period [type: enum {"minute"|"hour"|"day"|"month"|"year"}]`
The period of time that rate-limiting rule applies to.