Templates Configurations
========================

There are some configurations that apply to the template engine or the template content and resources. WebLauncher Framework uses `Smarty Template Engine <http://www.smarty.net/>`_ by default. It also provides extensions to the Smarty Template engine.
There is also a built-in PHP simple template engine. However this does not provide extensions available in the Smarty Template Engine.

To change the default template engine use::
	
	$this->template_engine='php';
	// to change to simple PHP template engine

To import a global css file into the template use::

	$this->addCssFile('/assets/style.css');
	// you can use Smarty predefined variables into the link provided {$root_styles} points to /assets/styles

To import a global javascript file into the template use::
	
	$this->addJsFile('/assets/jquery/jquery.js');
	// you can use Smarty predefined variables into the link provided {$root_scripts} points to /assets/scripts
	
Go here to find out more about the :doc:`predefined templated variables </views/predefined-template-variables>`.	