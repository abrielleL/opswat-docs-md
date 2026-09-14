<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/miscellaneous-settings -->

# Miscellaneous Settings

Certain miscellaneous settings can be configured in the file gears-onpremise_definition.properties, located at:

- On Windows systems: <System Drive>\ProgramData\OPSWAT\Central\gears-onpremise_definition.properties
- On RedHat and Ubuntu systems: /etc/opt/ocm/gears-onpremise_definition.properties

#DB address, should not be modified
HOST=127.0.0.1
 
#Redis address, should not be modified
redis.host.primary = 127.0.0.1:9005
 
#Scheduler interval setting for MetaDefender Core dashboard (milliseconds)
schedule.core.statistic.interval=60000
schedule.core.scanQueue.interval=60000
schedule.core.processing.history.interval=3600000
#Enable/disable processing history collection scheduled job
schedule.core.processing.history.enable=true
 
# Product timeout setting milliseconds
core.read.timeout = 10000
core.connect.timeout = 3000
engine.upload.read.timeout = 15000
engine.upload.connect.timeout = 15000
kiosk.read.timeout = 10000
kiosk.connect.timeout = 3000
icap.read.timeout = 10000
icap.connect.timeout = 3000
email.read.timeout = 10000
email.connect.timeout = 3000
vault.read.timeout = 10000
vault.connect.timeout = 3000
secure_storage.read.timeout = 10000
secure_storage.connect.timeout = 3000
#Set to true to disable server certificate verification for SMTP mail server
MAIL_SSL_CERT_VERIFICATION_DISABLE=false
#how long the system should keep an old version of a module (in days)
clean.engines.afterDays = 7

Some settings are hidden by default and may not be present in the actual gears-onpremise_definition.properties file. To modify these settings, manually add them to the file with the desired values.

OPSWAT Central Management will need to be restarted for these modifications to take effect.
