# Automic_Test
Acme-it_Test

# deploy.sh
# The deployment file
# Copyright (c) 2012, Comfirm AB

# Add files to be copied.
# file  group   file
# ------------------------------------------
file all 	/usr/local/app/script.sh
file all 	/usr/local/app/program
file all 	/usr/local/app/program.config
file all 	/usr/local/app/README
file all 	/etc/config-file
file all 	/etc/another-config-file
file db 	/etc/db-config
file web 	/var/www/index.html
file web 	/etc/web.config

# Begin script
# Runs before everything
# Available environment variables:
# $DEPLOY_GROUP:	all, db, etc...
BEGIN:
# Add commands here to run before the deployment
# ------------------------------------------
if [ -d '/usr/local/app/' ]; then
        echo 'App folder exists...'
else
        echo 'Creating app folder...'
        sudo mkdir /usr/local/app
fi
# ------------------------------------------
exit

# Finishing script
# Runs after everything
# Available environment variables:
# $DEPLOY_GROUP:	all, db, etc...
FINISH:
# Add commands here to finish the deployment
# ------------------------------------------
echo $DEPLOY_GROUP
sudo chmod 755 /usr/local/app/*
sudo chown root:root /usr/local/app/*

# Add to crontabs
if [ -d "/var/lib/redis/" ]; then
	echo "Updating crontab for redis..."
        sudo crontab -u redis -l | grep -v script.sh > /tmp/crontab
        sudo echo "*/5 * * * * /bin/bash /usr/local/app/script.sh" >> /tmp/crontab
        sudo crontab -u redis /tmp/crontab
else
	echo "Updating crontab for root..."
        sudo crontab -u root -l | grep -v script.sh > /tmp/crontab
        sudo echo "*/5 * * * * /bin/bash /usr/local/app/script.sh" >> /tmp/crontab
        sudo crontab -u root /tmp/crontab

fi
sudo rm /tmp/crontab
# -----------------------------------------
exit

# Update script
# Runs when call --update
# Available environment variables:
# $DEPLOY_GROUP:	all, db, etc...
UPDATE:
# Add commands here to do the update
# ------------------------------------------
echo "I'm update!"
echo "Server group: ${DEPLOY_GROUP}"
if [ "$DEPLOY_GROUP" = "all" ]; then
	sudo chmod 700 /usr/local/app/*
	sudo chown redis:redis /usr/local/app/*
fi
# ------------------------------------------
exit

