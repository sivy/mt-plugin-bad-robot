# BadRobot plugin for Melody and Movable Type 4.x #

## Overview ##

For site owners who need to be able to selectively allow or prevent access by web crawlers to their
Movable Type and Melody blogs.

### <a id="prerequisites">Prerequisites</a>

BadRobot depends on [Config Assistant](https://github.com/openmelody/mt-plugin-configassistant), available 
from the OpenMelody Github repository.

## <a id="installation">Installation</a> ##

The latest version of the plugin can be downloaded from its [Github
repo](https://github.com/sivy/mt-plugin-badrobot).

Installation follows the [standard plugin installation](http://tinyurl.com/easy-plugin-install) procedures.

## <a id="usage">Usage</a>

* Install the plugin
* In the blog you want to setup the feed for, go to "Tools > Plugins" and open the settings for "BadRobot".

![BadRobot Setup in the Plugin settings](https://img.skitch.com/20110525-b8w4f9fqsqfi26jgb9ias2qec1.png)

* The UserAgent defaults to '*' for all web crawlers. If you want to only disallow a particular bot, enter the exclusion user agent here (for Google, that's 'googlebot'). You can find more information on how to specifify web crawler user-agents on <a href="robotstxt.org">robotstxt.org</a>.
* To block all access to the blog, select 'Disallow' from the radio buttons marked 'Allow Robots?'. No value here will leave this blog out of the robots.txt file and will default to allowing crawler access to your content.
* Save your settings

## Template Setup

* If you don't already have a `robots.txt` template, create a new index template:
    * name: Robots.txt
    * outfile: robots.txt
    * template type: Custom Index Template
    * publish: Static (default)

![create your robots.txt template](https://img.skitch.com/20110525-d1am3y4p9jjn3b7bki5aimgs1y.png)

## Using The Tags

BadRobot defines two blog-level settings that are exposed via the tags `<mt:RobotsUserAgent>` and `<mt:RobotsAllow>`. In your robots.text template, add the following code:

    <mt:blogs><mt:if tag="RobotsAllow">
    # generated by the BadRobot plugin
    # for the '<mt:blogname>' blog
    User-agent: <mt:RobotsUserAgent>
    <mt:RobotsAllow>: <mt:BlogRelativeURL>
    </mt:if></mt:blogs>

This will output a file like this:

    # generated by the BadRobot plugin
    # for the 'My Public Blog' blog
    User-agent: *
    Allow: /
    
    # generated by the BadRobot plugin
    # for the 'My private blog' blog
    User-agent: googlebot
    Disallow: /private_blog/

    