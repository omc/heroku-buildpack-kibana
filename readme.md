# Heroku Buildpack for Kibana

This buildpack downloads and installs Kibana into a Heroku app slug. It is a fork of [issueapp/heroku-buildpack-kibana](https://github.com/issueapp/heroku-buildpack-kibana), with some light customization for use as a one-click Heroku Button app.

For a one-click deploy of Kibana on Heroku, see [omc/heroku-kibana](https://github.com/omc/heroku-kibana).

## Compatibility

Tested versions: 5.x.y -> 6.x.y

## Usage

See our other repo at https://github.com/omc/heroku-kibana for a one-click deploy of Kibana on Heroku.

Or, to use as a standalone buildpack:

    # Create a new project with the --buildpack option
    mkdir kibana1 && cd kibana1 && git init
    heroku create kibana1 --buildpack https://github.com/omc/heroku-buildpack-kibana

    # Let Kibana know where to find Elasticsearch
    heroku config:set ELASTICSEARCH_URL="https://kibanauser:kibanapass@host.region.bonsaisearch.net"

    # Create a Procfile to run the Kibana web server
    echo 'web: kibana --port $PORT' > Procfile

    # Push the above to trigger a deploy
    git add . && git commit -am "Kibana setup" && git push heroku master

    # Open the app in your browser.  You may be prompted for a username/password, which
    # matches the username and password of your elasticsearch URL.
    heroku open


### Private Spaces + VPC Peering

If you are using VPC peering from a private space, the automatic version detection will not work, since the compile phase is run outside of the private space.

You must set the addition config vars.

    # Set the verison
    heroku config:set ELASTICSEARCH_VERSION="6.5.4"

    # Optionally set the build flavor (oss or x-pack).  This defaults to oss.
    heroku config:set ELASTICSEARCH_FLAVOR="oss"
