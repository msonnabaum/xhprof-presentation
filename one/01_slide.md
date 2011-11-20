!SLIDE image title
# Profiling Drupal with XHProf
## (or, Identifying the Suck)
Presented by: Mark Sonnabaum

!SLIDE bullets
# whoami

## Mark Sonnabaum
- Performance engineer @ Acquia
- d.o. [msonnabaum](http://drupal.org/user/75278)
- twitter [@msonnabaum](http://twitter.com/msonnabaum)
- Not usually [moustached (http://mobro.co/msonnabaum)](http://mobro.co/msonnabaum)




!SLIDE bullets
# Profiling
- It's awesome
- You should do it

!SLIDE bullets
# What is XHProf?
- A php profiler (php extension)
- A PHP user interface (optional)
- Originally developed at Facebook

[https://github.com/facebook/xhprof](https://github.com/facebook/xhprof)
[http://pecl.php.net/package/xhprof](http://pecl.php.net/package/xhprof)

!SLIDE bullets
# xdebug/webgrind?
- No memory profiling as of Xdebug 2.0.4
- Adds overhead

!SLIDE bullets incremental
# Common code issues
- Unnecessary repitition (static caches, persistent caches)
- Stuff that is dumb (make less dumb)

!SLIDE bullets
# Installing: pecl (?)
    pecl install xhprof-0.9.2

!SLIDE bullets
# Installing: Ubuntu

[https://launchpad.net/~brianmercer/+archive/php5-xhprof](https://launchpad.net/~brianmercer/+archive/php5-xhprof)
!SLIDE bullets
# Installing: OSX - MAMP
## php 5.3 (simple)
[https://gist.github.com/1306569](https://gist.github.com/1306569)

## php 5.2 (painful)
[http://www.lullabot.com/articles/installing-xhprof-mamp-on-mac-os-106-snow-leopard](http://www.lullabot.com/articles/installing-xhprof-mamp-on-mac-os-106-snow-leopard)

!SLIDE bullets
# Installing: OSX - brew

[https://github.com/msonnabaum/megalodon/blob/master/formulas/xhprof.rb]( https://github.com/msonnabaum/megalodon/blob/master/formulas/xhprof.rb)
    brew install xhprof

!SLIDE bullets
# Installing: source

    wget http://pecl.php.net/get/xhprof-0.9.2.tgz
    tar -xzf xhprof-0.9.2.tgz && cd xhprof-0.9.2
    phpize
    make
    cp modules/xhprof.so $(php-config --extension-dir)/

!SLIDE bullets
# Preperations

- Setup the site locally
- disable xdebug
   <pre><code> ;zend_extension=/usr/lib/php/extensions/no-debug-non-zts-20090626/xdebug.so</code></pre>
- D6: [devel](http://drupal.org/project/devel), D7: [xhprof module](http://drupal.org/project/xhprof)
- [memcache](http://drupal.org/project/memcache) (optional)

!SLIDE bullets
# Preperations
## D6

    @@@ Php
    $conf['devel_xhprof_enabled'] = 1;
    $conf['devel_xhprof_directory'] = '/Users/msonnabaum/www/xhprof';
    $conf['devel_xhprof_url'] = 'http://localhost/xhprof/xhprof_html';

## D7

    @@@ Php
    $conf['xhprof_enabled'] = 1;

!SLIDE subsection
# PROFILIN' TIME

.notes http://xhprof-pres.dev/events - unpack_options

.notes native drupal xhprof ui
.notes - http://d7.dev/admin/reports/xhprof
.notes - http://d7.dev/admin/reports/xhprof/diff/4e99c0c276515/4e99c0bf949a8

.notes XHProflib - https://github.com/msonnabaum/XHProfLib
