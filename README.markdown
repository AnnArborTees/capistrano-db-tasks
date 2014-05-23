CapistranoDbTasks
=================

Add database AND assets tasks to capistrano to a Rails project.
It only works with capistrano 3. Older versions until 0.3 works with capistrano 2.

Currently

* It only supports mysql and postgresql (both side remote and local)
* Synchronize assets remote to local and local to remote

Commands mysql, mysqldump (or pg_dump, psql), bzip2 and unbzip2 must be in your PATH

Feel free to fork and to add more database support or new tasks.

Changes from original
=======
Removed all ability to override production data


Install
=======

Add it as a gem:

```ruby
    gem "capistrano-db-tasks", require: false
```

Add to config/deploy.rb:

```ruby
    require 'capistrano-db-tasks'

    # if you haven't already specified
    set :rails_env, "production"

    # if you want to remove the dump file after loading
    set :db_local_clean, true

    # If you want to import assets, you can change default asset dir (default = system)
    # This directory must be in your shared directory on the server
    set :assets_dir, %w(public/assets public/att)
    set :local_assets_dir, %w(public/assets public/att)

    # if you want to work on a specific local environment (default = ENV['RAILS_ENV'] || 'development')
    set :locals_rails_env, "production"
```

Add to .gitignore
```yml
    /db/*.sql
```

Available tasks
===============

    app:local:sync      || app:pull     # Synchronize your local assets AND database using remote assets and database

    assets:local:sync   || assets:pull  # Synchronize your local assets using remote assets
    
    db:local:sync       || db:pull      # Synchronize your local database using remote database data
    
Example
=======

    cap db:pull
    cap production db:pull # if you are using capistrano-ext to have multistages


Contributors
============

* tilsammans (http://github.com/tilsammansee)
* bigfive    (http://github.com/bigfive)
* jakemauer  (http://github.com/jakemauer)
* tjoneseng  (http://github.com/tjoneseng)


Copyright (c) 2009 [Sébastien Gruhier - XILINUS], released under the MIT license
