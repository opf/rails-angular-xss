rails-angular-xss [![Build Status](https://travis-ci.org/opf/rails-angular-xss.png?branch=master)](https://travis-ci.org/opf/rails-angular-xss)
===========

When rendering AngularJS templates with a server-side templating engine like ERB it is easy to introduce XSS vulnerabilities.
These vulnerabilities are enabled by AngularJS evaluating user-provided strings containing interpolation symbols (default symbols are `{{` and `}}`).

This gem patches ERB/rails_xss so AngularJS interpolation symbols are auto-escaped in unsafe strings.
And by auto-escaped we mean replacing `{{` with ` { { `. To leave AngularJS interpolation marks unescaped, mark the string as `html_safe`.

**This is an unsatisfactory hack.**
A better solution is very much desired, but is not possible without some changes in AngularJS. See the [related AngularJS issue](https://github.com/angular/angular.js/issues/5601).


Disable escaping locally
------------------------

If you want to disable angular_xss in some part of your app, you can use

```
Rails::AngularXss.disable do
  # no escaping here
end
# escaped again
```


Installation
------------

0. Read the code so you know what you're getting into.

1. Put this into your Gemfile

        gem 'angular_xss'

2. Run `bundle install`.

3. Run your test suite to find the places that broke.

4. Mark any string that is allowed to contain Angular expressions as `#html_safe`.


Development
-----------

- Fork the repository.
- Push your changes with specs. There is a Rails 3 test application in `spec/app_root` if you need to test integration with a live Rails app.
- Send a pull request.


Credits
-------

[Henning Koch](mailto:henning.koch@makandra.de) from [makandra](http://makandra.com/).
