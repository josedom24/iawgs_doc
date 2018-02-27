
apt install gcc build-essential zlib1g zlib1g-dev zlibc ruby-zip libssl-dev libyaml-dev libcurl4-openssl-dev ruby gem libapache2-mod-passenger apache2 apache2-dev libapr1-dev libxslt1-dev checkinstall libxml2-dev ruby-dev vim libmagickwand-dev imagemagick sudo rails

apt install postgresql
apt install postgresql-server-dev-9.6


cd /opt
mkdir redmine
cd redmine

wget http://www.redmine.org/releases/redmine-3.3.4.tar.gz


tar xzf ./redmine-3.3.4.tar.gz



sudo -u postgres psql postgres
CREATE ROLE redmine LOGIN ENCRYPTED PASSWORD 'your_password' NOINHERIT VALID UNTIL 'infinity';
CREATE DATABASE redmine WITH ENCODING='UTF8' OWNER=redmine;

/etc/postgresql/9.6/main/pg_hba.conf
local all postgres trust
sudo service postgresql reload

/opt/redmine/redmine-3.3.4/config/database.yml

    production:

        adapter: postgresql
        database: redmine
        host: localhost
        username: redmine
        password: your_password



bundle install
bundle exec rake generate_secret_token

RAILS_ENV=production bundle exec rake db:migrate
RAILS_ENV=production bundle exec rake redmine:load_default_data


bundle exec ruby /usr/bin/rails server -b 10.0.0.13 -p 8080 -e production


## apache

cd /opt/
sudo chown -R www-data:www-data /opt/redmine
cd /opt/redmine/redmine-3.3.4
sudo chmod -R 755 files log tmp public/plugin_assets
sudo chown www-data:www-data Gemfile.lock
sudo ln -s /opt/redmine/redmine-3.3.4/public/ /var/www/html/redmine



sudo nano /etc/apache2/sites-available/master.conf

    <VirtualHost *:80>

    ServerAdmin admin@example.com
    Servername hostname
    DocumentRoot /var/www/html/

    <Location /redmine>
    RailsEnv production
    RackBaseURI /redmine
    Options -MultiViews
    </Location>

    </VirtualHost>



sudo a2dissite 000-default.conf
sudo a2ensite master.conf


/etc/apache2/mods-available/passenger.conf

    PassengerUser www-data

sudo service apache2 restart




