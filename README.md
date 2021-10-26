# heroku-redis-cli-app

(Note: Instructions only valid for Redis 4 and Redis 5, as Redis 6 requires TLS connections and special configuration)

1. Create a new, empty Heroku app.
    * This process implies adding an extra buildpack and installing Redis tools, so this way it won't impact any of your existing apps.
2. In the Heroku Dashboard for your app, go to Settings>Buildpacks and add `https://github.com/heroku/heroku-buildpack-apt`
3. Create an `Aptfile` file in your app listing `redis-tools`, and a very basic `Procfile` too (example in this repo).
4. Deploy the (almost) empty app.
5. Start a one-off dyno for this app with `heroku run bash -a appname`.
6. `redis-cli` will be installed in your new app's dynos and you'll be able to use it directly to interact with your Redis instance.
7. Run `redis-cli -h HOSTNAME -p PORT -a PASSWORD`, replacing the hostname, password and port with the details from your Redis connection string.


#### Example:

```
~ % heroku run bash -a carla-private-testing
Running bash on ⬢ carla-private-testing... up, run.5828 (Private-M)

~ $ redis-cli -h xxxx -p 6379 -a zzz
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.

xxx.compute-1.amazonaws.com:6379> set a 1
OK
xxx.compute-1.amazonaws.com:6379> get a
"1"
xxx.compute-1.amazonaws.com:6379>
```
