Current Version: 0.36.1-Alpha

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

  TinyMCE paste plugin - (optional) if you want to autocheck on paste

#### Plugin name:

  languagetool

#### Toolbar item name:

  languagetool 

#### Options:

  lt_url =  The url of the LanguageTool installation. (Defaults to public server)
  
  lt_timer = Sets the timeout to process spelling and grammar in milliseconds (Defaults to 10000 which equals 10 seconds) DO NOT LOWER THIS UNLESS YOU USE YOUR OWN INSTALLATION
  
  lt_lang = Sets the language (Defaults to en-US) (You can use 'auto' to have languagetool detect automatically)
  
  lt_mode = Sets the processing mode (Defaults to new_sentece)
  
     Available modes:
	
	    new_sentece = Processing starts on new line, period, exclamation mark and question mark.
	    new_word = Processing starts same as above plus comma and space. (not suggested on public instance)
	    manual = Processing will be done manually with mceLTProcess command.

  lt_viewport_process = Sets the viewport processing mode (Defaults to disabled)

     Available modes:

	    disabled = Will process the entire document off the bat. (Long initial load)
	    only = Will process only the stuff in your viewport. (Fast initial load, slight influence on scroll performance)
	    nearby = Will process only the stuff in your viewport plus one screen up and down. (Fast initial load, slight influence on scroll performance)
            temp = Used internally to replicate disabled

  WARNING: During only and nearby modes, the Progressbar will only show issues it found in the viewport or nearby. When Dialog is opened, only and nearby mode are temporarily disabled into temp mode and all issues will be loaded. Once dialog is closed, mode will be restored.

You can also manually turn on and off temp mode via execCommand. See below.
  
  lt_highlight = Object that sets the classes for the highlighting [It is best to edit the CSS instead of touching this]

  lt_monopolize_highlight_contextmenu = When true, this will hide the contextmenu plugin and prevent all furthur events on the 'contextmenu' event when you click on highlighted words/phrases (Defaults to true)

  lt_highlight_click = Set which click you wish the context menu to be tiggered on, possible options include: left or right (Defaults to right)
  
  lt_full_message = If set to true, will force to use the long message descriptions, if false it will use the short descriptions and if not available, only then use the long ones (Defaults to false)

  lt_size_of_instances = Set content length limit sent to LanguageTool per request. (Defaults to 10000 for public server and 25000 for private) DO NOT INCREASE THIS UNLESS YOU USE YOUR OWN INSTALLATION

  lt_max_instances = How many instance are allowed in parrelel [They will still respect the timers] (Defaults to 1 for public server and 2 for private server)

  lt_show_progress_bar = Show the progress bar (Defaults to true)

  lt_debug = Set debug level (Defaults to 0 = off)
  
  lt_postdata = A HASH/ASSOCIATED ARRAY which appends to the posting of LanguageTool. 

    Example: lt_postdata:{ disabledRules:"MORFOLOGIK_RULE_EN_US" } 
  
    See more at: https://languagetool.org/http-api/swagger-ui/#!/default/post_check
  
  lt_ignore_callback = Callback that is called when Ignore Rule or Ignore All is called. You should probably store it in localstorage or in the document if you wish to save user preferences. Callback first parameter is 'addRule', 'addWord', 'removeRule', 'removeWord' and second parameter is the word or rule in question.
  
  lt_ignore_words = A HASH/ASSOCIATED ARRAY of words/phrases to ignore
  
  lt_ignore_rules = A HASH/ASSOCIATED ARRAY of rules to ignore

  lt_ignore_block_tags = A HASH/ASSOCIATED ARRAY which sets a block list for tags you don't want UUIDs assigned to. [This is advanced functionality ment to filter out block containers, for example, you may be making your content divided into chapters via section tag. Currently section tag would force the entire content to be sent to the system instead of dividing it up. By including the section tag to be ignored, it would then default back to the P tags]

    Example: lt_ignore_block_tags:{ 'SECTION':1 } 
    
  lt_ignore_selector = Same as above but uses selectors instead of a HASH of tags
  
    Example: lt_ignore_selector:'section, header, article' 

#### Commands:

  mceLTDisable = Disable new content from entering the LT processing queue

  mceLTEnable = Enable new content to enter the LT processing queue

  mceLTProcess = Process manually

  mceLTViewportProcessDisable = Turn on temp mode for viewport_process

  mceLTViewportProcessEnable = Go back to original mode for viewport_process

#### Syntax:

```
  <script>  
  tinymce.init({  
    selector: "#mytextarea",  
    toolbar: 'undo redo | styleselect | bold italic | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | languagetool',  
    height: 700,  
    plugins: ['languagetool paste']  
  });  
  </script>
```

#### Demo:

This demo uses this plugin via external_plugin hosted by github, which is not the recommended way to go, especially since github is not a cdn. Add the plugin to your plugins folder and include languagetool

  https://knowzero.github.io/tinymce4-languagetool/demo.html
  
A TinyMCE 5 quick port has also been done, but TinyMCE4 version is suggested:

  https://knowzero.github.io/tinymce4-languagetool/TinyMCE5/demo.html

