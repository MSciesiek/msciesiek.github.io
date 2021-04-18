---
layout: post
title: "Access mariadb running on Lightsail via a ssh tunnel"
date: 2021-04-18 09:50:41 +0200
categories: aws mariadb
---
#### The problem

Accessing Mariadb database running in AWS cloud on a Lightsail instance.

#### The solution

SSH tunnelling (port forwarding) to the remote host. This will make the remote database appear on the local system as if it was run locally.

#### The implementation

Creating of a tunnel:
{% highlight bash %}
ssh -N -L 6604:localhost:3306 -i cert_file.pem system_username@123.123.123.123
{% endhighlight %}
This will make `localhost:3306` from a remote machine appear as port `6604` on a local one.\
Breakdown of the command:\
`-L` -- local port forwarding,\
`-N` -- not executing of a remote command.\
`-i cert_file.pem` -- the certificate to be used for connection\
`system_username` -- the username on a remote host that we log as\
`123.123.123.123` -- address of the remote host

The dababase should be now accessible locally (that is as long as the tunnel is open):
{% highlight bash %}
mariadb --host 127.0.0.1 -P 6604 --user db_username -p
{% endhighlight %}
or using phpmyadmin, dbeaver or other software.

#### Troubleshooting db connection:

When trying to connect to a database throught the tunnel from my local machine using db_user@localhost or db_user@127.0.0.1 I run into two errors (though not at the same time):\
`channel 2: open failed: administratively prohibited: open failed` (displayed in the console with ssh tunnel).\
and\
`Host '127.0.0.1' is not allowed to connect to this MySQL server` (displayed in the console where I tried to connect to db).
To solve this problem I started by looking at db users and their host. From remote host, logged in into a database as root, I executed:
{% highlight sql%}
SELECT user, host FROM mysql.user;
{% endhighlight%}
It turned out that the user that I wanted to use was only available on host `localhost`.

Creation of a dedicated user on host `127.0.0.1` and using it to make a connection solved the problem for me:
{% highlight sql %}
CREATE USER 'dedicated_user'@'127.0.0.1' IDENTIFIED BY 'password';
GRANT ALL ON db_name.* TO 'dedicated_user'@'127.0.0.1';
FLUSH PRIVILEGES;
{% endhighlight %}
