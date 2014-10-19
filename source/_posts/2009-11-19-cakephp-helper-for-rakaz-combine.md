---
title: CakePHP Helper for rakaz Combine
categories:
  - CakePHP
  - Javascript
  - PHP
tags:
  - cakephp helper
  - combine
  - compress
  - CSS
  - helpers
---

Combine is still my favorite javascript/css combine and compress script.

I [posted][1] a solution how to use it in a CakePHP application and here is a little helper to make it more useful:

```php app/views/helpers/combine.php
<?php
class CombineHelper extends AppHelper
{
	public $helpers = array('Html', 'Javascript');
	
	private $_pattern = '../combine.php?type=:type&files=:files';
	
	public function js($files)
	{
		echo $this->Javascript->link($this->_format($files));
	}
	
	public function css($files)
	{
		echo $this->Html->css($this->_format($files, 'css'));
	}
	
	private function _format($files = array(), $type = 'javascript')
	{
		return String::insert($this->_pattern, array('type' => $type, 'files' => implode(',', $files)));
	}
}
```

Add it to controller's helpers property:

```php
<?php
class MyController extends AppController
{
	public $helpers = array('Combine');
```

And call it by passing an array of file names in your view:

```php
$combine->js(array(
    'javascript1.js',
    'javascript2.js',
    'javascript3.js'
));

$combine->css(array(
    'stylesheet1.css',
    'stylesheet2.css',
    'stylesheet3.css'
));
```

### Don't forget to add file extensions!
If you want to add only one file, you don't have to use combine helper. Directives added to `.htaccess` file let combine script to compress the file([See related post][1]). Just use `$javascript->link('filename')`.

 [1]: {% post_url 2009-01-29-using-rakaz-combine-with-your-cakephp-application %}
