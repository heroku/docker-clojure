# Heroku Clojure Docker Image

This image is for use with Heroku Docker CLI.

## Usage

Your project must contain the following files:

* `project.clj` (see the [Leiningen documentation for details](https://github.com/technomancy/leiningen/blob/master/doc/TUTORIAL.md#projectclj))
* `Procfile` (see [the Heroku Dev Center for details](https://devcenter.heroku.com/articles/procfile))

Your project must be built as an [uberjar](https://github.com/technomancy/leiningen/blob/master/doc/TUTORIAL.md#uberjar).

Then create an `app.json` file in the root directory of your application with
at least these contents:

```json
{
  "name": "Your App's Name",
  "description": "An example app.json for heroku-docker",
  "image": "heroku/clojure"
}
```

Install the heroku-docker toolbelt plugin:

```sh-session
$ heroku plugins:install heroku-docker
```

Initialize your app:

```sh-session
$ heroku docker:init
Wrote Dockerfile
Wrote docker-compose.yml
```

And run it with Docker Compose:

```sh-session
$ docker-compose up web
```

The first time you run this command, `lein` will download all dependencies into
the container, build your application, and then run it. Subsequent runs will
use cached dependencies (unless your `project.clj` file has changed).

You'll be able to access your application at `http://<docker-ip>:8080`, where
`<docker-ip>` is the value of running `docker-machine ip default` if you are on Mac.
