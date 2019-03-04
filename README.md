# README

Rails/PostgreSQL app. Before starting, [install Compose](https://docs.docker.com/compose/install/).

## Ruby version 
  
* `Ruby '2.5.3'`
* `Rails '5.2.2'`

## Configuration

If you are running Docker on Linux, the files rails new created are owned by root. This happens because the container runs as the root user. If this is the case, change the ownership of the new files.

```sh
sudo chown -R $USER:$USER .
```

> In linux you need run the docker commands with `sudo`

## Build the image

```sh
$ docker-compose build
```

## Up the apllication

To boot or restart the application run `docker-compose up` in the project directory.

## Database creation 

You need up the aplication before, and in another terminal, run.

```sh
$ docker-compose run web rake db:create
```

## Stop the application

To stop the application, run `docker-compose down` in your project directory. You can use the same terminal window in which you started the database, or another one where you have access to a command prompt. This is a clean way to stop the application.

## Rebuild the application

If you make changes to the Gemfile or the Compose file to try out some different configurations, you need to rebuild. Some changes require only `docker-compose up --build`, but a full rebuild requires a re-run of `docker-compose run web bundle install` to sync changes in the `Gemfile.lock` to the host, followed by `docker-compose up --build`.

Here is an example of the first case, where a full rebuild is not necessary. Suppose you simply want to change the exposed port on the local host from `3000` in our first example to `3001`. Make the change to the Compose file to expose port `3000` on the container through a new port, `3001`, on the host, and save the changes:

`ports: - "3001:3000"`

### Rebuild and restart the app with 
```sh
$ docker-compose up --build
```

Inside the container, your app is running on the same port as before `3000`, but the Rails Welcome is now available on `http://localhost:3001` on your local host.

### To use the rails commands 

```sh
$ docker-compose run --rm web + command
```

# Running specs

### Default: Run all spec files (i.e., those matching spec/**/*_spec.rb)
```sh
$ docker-compose run --rm web bundle exec rspec
```
### Run all spec files in a single directory (recursively)
```sh
$ docker-compose run --rm web bundle exec rspec spec/models
```

### Run a single spec file
```sh
$ docker-compose run --rm web bundle exec rspec spec/controllers/accounts_controller_spec.rb
```

### Run a single example from a spec file (by line number)
```sh
$ docker-compose run --rm web bundle exec rspec spec/controllers/accounts_controller_spec.rb:8
```

### See all options for running specs
```sh
$ docker-compose run --rm web bundle exec rspec --help
```


> References
* [Gem Rspec-rails](https://github.com/rspec/rspec-rails)
* [Docker Compose Rails](https://docs.docker.com/compose/rails/)
* [Guide Ruby on Rails](https://guides.rubyonrails.org/getting_started.html)