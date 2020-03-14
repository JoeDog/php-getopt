Getopts for php command line scripts. To use these classes,  
you'll probably probably want the php commandline utility:

  $ sudo apt-get install php-cli
  $ sudo yum install php-cli  

This is a PHP port of GNU getopt based on the 1998 Java port by  
by Aaron M. Renn. I attempted to keep my implementation as close  
to his as possible. To install the code, place the 'gnu' directory  
inside your include path. In order to see you path, run this on  
the command line:  
 
 $ php -r "echo ini_get('include_path');"  

My result was '/usr/share/pear:/usr/share/php:.' Once I copied  
'gnu' and all its contents to /usr/share/php it was available for  
all my applications. You could also place at the same directory  
level as your program.  

Here's a quick example that uses both long and short options:  

#!/usr/bin/php  
<?php  
  require_once("gnu/getopt/Getopt.php");  
  require_once("gnu/getopt/Longopt.php");  

  $longopt = array();  
  $longopt[0] = new LongOpt("help",  NO_ARGUMENT,       null, 'h');  
  $longopt[1] = new LongOpt("about", REQUIRED_ARGUMENT, null, 'a');  
  $getopt     = new Getopt($argv, "a:bc:d:hW;", $longopt);  
  $c;  
  $arg;  
  while (($c = $getopt->getopts()) != -1) {  
    switch($c) {  
    case 'a':  
    case 'd':  
      $arg = $getopt->getOptarg();  
      print("You picked $c with an argument of ".(($arg != null) ? $arg : "null")."\n");  
      break;  
    case 'b':  
    case 'c':  
      $arg = $getopt->getOptarg();  
      print("You picked $c with an argument of ".(($arg != null) ? $arg : "null") . "\n");  
      break;  
    case 'h':  
      print "Usage: test [options] \n";  
      break;  
    case '?':  
      break; // getopt() already printed an error  
    default:  
      print("getopt() returned $c\n");  
    }  
  }  
?>   

Happy hacking!  
Jeff Fulmer <jeff@joedog.org>  
