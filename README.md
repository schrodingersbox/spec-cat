# schrodingersbox/spec-cat

This gem contains trivial matchers to make RSpecs a bit more effective and annoying.

 * eql_file
 * have_a_spec

 NOTE: This gem does not depend on Rails.  All paths are relative to cwd, which
 may be Rails.root or anywhere else.

## Getting Started

Add this to your gemfile...

      gem 'spec-cat', :git => 'https://github.com/schrodingersbox/spec-cat.git'

## Matchers

### eql_file

`eql_file` will compare method output to a ground truth file and fail if they
are different.

It also writes a .tmp file to replace the old ground truth if it's gone stale.

e.g.  #foo produces a gnarly string too nasty to copy and paste into code.

     foo.should eql_file( 'spec/data/foo.json' )

... if it fails for a valid change, you can just....

    cp spec/truth/foo.json.tmp spec/truth/foo.json

... and all will be good again.

This mechanism is a bit brittle, but great for big blobs of data.

If you use this, you should add `*.tmp` to your .gitignore.

### have_a_spec

`have_a_spec` will ensure that any given path has a corresponding spec file to
help ensure that you have good coverage.

    'app/controllers/application_controller.rb'.should have_a_spec

... is a good thing to write right after you integrate RSpec.

Here's an example coverage spec...

<https://github.com/schrodingersbox/spec-cat/blob/master/spec/coverage_spec.rb>

## Rake Tasks

### spec-cat:accept

`rake spec-cat:accept` runs all specs and causes the eql_file matcher to overwrite
the ground truth files, rather than output .tmp files.

This is convenient when a code change impacts a large number of ground truth files,
but is also risky, as it may allow an incorrect change to become ground truth.

### spec-cat:coverage

`rake spec-cat:coverage` runs all specs and then opens the coverage report if all the
specs pass.

## Reference

 * [RSpec](https://github.com/rspec/rspec)
 * [Testing Rake Tasks with RSpec](http://www.philsergi.com/2009/02/testing-rake-tasks-with-rspec.html)
 * [Nathan Humbert's Blog: Rails 3: Loading rake tasks from a gem](http://blog.nathanhumbert.com/2010/02/rails-3-loading-rake-tasks-from-gem.html)

## TODO

 * Add helper method to accept ground truth files  - "cp #{path}.tmp #{path}"
 * Add more matchers
 * Publish to rubygems.org


