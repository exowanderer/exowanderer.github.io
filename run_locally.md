1. Run `bundle clean` to clean up the directory (no need to run `--force`)
2. Run `bundle install` to install ruby dependencies. If you get errors, delete Gemfile.lock and try again.
3. Run `bundle exec jekyll liveserve` to generate the HTML and serve it from `localhost:4000` the local server will automatically rebuild and refresh the pages on change.