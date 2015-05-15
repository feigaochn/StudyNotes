- database: `DATABASE_URL`

- database creation / migration / upgrade
	- local: 

	```sh
	python manage.py db init
	python manage.py db migrate
	python manage.py db upgrade
	```

	- remote: *only* run `upgrade`

	```sh
	heroku addons:add heroku-postgresql:dev --app MY-APP-NAME
	git push heroku master
	heroku run python manage.py db upgrade --app MY-APP-NAME
	```
