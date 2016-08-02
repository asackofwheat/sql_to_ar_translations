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
At least one should use an aggregate function (e.g. COUNT) and at least one should use GROUP.

The user with the first name 'Tom' with the most number of posts:

1. User.select('COUNT(\*) AS post\_count, user.id, user.full\_name').where(:first_name => 'Tom').joins(:posts).group('user.id, user.full\_name').order('post\_count DESC').limit(1)

```sql
SELECT user.id, user.full\_name, COUNT(*) AS post\_count
  FROM users JOIN posts ON user.id=posts.author_id
 WHERE user.first_name='Tom'
 GROUP BY user.id, user.full\_name
 ORDER BY post\_count DESC
 LIMIT 1
```

The most used category

2. Post.select('COUNT(*) AS category_count, category').group('category').order('category\_count DESC').limit(1)

```sql
SELECT category, COUNT(*) AS category_count
  FROM posts
 GROUP BY category
 ORDER BY category\_count DESC
  LIMIT 1
```

All the users whose first names start with Mike.

3. User.where("first_name LIKE 'Mike%'")

```sql
SELECT *
 FROM users
 WHERE first_name LIKE 'Mike%'
```