E-mail Configurations
=====================

Most of the applications need to send an e-mail now and then. WebLauncher Framework extend PHPMailer as the default mailer. (https://github.com/PHPMailer/PHPMailer)

Here are the configurations you can use to setup your e-mail delivery system::

	$this->mail_host='your_mail_server';		
	// yout mail server address if local use localhost or 127.0.0.1
	
	$this->mail_type='smtp'; 					
	// we recommend smtp (other: qmail, sendmail, mail, queue)
	
	$this->mail_user='noreply@yoursite.com';	
	// the smtp address user to use for e-mail sending
	
	$this->mail_password='smtp password';		
	// the smtp password
	
	$this->mail_ssl=false;						
	// true if the smtp connection is using SSL
	
	$this->mail_port=25;						
	// the smtp port to use	
			
	$this->mail_defaults = array(
		'subject' => 'Default e-mail subject',	// the default e-mail subject 
		'from' => 'from@yoursite.com',			// the default from e-mail address 
		'fromname' => 'Your Site Name',			// the default from name value 
		'reply_to' => 'noreply@heyduckee.com', 	// the default reply e-mail address
		'reply_name' => 'Your Site Reply Name',	// the default reply name value 
		'mail_in' => 'to',						// the default email method (to, cc, bcc)
		'others' => array('headers'=>array('X-SendFrom'=>'address')) // this can be used to set custom headers to the e-mails					
	);