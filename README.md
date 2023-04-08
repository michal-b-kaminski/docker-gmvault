# docker-gmvault

Docker image wrapping [Gmvault](http://gmvault.org/) Gmail backup solution. Allows periodic running of quick and full sync jobs. Requires creating of Google Project and obtaining OAuth token through browser.

## Parameters

Supported environment parameters:
- `GMVAULT_DIR`: (default `/data`) directory mounted inside Docker container for storing Gmvault data
- `GMVAULT_EMAIL_ADDRESS`: (default: `test@example.com`) e-mail account to backup
- `GMVAULT_FULL_SYNC_SCHEDULE`: (default: `1 3 * * 0`) cron schedule for full backups
- `GMVAULT_QUICK_SYNC_SCHEDULE`: (default: `1 2 * * 1-6`) cron schedule for quick backups
- `GMVAULT_DEFAULT_GID`: (default: `9000`) GID for backups
- `GMVAULT_DEFAULT_UID`: (default: `9000`) UID for backups
- `GMVAULT_SYNC_ON_STARTUP`: (default: `no`) should backup be run on container startup
- `GMVAULT_SEND_REPORTS_TO`: (default: `$GMVAULT_EMAIL_ADDRESS`) address to send backup reports to 
- `GMVAULT_OPTIONS`: additional Gmvault options
- `GMVAULT_TIMEZONE`: (default: `America/Los_Angeles`) timezone to use

## Authentication 

OAuth token must be set up before periodic backups can be started. To do so, container must be started and terminal attached. Then run:
`su -c 'gmvault sync -d /data $GMVAULT_EMAIL_ADDRESS' gmvault`
And follow instructions displayed. After synchronization starts, restart the container.

Some links with info about possible problems with Oauth auth:
1. http://gmvault.org/in_depth.html#authentication
2. https://wolfnotes.doulos.at/backing-up-gmail-with-gmvault/
3. https://github.com/gaubert/gmvault/issues/361
