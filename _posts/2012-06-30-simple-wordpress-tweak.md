---
title: Simple WordPress Tweaks for your Site
author: Bob Orchard
excerpt: "Customizing your client's deployment of a Wordpress website doesn't need to be all that difficult. In fact - you can customize your client's installation of Wordpress at the same time you create the design & theme for them."
layout: post
permalink: /articles/simple-wordpress-tweak/
dsq_thread_id:
  - 1018373506
categories:
  - Articles
---
Customizing your client's deployment of a WordPress website doesn't need to be all that difficult. In fact &#8211; you can customize your client's installation of WordPress at the same time you create the design & theme for them.

<!--more-->

### Change &#8216;Posts' to &#8216;Articles'

[sourcecode language=&#8221;php&#8221;]

add\_filter( &#8216;gettext', &#8216;change\_post\_to\_article' );  
add\_filter( &#8216;ngettext', &#8216;change\_post\_to\_article' );

function change\_post\_to_article( $translated ) {  
$translated = str_ireplace( &#8216;Post', &#8216;Article', $translated ); // ireplace is PHP5 only  
$translated = str_ireplace( &#8216;Articleal', &#8216;Postal', $translated ); // Gravityforms &#8211; correct &#8216;postal code text'  
return $translated;  
}

[/sourcecode]

###  Removing &#8216;Links' from the Sidebar

[sourcecode language=&#8221;php&#8221;]

add\_action( &#8216;admin\_menu', &#8216;tp\_admin\_menu' );  
function tp\_admin\_menu() {  
remove\_menu\_page(&#8216;link-manager.php');  
}

[/sourcecode]

### Adding your RSS Feed to their Dashboard

Getting news out to your clients is extremely important &#8211; make sure they get yours!

[sourcecode language=&#8221;php&#8221;]

add\_action(&#8216;wp\_dashboard\_setup', &#8216;tp\_dashboard_widgets');  
function tp\_dashboard\_widgets() {  
global $wp\_meta\_boxes;  
// remove unnecessary widgets  
// var\_dump( $wp\_meta_boxes[&#8216;dashboard'] ); // use to get all the widget IDs  
unset(  
$wp\_meta\_boxes\[&#8216;dashboard'\]\[&#8216;normal'\]\[&#8216;core'\]\[&#8216;dashboard_plugins'\],  
$wp\_meta\_boxes\[&#8216;dashboard'\]\[&#8216;side'\]\[&#8216;core'\]\[&#8216;dashboard_secondary'\],  
$wp\_meta\_boxes\[&#8216;dashboard'\]\[&#8216;side'\]\[&#8216;core'\]\[&#8216;dashboard_primary'\]  
);  
// add a custom dashboard widget  
wp\_add\_dashboard\_widget( &#8216;dashboard\_custom\_feed', &#8216;News from Tinypint', &#8216;dashboard\_tp_rss' ); //add new RSS feed output  
}  
function dashboard\_tp\_rss() {  
echo &#8216;</pre>  
<div class="rss-widget">';  
wp\_widget\_rss_output(array(  
&#8216;url' => &#8216;http://feeds.feedburner.com/tinypint',  
&#8216;title' => &#8216;The Latest from Tinypint',  
&#8216;items' => 2,  
&#8216;show_summary' => 1,  
&#8216;show_author' => 0,  
&#8216;show_date' => 1  
));  
echo "</div>  
<pre>  
";  
}

[/sourcecode]

### Adding Your Company's Name to their Admin Panel

[sourcecode language=&#8221;php&#8221;]

add\_filter( &#8216;admin\_footer\_text', &#8216;tp\_admin\_footer\_text' );  
function tp\_admin\_footer\_text( $default\_text ) {  
return &#8216;<span id="footer-thankyou">Website managed by <a href="http://www.tinypintdesign.com">Tinypint Design & Consulting</a><span> | Powered by <a href="http://www.wordpress.org">WordPress</a>';  
}

[/sourcecode]