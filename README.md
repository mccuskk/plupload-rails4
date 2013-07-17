Rails 4.0 Integration for Plupload
==

This gem integrates [Plupload](http://www.plupload.com/) with the Rails 4.0 asset pipeline.

Install
--

Just add it got your Gemfile:
```
  gem 'plupload-rails4'
```

Quick Start
--

Add to your application.js:

  //= require jquery_plupload/plupload

  // optional, only needed if you'd like to use plupload localized
  //= require jquery_plupload/i18n/de

  // optional, only if you want to use the jquery integration
  //= require jquery_plupload/jquery.plupload.queue

  // optional, choose the ones you'd like to use
  //= require jquery_plupload/plupload.flash
  //= require jquery_plupload/plupload.silverlight
  //= require jquery_plupload/plupload.html4
  //= require jquery_plupload/plupload.html5
  //= require jquery_plupload/plupload.gears
  //= require jquery_plupload/plupload.browserplus


Add to your application.scss:

  *= require jquery_plupload/jquery.plupload.queue


Simple example haml for your views:

  div#uploader
  javascript:
    $(function(){
      $("#uploader").pluploadQueue({
        runtimes: 'gears,flash,silverlight,browserplus,html5',
        url: '#{images_path}',
        multipart_params: {
          '#{request_forgery_protection_token}': '#{form_authenticity_token}',
          '#{request.session_options[:key]}': '#{request.session_options[:id]}'
        }
      });
    });

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
