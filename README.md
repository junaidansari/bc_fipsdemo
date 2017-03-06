# Demo App using Bouncy Castle FIPS Provider

This app aims at demonstrating the issue when using Bouncy Castle FIPS Provider started in FIPS unapproved mode and then changing the thread's FIPS mode to approved using org.bouncycastle.crypto.CryptoServicesRegistrar.setApprovedOnlyMode( true ) API.


A property file fips.properties in WEB-INF/lib has options for running the app in FIPS vs Non-FIPS mode.

Option to run the app using Bouncy Castle FIPS Provider. If set to true, adds the provider to the top of security provider list. 
fipsEnabled=true

Option to change the thread's FIPS Mode to approved.  
setFipsModeApproved=true 

Note: This app aims to demonstrate the issue when changing the thread's FIPS mode to approved.
