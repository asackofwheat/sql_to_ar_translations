Matt and Mike

SQL TO ACTIVE RECORD

1. User.all

2. User.find(1)

3. User.order('created_at DESC').limit(1)

4. User.joins('JOIN posts ON posts.author_id = users.id').where('posts.created_at >= 2014-08-31 00:00:00')

5. User.select('count(*) AS color_count').group(:favorite_color).having('color_count > 1')

6. User.order('updated_at DESC').limit(1)

7. User.order('age DESC').limit(1)

8. User.all

9. Post.order('created_at DESC')

ACTIVE RECORD TO SQL

1. SELECT *
FROM posts

2. SELECT *
FROM posts
ORDER BY posts.id
LIMIT 1

3. SELECT *
FROM posts
ORDER BY posts.id DESC
LIMIT 1

4. SELECT *
FROM posts
WHERE id = 4

5. SELECT *
FROM posts
WHERE id = 4
LIMIT 1

6. SELECT COUNT(*) AS user_count
FROM users

7. SELECT name
FROM posts
WHERE created_at > CURRENT_DATE - 3
ORDER BY created_at

8. SELECT COUNT(*)
FROM posts
GROUP BY category_id

9. SELECT *
FROM posts
WHERE created_at < '2014-1-1'

10. SELECT DISTINCT authors.first_name, COUNT(posts.author_id) AS count_posts
FROM posts JOIN authors ON posts.author_id = authors.id
HAVING count_posts >= 3

11. SELECT *
FROM posts
WHERE title LIKE 'The %'

12. SELECT *
FROM posts
WHERE id IN (3,5,7,9)

CUSTOM TRANSLATIONS

1. 

2. 

3. 