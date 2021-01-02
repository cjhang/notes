# Full Stack Website Development

## HTML

Show the newline from the text with '\n'

```html
white-space: pre;
```



## CSS



## Server

### Host flask on apache2

Requisites:

1. apache2
2. mod_wsgi (for python3)
3. flask

For Debian:

```shell
sudo apt update
sudo apt install apache2 libapache2-mod-wsgi-py3 python3-dev
```

The flask then installed through though the pip

```shell
pip install flask
```

Three files for the Flask app:

1.  Empty `__init__.py`

2. Flask application file `flask_app.py`

   ```python
   from flask import Flask
   app = Flask(__name__)
   @app.route("/")
   def hello():
       return "Hello world!"
   if __name__ == "__main__":
       app.run()
   ```

3. The wsgi file `flask_app.wsgi`, with the shebang line

   ```shell
   #! /usr/bin/python3.6
   
   import logging
   import sys
   logging.basicConfig(stream=sys.stderr)
   sys.path.insert(0, '/home/username/ExampleFlask/')
   from my_flask_app import app as application
   application.secret_key = 'anything you wish'
   ```

   



Apache2 config file for flask, when you using other port, make sure it is listen by apache2 in configure '/etc/apache2/port.conf'

```xml
<VirtualHost *:80>
     # Add machine's IP address (use ifconfig command)
     ServerName 192.168.1.103
     # Give an alias to to start your website url with
     WSGIScriptAlias /testFlask /home/username/ExampleFlask/my_flask_app.wsgi
     <Directory /home/username/ExampleFlask/ExampleFlask/>
     		# set permissions as per apache2.conf file
            Options FollowSymLinks
            AllowOverride None
            Require all granted
     </Directory>
     ErrorLog ${APACHE_LOG_DIR}/error.log
     LogLevel warn
     CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

 

Enable the flask configuration and restart apache2

```shell
a2ensite /etc/apache2/sites-available/Flask.conf
systemctl restart apache2.service
systemctl status apache2.service
```



### Webdav

Install the requisite softwares:

```shell
apt install apache2
sudo a2enmod dav
sudo a2enmod dav_fs
```



