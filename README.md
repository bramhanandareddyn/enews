# eNews CMS

eNews is a ready-to-deploy News Portal CMS project written in Ruby on Rails. You will only need to create view files to put a news portal into production. eNews is ready to be used with Heroku and AWS (Amazon Web Service). So that means you will need to have one Heroku account and one AWS S3 account to start journey. I started project in third quarter of July 2013. Let's see if there will be any contribution.

## Installation

Firstly, clone the project to your local development environment:

```console
git clone https://github.com/scaryguy/enews.git
cd enews
bundle install
```
> You should set up your `database.yml` properly. PostgreSQL is recommended as your database.

You should create `config/application.yml` and define your ENV variables inside it.

```yaml
# Add account credentials and API keys here.
# See http://railsapps.github.io/rails-environment-variables.html
# This file should be listed in .gitignore to keep your settings secret!
# Each entry sets a local environment variable and overrides ENV variables in the Unix shell.
# For example, setting:
# GMAIL_USERNAME: Your_Gmail_Username
# makes 'Your_Gmail_Username' available as ENV["GMAIL_USERNAME"]
# Add application configuration variables here, as shown below.
#
ADMIN_NAME: <here comes admin user name>
ADMIN_EMAIL: <here comes admin email>
ADMIN_PASSWORD: <here comes admin password>
ROLES:
  - admin
  - user
  - editor
  - columnist
UNCATEGORIZED: <here comes UNCATEGORIZED category title>
AWS_BUCKET: <here comes AWS bucket name>
AWS_ACCESS_KEY_ID: <here comes AWS access key ID>
AWS_SECRET_ACCESS_KEY: <here comes AWS secret access key>
```

Setup DB to create necessary DB structure:

```console
rake db:setup
```

Now you should be able to run the application locally:

```console
rails s
```

Try to browse:
```code
http://localhost:3000
```

# For production installation

Create a Heroku application:

```console
heroku create
```

Create your database:

```console
heroku addons:add heroku-postgresql:dev
```

If you get this error:
>could not connect to server: Connection refused
>Is the server running on host "127.0.0.1" and accepting
>TCP/IP connections on port xxxx?
be sure that your `DATABASE_URL` environment variable is set properly inside your Heroku config.

```console
heroku config
```

You should enable user env compile:

```console
heroku labs:enable user-env-compile -a YOUR_APP
```

You should set ENV variables at Heroku. Fourtanetly, you can do it easily with Figaro gem:

```console
rake figaro:heroku
```

```console
git push heroku master
heroku run rake db:schema:load
heroku run rake db:seed
```

Now you should be able to run the application.

Cheers!


## Contributing

If you make improvements to this application, please share with others.

* Fork the project on GitHub.
* Make your feature addition or bug fix.
* Commit with Git.
* Send the author a pull request.

If you add functionality to this application, create an alternative implementation, or build an application that is similar, please contact me and I'll add a note to the README so that others can find your work.

## Credits

scaryguy, Istanbul, Turkey - 2013

## License

Not sure  :)
