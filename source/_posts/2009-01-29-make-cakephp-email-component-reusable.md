---
title: Make CakePHP Email Component Reusable
date: 2009-01-29 10:00:00
categories:
  - CakePHP
  - PHP
tags:
  - components
  - extending cakephp component
---

I know the title of this post a little bit confusing but let me explain what I want to tell.

You are using [CakePHP](http://cakephp.org)'s email component and you should set the same information in each time before you send your email like server address, username, password etc.

Just create a new file mailer.php with the following content and drop it into your CakePHP application components folder (I like convention over configuration! ;).

```php
<?php
App::import('Component', 'Email');

class MailerComponent extends EmailComponent
{
  var $from     = 'ME <me@localhost>';
  var $replyTo  = 'noreply@localhost';
  var $sendAs   = 'both';
  var $delivery = 'smtp';
  var $xMailer  = 'Postman';
  var $smtpOptions = array(
    'port'     => 25, 
    'host'     => 'serveradress', 
    'timeout'  => 30, 
    'username' => 'username', 
    'password' => 'password'
  );
}
```

And right now you have a new component with the name `Mailer` and its server configuration is predefined. You can reuse it without being affected by any kind of mail server change.

You can define a new function inside your controller (`_sendEmail()` in our case) and make the email sending process more painless.


```php
class AnyController extends AppController
{
  function contact()
  {
    if ($this->_sendEmail('Name', 'blabla@fakeemail', 'Grate site!')) {
      $this->Session->setFlash(__("Thank you", true));
    } else {
      $this->Session->setFlash('Damn it!');
    }
  }

  function _sendEmail($name, $email, $message)
  {
    $this->Mailer->to = 'info@localhost';
    $this->Mailer->subject = __("Site Contact", true);
    $this->Mailer->template = 'contact';
    
    $this->set('name', $name);
    $this->set('email', $email);
    $this->set('message', $message);
    $this->Mailer->send();
    
    $this->log( $this->Mailer->subject . ' -> Name:'. $name .' | E-posta: '. $email .' | Message: '. $message .' | smtp error: '. serialize($this->Mailer->smtpError) );
		
    return $this->Mailer->smtpError ? false : true;
  }
}
```

That's all! Check [Bakery](http://bakery.cakephp.org/) for other cakes :)
