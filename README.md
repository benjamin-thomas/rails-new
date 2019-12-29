# Quickly create a new rails project with docker-compose

Based on the setup workflow at: https://docs.docker.com/compose/rails/

## Step 1: Clone as new project

    mkdir ~/code/my_new_app
    git clone --depth 1 https://github.com/benjamin-thomas/rails-new.git .
    rm -rf ./.git
    rm README.md

## Step 2: Update config values

- Dockerfile: lock ruby version + underlying Debian stable version
- docker-compose.yml: change listening IP (`services > web > ports`)
- Gemfile: rails version (warning: avoid buggy 2.7 and broken bundler v2 config, see: https://github.com/bundler/bundler/issues/7494)

Then add first commit:

    git init .
    git add .
    git commit -m 'Initial commit'
    git remote add origin git@github.com:benjamin-thomas/my_new_app.git
    git push -u origin master

## Step 3: Initialize the new app

    docker-compose build --no-cache # Do this if rebuilding existing repo
    docker-compose run --rm web bash # check rails version

    docker-compose run web rails new . --force --no-deps --database=postgresql # if requires bundle exec, see buggy 2.7 note above
    sudo chown -R $USER:$USER .

## Step 4: Start developing

    docker-compose up
    docker-compose run --rm web bash
