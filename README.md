# img-angular-twemoji

This is a [Bower](http://bower.io/) component for using [Twitter Emoji](https://github.com/twitter/twemoji) with [Emoji Codes]
(http://emoji.codes/) in [Angular](https://angularjs.org//) as a Service, Directive & Filter for images insertion *(by default \*.svg)*.

Insert svg images into your html either by emoji unicode or by emoji "short codes".

    "I :heart: emoji!"
    
becomes
    
    "I <img class="img-twemoji" draggable="false" alt="?" src="http://twemoji.maxcdn.com/svg/2764.svg" width="72px" height="72px"> emoji"

**Files:** 

* img-angular-twemoji.js

----
## Getting Started:

1. Install *twemoji.js* via [bower](http://bower.io/) `$ bower install twemoji` or download;
2. Install *img-angular-twemoji* via [bower](http://bower.io/) `$ bower install img-angular-twemoji` or download;
3. Include both `\*.js` files into your `\*.html`;
4. Add `am.imgtwemoji` to main module's list.

----
## Usage Examples:
In your `index.html`:

	<script src="bower_components/angular/angular.js"></script>  
	<script src="bower_components/twemoji/twemoji.js"></script>   	
	<script src="bower_components/img-angular-twemoji/img-angular-twemoji.js"></script>  

In your `app.js`:

    angular.module('myApp', ['am.imgtwemoji']);

----
## As a Filter
To insert `imgtwemoji.parse(<any_string>)` that'll contain `<img/>` tags you have to use `ng-bind-html` directive.

simple filter:
 
    <p ng-bind-html="'I \ud83c\udf73 emoji!' | imgtwemoji"></p>
        
pass the size:
         
    <p ng-bind-html="'I \ud83c\udf73 emoji!' | imgtwemoji:'98x98'"></p>
             
use more friendly emoji shortcode:
         
    <p ng-bind-html="'I :egg: emoji!' | imgtwemoji:'98x98'"></p>

----
## As a Service
U can use either unicode or emoji shortcode in your input.  
If you want to embed the result in `\*.html` u need to allow it via `$sce` manually as it's already done in filter.
             
    .controller('SomeCtrl', ['imgtwemoji', function (imgtwemoji) {
                
            $scope.getTwemojiImg = function(){
                return imgtwemoji.parse('I \ud83d\udd25 emoji!');
            };
        }]);  
                   
You also can pass the options object, so it will be applied only for this particular case: 

    imgtwemoji.parse('I :heart: emoji!', opts);

----
## As a Directive 
U can pass either unicodes in html format or emoji shordcodes in your input via `code` attribute.  
U can also define such options as `size`, `class`, `draggable`:   

    <img-twemoji code='&#x1F332;' size="60x60"></img-twemoji> 

If you need to define `em`/`rem` size you can do it via `width`/`height` *(`size` field won't override those)*:
    
    <img-twemoji code=':heart:' width="4rem" height="4rem"></img-twemoji> 

> All images have `class=img-twemoji` by default.   
> So, you can define size for all images via css.   
> You also can redefine particular img class via `class` attribute.                       
    
## Configuration
For the full documentation of all options please refer to [twemoji](https://github.com/twitter/twemoji#object-as-parameter). If you like to override the default configuration use the `twemojiProvider` as follows:

    app.config(function(imgtwemojiProvider) {
      imgtwemojiProvider.setOptions({
        base: string,           // default Twitter Inc. CDN
        ext: string,            // default ".svg"
        className: string,      // default "img-twemoji"
        size: string|number,    // default "72x72" (yay, works for svg!)
        folder: string,         // default "svg"
        draggable: boolean,     // default false
        emojiToUnicode: boolean // default true (allows to use emoji short codes e.g. :heart:)
      });
    });
    
## Extras
U can use embedded [angular-emoji-map](https://github.com/mmattax/angular-emoji-map):

as filter:

    {{":heart:" | emojiToUnicode}}
   
as service:
   
    emojiToUnicode(":heart:") 
      
U can make the same tricks with `width` & `heigh` in provider config as we did in directive usage.  

U can also use `imgtwemoji.parse(input, opts)` to invoke the direct `twemoji.parse(input, opts)`, also `toCodePoint` util method.       

## Acknowledgments
Based on:
* Twitter Emoji [twemoji](https://github.com/twitter/twemoji);
* Emoji map [angular-emoji-map](https://github.com/mmattax/angular-emoji-map).    


## Copyright and license
Code and documentation copyright 2015 Andrew Mur. Code released under [the MIT license](https://github.com/andrewmur/img-angular-twemoji/blob/master/LICENSE).
