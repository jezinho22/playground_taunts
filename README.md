#Playground Taunts dot com

- Post your proposed names for your child and find out what the nicknames might be - is it worth the risk?

```
CREATE TABLE IF NOT EXISTS user_profile 
( id SERIAL PRIMARY KEY,
  username VARCHAR(255),
  clerk_id VARCHAR(255),
  first_name TEXT,
  last_name TEXT,
  UNIQUE (clerk_id)
  )

CREATE TABLE IF NOT EXISTS child_names
( id SERIAL PRIMARY KEY,
  clerk_id VARCHAR(255) REFERENCES user_profile(clerk_id),
  first_name TEXT,
  last_name TEXT,
  comment TEXT  )

  CREATE TABLE IF NOT EXISTS comments
( id SERIAL PRIMARY KEY,
  clerk_id VARCHAR(255) REFERENCES user_profile(clerk_id),
  post_id INT references child_names(id),
  comment TEXT
  )

  CREATE TABLE IF NOT EXISTS comment_likes
  ( id SERIAL PRIMARY KEY,
  clerk_id VARCHAR(255) REFERENCES user_profile(clerk_id),
  post_id INT references child_names(id),
  comment_id INT REFERENCES comments(id),
  vote TEXT
  )

  CREATE TABLE IF NOT EXISTS child_name_likes
( id SERIAL PRIMARY KEY,
  clerk_id VARCHAR(255) REFERENCES user_profile(clerk_id),
  post_id INT references child_names(id),
  vote TEXT
  )

INSERT INTO user_profile (username, clerk_id, first_name, last_name)
VALUES ('jezinho', 'jo2327R4', 'Jez', 'Johns'),
('dibster', 'nl60xct', 'Lily', 'Johns')

select * from user_profile

INSERT INTO child_names 
(clerk_id, first_name, last_name, comment)
VALUES ('jo2327R4', 'Christopher', 'Peacock', 'Boy'),
('jo2327R4', 'Andrew', 'Peacock', 'Boy'),
('jo2327R4', 'Louise', 'Peacock', 'Girl'),
('nl60xct', 'Paul', 'Lee', 'Boy'),
('nl60xct', 'Kevin', 'Lee', 'Boy'),
('nl60xct', 'Kai', 'Lee','Boy')

# your own posts and the comments
SELECT child_names.first_name, child_names.last_name, child_names.comment AS post_comment, user_profile.username, comments.comment 
FROM child_names 
JOIN user_profile ON child_names.clerk_id = user_profile.clerk_id
JOIN comments ON comments.post_id = child_names.id
WHERE user_profile.clerk_id = 'jo2327R4'

# comments for a user id
SELECT comments.comment, user_profile.username
FROM comments
JOIN user_profile
ON comments.author_id = user_profile.clerk_id
WHERE comments.author_id = 'nl60XCT'

# name, comment and comment author
SELECT comments.comment, user_profile.username, child_names.first_name, child_names.last_name
FROM comments
JOIN user_profile
ON comments.author_id = user_profile.clerk_id
JOIN child_names
ON comments.post_id = child_names.id

```
