# Shibboleth
Information to get to know shibboleth system better

<h4>Installation Process</h4>
<ul>
<li>curl -o /etc/yum.repos.d/security:shibboleth.repo http://download.opensuse.org/repositories/security://shibboleth/CentOS_7/security:shibboleth.repo </li>
  <li>yum install shibboleth</li>
  <li>rpm -qa | grep shibboleth  <i>(This will ensure that you got the right version of Shibboleth installed)</i></li> 
  <li>The runtime Shibboleth directory will now exist at <code>/etc/shibboleth</code></li>
  <li><code>systemctl status ntpd</code> (if inactive, run <code>systemctl start ntpd</code>)</li>
  <li>If Apache httpd is not installed, install it (and the SSL module) via yum:
    <code>yum install httpd mod_ssl</code>
</li>
  <li> Go to <code>/etc/httpd/conf/httpd.conf</code> and add <code>UseCanonicalName On
    ServerName web.server:80</code></li>
  <li>Check if <code>/etc/httpd/conf.d/ssl.conf</code> exists. If not, run <code>yum install mod_ssl</code></li>
  <li>Let's make SP alive, run <code>systemctl start shibd</code> and <code>systemctl start httpd</code></li>
  <li>Try accessing it on <code>web.server/Shibboleth.sso/Status</code></li>
</ul>
