<img src="https://s3-eu-central-1.amazonaws.com/centaur-wp/designweek/prod/content/uploads/2016/05/11170038/Instagram_Logo-1002x1003.jpg" width="200" align="right">

# InstagramResearch
📄 Research repository for new instagram project
[![MIT license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/MohanSha/TwitterBot/blob/master/LICENSE)

## Basic Information that are displayed when accessing a page

**Schema:**
```bash
https://instagram.com/<path>?__a=1
```

**[Examples](./basic_endpoint)**
```bash
# Explore tags
https://www.instagram.com/explore/tags/<tag_name>/?__a=1

# Post page
https://www.instagram.com/p/<id_of_post>/?__a=1

# When logged in, feed
https://www.instagram.com/?__a=1

# Own/other profiles
https://www.instagram.com/<userame>/?__a=1
```

## GraphQL modifiable data endpoints

**Schema:**
```bash
https://www.instagram.com/graphql/query/?query_id=<query_id>&variables=%7B<parameters>%7D
```

| QueryID | Endpoint |
|---------|----------|
|17875800862117404|posts for tags|
|17874545323001329|user following|
|17851374694183129|user followers|
|17888483320059182|user posts|
|17864450716183058|likes on posts|
|17852405266163336|comments on posts|
|17842794232208280|posts on feed|
|17847560125201451|feed profile suggestions|
|17863787143139595|post suggestions|

Available parameters:
- id (user_id)
- tag_name (only one needed for explore tags)
- first (amount of nodes to get)
- after (haven't completely figured out, but looks like this is for the offset, use the cursor field)
- shortcode (used for the "on posts" queries like "likes on post")

Needed for the feedpage
- filter_followed_friends
- fetch_suggested_count
- fetch_like
- fetch_media_count
- fetch_comment_count
- fetch_media_item_count
- has_stories

**[Examples](./custom_endpoint)**

```bash
# Explore tags
https://www.instagram.com/graphql/query/?query_id=17875800862117404&variables=%7B%22tag_name%22%3A%22<tag_name>%22%2C%22first%22%3A<num_of_posts>%7D

# Note: Still have to figure out how to get this data without using selenium once logged in.
# **Only works with logged in user**

# User profile following
https://www.instagram.com/graphql/query/?query_id=17874545323001329&variables=%7B%22id%22%3A%22<user_id>%22%2C%22first%22%3A<num_of_following>%7D

# User profile followers
https://www.instagram.com/graphql/query/?query_id=17874545323001329&variables=%7B%22id%22%3A%22<user_id>%22%2C%22first%22%3A<num_of_followers>%7D

# User profile posts
https://www.instagram.com/graphql/query/?query_id=17888483320059182&variables=%7B%22id%22%3A%22<user_id>%22%2C%22first%22%3A<num_of_posts>%7D

# Post page likes
https://www.instagram.com/graphql/query/?query_id=17864450716183058&variables=%7B%22shortcode%22%3A%22<id_of_post>%22X2C%22first%22%3A<num_of_likes>%7D

# Post page comments
https://www.instagram.com/graphql/query/?query_id=17852405266163336&variables={"shortcode":"<id_of_post>","first":<num_of_comments>}

# Feed posts
https://www.instagram.com/graphql/query/?query_id=17842794232208280&variables={%22fetch_media_item_count%22:<num_of_posts>,%22fetch_comment_count%22:<num_of_comments_per_post>,%22fetch_like%22:<num_of_likers_per_post>}

# Profile suggestios in feed
https://www.instagram.com/graphql/query/?query_id=17847560125201451&variables={%22fetch_media_count%22:<num_of_posts_per_suggestion>,%22fetch_suggested_count%22:<num_of_suggestions>,%22filter_followed_friends%22:true, "has_stories":false}

# Post suggestions for user
https://www.instagram.com/graphql/query/?query_id=17863787143139595&variables={%22first%22:<num_of_posts>}
```


Stay Tuned for updates 
