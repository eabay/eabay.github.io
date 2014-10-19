---
title: 'PHP: lcfirst'
date: 2009-07-01 10:00:00
categories:
  - PHP
tags:
  - PHP 5.3
---

I need to make the first character of the string lowercase. I know `ucfirst` exists and I supposed that there is a `[lcfirst](http://us2.php.net/manual/en/function.lcfirst.php)` one as well.

When I started to type `lcfirst`, Zend Studio didn't suggest me a function with this name and it was interesting. PHP documentation says that it is available but it throws an exception. What the hack goes wrong?

Here is the answer: It was too late and too hard to keep my eyes open :)

`lcfirst` function is available in [newly released version of PHP, 5.3](http://www.php.net/archive/2009.php#id2009-06-30-1). I am still using 5.2.9. Here is a code snippet:

```php
if (!function_exists('lcfirst')) {
    function lcfirst($string) {
        return substr_replace($string, strtolower(substr($string, 0, 1)), 0, 1);
    }
}
```

It is unbelivable that I don't ever need the function lcfirst before. :)
