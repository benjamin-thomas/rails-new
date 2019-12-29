# Quickly create a new rails project with docker-compose

Based on the setup workflow at: https://docs.docker.com/compose/rails/


## Step 1: Clone as new project

Per: https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository
Or: https://stackoverflow.com/questions/30001304/clone-git-repository-without-history/30001366

    mkdir ~/code/my_new_app
    git clone --depth 1 https://github.com/benjamin-thomas/rails-new.git
    rm -rf ./.git

## Step 2: Update config values

- Dockerfile: lock ruby version + underlying Debian stable version
- docker-compose.yml: change listening IP (`services > web > ports`)

## Step 2: Initialize the new app

    docker-compose run web rails new . --force --no-deps --database=postgresql
    sudo chown -R $USER:$USER .
