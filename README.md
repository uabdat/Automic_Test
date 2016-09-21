# Automic_Test
Acme-it_Test

<?xml version="1.0" encoding="UTF-8"?>
<projectDescription>
	<name>com.microsoftopentechnologies.acsfilter.feature</name>
	<comment></comment>
	<projects>
	</projects>
	<buildSpec>
		<buildCommand>
			<name>org.eclipse.pde.FeatureBuilder</name>
			<arguments>
			# The server list.
# deploy.sh
# Copyright (c) 2012, Comfirm AB
# 
# To get the most out of deploy.sh you can make it dynamic.
# Use a heartbeat software or similar to maintain it.

# Define the user to login with: <Username>
# user  name    keyfile
# ------------------------------------------
user    ubuntu  /var/keyfiles/ubuntu.rsa

# Add server groups like this:
# server        group   ip address
# ------------------------------------------
server  all     10.0.0.101
server  all     10.0.0.102
#server all     10.0.0.104
server  all     10.0.0.105
server  all     10.0.0.106
server  all     10.0.0.108
server  all     10.0.0.109
server  all     10.0.0.120
server  all     10.0.0.150

# DB servers
server  db      10.0.0.106
server  db      10.0.0.150

# Web servers
server  web     10.0.0.105
server  web     10.0.0.120

#Contact GitHub API Training Shop Blog About
			</arguments>
		</buildCommand>
	</buildSpec>
	<natures>
		<nature>org.eclipse.pde.FeatureNature</nature>
	</natures>
</projectDescription>
