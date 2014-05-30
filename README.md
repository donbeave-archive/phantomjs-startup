PhantomJS startup script (NEED Selenium Grid)
======================================================

This is a simple startup script based on the selenium startup script.

This startup script assumes you have selenium server 2.x installed with startup script from feniix (https://github.com/feniix/selenium-grid-startup).
also assumes you have the pkg `daemon` installed and a java runtime installed (this was tested in ubuntu 10.04.4 with `openjdk-6-jdk`)

Install PhantomJS:

	sudo add-apt-repository ppa:pcarrier/ppa
	sudo apt-get update
	sudo apt-get phantomjs

and the following already created in your linux box:

id: phantomjs

home: /var/lib/phantomjs

shell: /bin/bash

phantomjs installation directory: /var/lib/phantomjs

    sudo groupadd -r phantomjs
    sudo useradd -r -d /var/lib/phantomjs -s /bin/bash -m -g phantomjs -G phantomjs phantomjs


log dir: /var/log/phantomjs owned by the phantomjs id

    sudo mkdir /var/log/phantomjs
    sudo chown phantomjs.phantomjs /var/log/phantomjs
    

Copy the default file and the init.d file in the right locations:

    sudo cp /local/repo/path/etc/init.d/phantomjs /etc/init.d/
    sudo cp /local/repo/path/etc/default/phantomjs /etc/default/
    
Make sure the init.d script is executable:

    sudo chmod +x /etc/init.d/phantomjs   

Install the service startup:

    sudo update-rc.d phantomjs defaults
   
Change the Selenium Grid port to 5555.

	nano -w /etc/default/selenium

Find and change the the line to:

	# SELENIUM_PORT=5555
	SELENIUM_PORT=4444

Start the selenium:

    sudo /etc/init.d/selenium start

Start the phantomjs:

    sudo /etc/init.d/phantomjs start
    

Check the logs:

    sudo tail -f /var/log/phantomjs/phantomjs.log
    

The service configuration can be found in `/etc/default/phantomjs`

Copyright and license
---------------------

Copyright 2013-2014 Alexey Zhokhov under the [Apache License, Version 2.0](LICENSE). Supported by [Polusharie][polusharie].

[polusharie]: http://www.polusharie.com
