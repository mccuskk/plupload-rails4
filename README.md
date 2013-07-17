Rails 4.0 Integration for Plupload
==

This gem integrates [Plupload](http://www.plupload.com/) with the Rails 4.0 asset pipeline.

Install
--

Just add it got your Gemfile:
```ruby
gem 'plupload-rails4'
```

Quick Start
--

Add to your application.js:

```javascript
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
```

Add to your application.scss:

```css
/*
 *= require jquery_plupload/jquery.plupload.queue
 */
```

Simple example haml for your views:
```html
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
```
ERB example
```erb
<script>
  <% session_key_name = Rails.application.config.session_options[:key] %>
  $(function() {
    $("#uploader").pluploadQueue({
      runtimes: 'html5,flash,silverlight',
      url: "<%= attachments_path %>",
      max_file_size: '20mb',
      multiple_queues: true,
      flash_swf_url: "/assets/jquery_plupload/plupload.flash.swf",
      silverlight_xap_url: "/assets/jquery_plupload/plupload.silverlight.xap",
      multipart: true,
      multipart_params: {
        '_http_accept': 'application/javascript',
        'authenticity_token' : "<%= form_authenticity_token %>",
        "<%= session_key_name %>" : encodeURIComponent("<%= u cookies[session_key_name] %>")
      },

      init: {
        FileUploaded: function(up, file, info) {
          eval(info["response"]);
        }
      }
    });
  });
</script>
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
