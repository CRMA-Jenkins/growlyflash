# Growlyflash

The growlyflash gem turns boring [ActionDispatch::Flash](http://api.rubyonrails.org/v3.2.14/?q=ActionDispatch::Flash) messages in your Rails 3 app to asynchronous Growl-like notifications with [Bootstrap Alert](http://getbootstrap.com/2.3.2/components.html#alerts) markup.

With XHR requests it places flash hash to the `X-Messages` HTTP header or inline in javascript.

Based on rewritten in coffeescript [Bootstrap Growl](https://github.com/ifightcrime/bootstrap-growl) plugin and inspired by [Bootstrap Flash Messages](https://github.com/RobinBrouwer/bootstrap_flash_messages)

## Installation

Add this line to your application's Gemfile:
````ruby
gem 'growlyflash'
````
And then execute:
````
$ bundle
````
For non-XHR requests append the following before other javascripts inside `<head>`:
````erb
<%= growlyflash_static_notices %>
````
And require glowlyflash in `app/assets/javascripts/application.js`
````js
//= require growlyflash/growlyflash
````

## Customize

If you want to change default options, you can override them somewhere in your coffee/js:
````coffee
$.bootstrapGrowl.defaults = $.extend on, $.bootstrapGrowl.defaults,
  # Box width (number or css-like string, etc. "auto")
  width:       250
  
  # Auto-dismiss timeout. Set it to 0 if you want to disable auto-dismiss
  delay:       4000
  
  # Spacing between boxes in stack
  spacing:     10
  
  # Appends boxes to a specific container
  target:      'body'
  
  # Show close button
  dismiss:     true
  
  # Default class suffix for alert boxes.
  type:        null
  
  # Use the following mapping (Flash key => Bootstrap Alert)
  type_mapping:
    warning: null
    error  : 'error'
    notice : 'info'
    success: 'success'
  
  # Horizontal aligning (left, right or center)
  align:       'right'
  
  # Margin from the closest side
  alignAmount: 20
  
  # Offset from window bounds
  offset:      
    from:      'top'
    amount:    20
````

Insert the following if you want to close alert boxes by clicking on themselves. 
Also it doesn't steel focus from toggled elements like dropdowns and works fine with touch devices, 
so I advise to use it:
````coffee
jQuery ->
  # ...
  $(document).on 'click.alert.data-api', '[data-dismiss="alert"]', (e) -> 
    e.stopPropagation()
  
  $(document).on 'touchstart click', ".bootstrap-growl", (e) -> 
    e.stopPropagation()
    $('[data-dismiss="alert"]', @).click()
    off
````

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
