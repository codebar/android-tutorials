# Codebar Android Workshop Resources

## Getting started

This is a [GitHub Pages](https://pages.github.com/) repo, so you can render the pages with [Jekyll](https://jekyllrb.com/). First make sure to [install Ruby](https://www.ruby-lang.org/en/documentation/installation/) and then the [bundler](https://bundler.io/) gem. Then:

1. `bundle install`, which will install Jekyll.
2. `bundle exec jekyll serve --watch`
3. go to <http://localhost:4000/android-tutorials/>

You are now ready to make changes!

You could also use your favorite manager, `chruby`, `rbenv`, `rvm`, etc. For [RVM](https://rvm.io/rvm/install), follow the [quick installation guide](https://rvm.io/rvm/install#quick-guided-install) and then run:

```bash
$ rvm install 2.2.1  # inside `codebar/tutorials` folder
$ rvm gemset use codebar-tutorial --create
$ gem install bundler
$ bundle install
$ jekyll serve  # go to http://127.0.0.1:4000/android-tutorials/
```
