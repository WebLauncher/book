Templates Configurations
========================

There are some configurations that apply to the template engine or the template content and resources. WebLauncher Framework uses `Smarty Template Engine <http://www.smarty.net/>`_ by default. 
There is also a built-in PHP simple template engine.

To change the default template engine use::
	
	$page->template_engine='php'; // to change to simple PHP template engine

To import a global css file into the template use::

	$page->add_css_file('/assets/style.css'); // you can use Smarty predefined variables into the link provided {$root_styles} points to /assets/styles

To import a global javascript file into the template use::
	
	$page->add_js_file('/assets/jquery/jquery.js'); // you can use Smarty predefined variables into the link provided {$root_scripts} points to /assets/scripts
	
Go here to find out more about the :doc:`predefined templated variables </views/predefined-template-variables>`.	