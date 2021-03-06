Social JS 0.6.0
==================
Social JS is a jQuery plugin to easily create share buttons for the most common social media sites. It's built in a way that requires almost no knowledge in javascript but depends instead of the use of data attributes.

[View Demo](http://andreasnorman.com/socialjs/)

<div style="text-align:center">
<img src="https://github.com/SubZane/socialjs/raw/master/demo/img/logo.png" alt="Social JS"/>
</div>


##Features
* Twitter
* Facebook
* LinkedIn
* Google Plus
* Reddit
* Can fetch share count for each social media. Requires server side client to provide a count for Google Plus. A PHP client is provided.

##Browser Support
* Google Chrome
* Internet Explorer 8+
* Firefox
* Safari 6+

##Installation
```
bower install socialjs --save
```

###Setup
```html
<!-- You'll need jquery -->
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
<!-- and you'll need to include socialjs of course! -->
<script src="jquery.socialjs.min.js"></script>
```
##Usage
```javascript
$('#id_of_your_div').socialjs();
```

###Settings and Defaults
```javascript
options: {
  fetchCounts: true,
  GooglePlusAPIProvider: 'backend/GooglePlusCall.php',
  shortCount: true,
  onInit: function () {},
  onLoad: function () {},
  onClick: function(){},
  onDestroy: function () {}
};
```
* `fetchCounts`: Default true. If the plugin should fetch share count or not.
* `shortCount`: Default true. Show total by k or M when number is to big.
* `GooglePlusAPIProvider`: Path to server side google plus client.
* `onInit`: Executes when initialized.
* `onLoad`: Executes when finished loading all buttons and counts.
* `onClick`: Executes when user clicks any share button.
* `onDestroy`: Executes when plugin is removed/destroyed.

###Required classes, data-attributes and elements.
* `.sharebutton`: Required. Class of the `<a href>` element containing all data-attributes.
* `data-sharetype`: Required. To tell the script what social media it is. Supports twitter, facebook, linkedin or googleplus
* `data-basecount`: Optional. If you want to cheat or have moved pages or switched domain but want to keep the old count you can add this and specify a number
* `data-text`: Optional. If not specified the plugin will take the title of the page as text.
* `data-via`: Only for Twitter. Optional. The creator of the content. Usually your twitter name without the @
* `data-related`: Only for Twitter. Optional. The creator of the content. Usually your twitter name without the @

If you want a count to be presented you'll need to add a `span` element inside the `<a href>`

###Public methods
Exposed methods that you can access and use. The count methods is best to use within the `onLoad` hook since the count will be fetched by and Ajax request.
* `option`: option,
* `destroy`: destroy,
* `getTotalCount`: getTotalCount,
* `getFacebookCount`: getFacebookCount,
* `getGooglePlusCount`: getGooglePlusCount,
* `getLinkedinCount`: getLinkedinCount,
* `getTwitterCount`: getTwitterCount
* `getRedditCount`: getTwitterCount

####How to use a public method
In this example we alert the count of all twitter shares.
```javascript
jQuery(document).ready(function($) {
  $('.socialjs').socialjs({
    onLoad: function() {
      alert($('.socialjs').socialjs('getTwitterCount'));
    }
  });
});
```

###Typical setup
This could be your typical script setup for a twitter share button.

```javascript
jQuery(document).ready(function($) {
  $('.socialjs').socialjs();
});
```

```html
<div class="socialjs">
  <a class="sharebutton twitter" data-basecount="249" data-sharetype="twitter" data-text="The neat page title" data-via="andreasnorman" data-related="andreasnorman" title="Share this on Twitter" href="#"><span class="count"></span></a>
</div>
```

###About server side Google Plus clients
Currently I have only written one in PHP but you can write your own in any language really. The only thing you need to know is that the expected return value from the client is a number and nothing else.

If you want to contribute with a C# client or a client in any other language please do! Just fork and pull request.

##change log
####0.6.0
* Added support for Reddit
* Renamed to Social JS since SimpleShareButtons already existed

####0.5.0
* First real public release
