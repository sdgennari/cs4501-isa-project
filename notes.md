# Setup Commands
- `mkdir test-db`
- `docker run --name mysql-test -d -e MYSQL_ROOT_PASSWORD='$3cureUS' -v C:/Users/sdgennari/cs4501/test-db:/var/lib/mysql mysql:5.7.14`
- `docker run -it --name mysql-test-cmdline --link mysql-test:db mysql:5.7.14 bash`
- In the mysql-test-cmdline container:
	- `mysql -uroot -p'$3cureUS' -h db`
	- In mysql:
		- `create user 'www'@'%' identified by '$3cureUS';`
		- `create database cs4501 character set utf8;`
		- `grant all on cs4501.* to 'www'@'%';`
- `docker run -it --name web --link mysql-test:db -v C:/Users/sdgennari/cs4501/app:/app tp33/django`
- In web container:
	- `cd sampleProject/`
	- `python manage.py migrate`
	- `mod_wsgi-express start-server --working-directory /app/sampleProject/ /app/sampleProject/sampleProject/wsgi.py &`


# Helpful Info
- `docker logs <container_name>`
	- Show logs for container
	- Useful when debugging why a container did not start