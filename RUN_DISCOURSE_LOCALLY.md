# Running locally
There is a docker-compose.yml that is configured to run the three pieces
necessary (redis, postgres, discourse).

`docker-compose up`

## Initial startup
Startup of the docker compose will bring in fresh redis and postgres.
One needs to run `db:create` to populate those data sources.

docker exec into docker container - `docker exec -it <container id> /bin/bash`

 * sv stop unicorn
 * cd /var/www/discourse
 * bundle exec rake db:migrate
 * sv start unicorn
 * bundle exec rake admin:create (to create admin user w/o email working)

