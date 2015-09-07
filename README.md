# ssh-private-key-buildpack

A heroku buildpack for setting the ssh private key as part of the application build. It's meant to be used with [heroku-buildpack-multi](https://github.com/heroku/heroku-buildpack-multi), before other buildpacks which require the key to be present, like installing private `npm` modules from `github`.

# Example usage

Upload the private key to heroku (note that the key needs to be base64 encoded).

``` sh-session
$ heroku config:set SSH_KEY="$(cat ~/.ssh/id_rsa)"
```

Use the Heroku Toolbelt to
[add this buildpack](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app#adding-a-buildpack).
Use `--index` to make sure the buildpack runs before any others which might need
the SSH key setup:

``` sh-session
$ heroku buildpacks:add --index 1 https://github.com/bjeanes/ssh-private-key-buildpack.git
```

Now as long as the public key is present on github and the user has the correct permissions, it's possible to install `npm` modules from private `github` repositories.
