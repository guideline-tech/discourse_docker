docker-compose up
exec into docker container

 * sv stop unicorn
 * cd /var/www/discourse
 * bundle exec rake db:migrate
 * sv start unicorn
 * bundle exec rake admin:create (to create admin user w/o email working)

