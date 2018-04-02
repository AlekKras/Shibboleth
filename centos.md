# Install via yum
## Step 1
<ul>
<li>CentOS 7 - http://download.opensuse.org/repositories/security://shibboleth/CentOS_7/security:shibboleth.repo</li>
<li>RHEL 7 - 	http://download.opensuse.org/repositories/security://shibboleth/CentOS_7/security:shibboleth.repo</li>
</ul>
## Step 2
sudo wget <repo file from link above> -O /etc/yum.repos.d/shibboleth.repo

## Step 3 (for 64-bit OS)
sudo yum -y install shibboleth.x86_64

## Step 4
sudo mkdir -p /var/log/shibboleth
sudo chown -R shibd:shibd /var/log/shibboleth
sudo touch /var/log/httpd/native.log
sudo /sbin/chkconfig --add shibd
sudo /sbin/chkconfig --levels 345 shibd on

## Step 5

sudo /sbin/service shibd start
sudo /sbin/service httpd restart
sudo grep CRIT /var/log/shibboleth/shibd.log

If you get something like ...No MetadataProvide available, then it's good

## Step 6 - Setting up SP

vim /etc/httpd/conf/httpd.conf

The UseCanonicalName directive should be set to On or resource mapping errors will result.
Ensure that the ServerName directive is properly set, and that Apache is being started with SSL enabled.

Edit /etc/httpd/conf.d/shibd.conf to enable Shibboleth for specfic Locations:

<code>
<Location /path/to/secured/content>
  AuthType shibboleth
  ShibRequestSetting applicationId https://www.yoursite.wisc.edu/shibboleth
  ShibRequestSetting requireSession 1
  require valid-user
</Location>
</code>

Highly recommend restarting httpd

P.S. you would need a metadata for correct configuration. SSL is highly recommended.

