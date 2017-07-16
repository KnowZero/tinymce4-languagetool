Current Version: 0.09-Alpha

This is an attempt to port the Language Tool Spelling and Grammar Check to TinyMCE4\. It also does things like highlighting as you type and etc.

Currently the code is is EXPIREMENTAL. Use at your own risk.

It is also currently set to process requests when you are on a new line or end of line, once every 10 seconds via the public Language Tool site. (But you should change it to your own server)

There is a few concepts that I am exploring here from making it work:

1 - As you type functionality  
2 - Only check for changes

The plugin already works, but I only tested it for 10 minutes of typing and trying things out. This repository exists to mostly track bugs and etc.

Once I am done coding the basic stuff, I'll clean up the code and make it more presentable.

#### Requirements:

  jQuery 1.X+

  TinyMCE 4.X

#### Plugin name:

  languagetool

#### Toolbar item name:

  languagetool 

#### Options:

  lt_url =  The url of the LanguageTool installation. (Defaults to public server)
  
  lt_timer = Sets the timeout to process spelling and grammar in milliseconds (Defaults to 10000 which equals 10 seconds) DO NOT LOWER THIS UNLESS YOU USE YOUR OWN INSTALLATION
  
  lt_lang = Sets the language (Defaults to en-US)
  
  lt_highlight = Object that sets the classes for the highlighting [It is best to edit the CSS instead of touching this]
  
  lt_debug = Set debug level (Defaults to 0 = off)
  
  lt_postdata = A HASH/ASSOCIATED ARRAY which appends to the posting of LanguageTool. 
  
  Example: lt_postdata:{ disabledRules:"MORFOLOGIK_RULE_EN_US" } 
  
  See more at: https://languagetool.org/http-api/swagger-ui/#!/default/post_check
  
  lt_ignore_callback = Callback that is called when Ignore Rule or Ignore All is called. You should probably store it in localstorage or in the document if you wish to save user preferences. Callback first parameter is 'addRule', 'addWord', 'removeRule', 'removeWord' and second parameter is the word or rule in question.
  
  lt_ignore_words = A HASH/ASSOCIATED ARRAY of words/phrases to ignore
  
  lt_ignore_rules = A HASH/ASSOCIATED ARRAY of rules to ignore

#### Syntax:

```
  <script>  
  tinymce.init({  
    selector: "#mytextarea",  
    toolbar: 'undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | languagetool',  
    height: 700,  
    plugins: ['languagetool']  
  });  
  </script>
```

#### Demo:

This demo uses this plugin via external_plugin hosted by github, which is not the recommended way to go, especially since github is not a cdn. Add the plugin to your plugins folder and include languagetool

  https://knowzero.github.io/tinymce4-languagetool/demo.html

