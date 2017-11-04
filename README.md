# OK Log Buildpack

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks) that will download [OK Log](https://github.com/oklog/oklog) into your heroku app.

You'll probably want to use this with the [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) features on heroku:

```sh
heroku buildpacks:add --index 1 https://github.com/zombor/heroku-oklog-buildpack --app <your-app>
```

Then redeploy your app. `oklog` will be available in your `$PATH`.

You can use this in your `Procfile`:

```
web: <your-app> 2>&1 | tee >(oklog forward $OKLOG_HOST)
```

We use `$OKLOG_HOST` above as a config var set with `heroku config`. This kind of `Procfile` will output to both your STDOUT as well as your oklog forwarder which means your `heroku logs` will still work.
