# RNDCKeyGeneration
RNDC manual key generation if you by mistake delete the auto-generated. 

rndc reload
# Reload the configuration.This command results in error because there is no key file or configuration.

systemctl stop named
# stop the named service.

rndc-confgen -r /dev/urandom > /etc/rndc.conf
# creates a key file and the configuration file for the key.

cat /etc/rndc.conf
# copy the section regarding using the key in the named.conf file and paste into /etc/named.conf,before the Include statement, and uncomment the section. 

chgrp named /etc/rndc.conf
# change the group of the file to named.

chmod 640 /etc/rndc.conf 
# change the permissions to remove read access from Other.

systemctl start named
# start named service.

rndc reload
# you will get an error stating there is a configuration file and a key, so the default is to use the configuration file.To remove this message,simply remove the rndc.key file and reload the configuration. - rm /etc/rndc.key then rndc reload.

nslookup www.google.com or you can use dig www.google.com
# To test the RNDC key manual generation is successful or not.
