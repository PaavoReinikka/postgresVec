### Scipts for populating the database

Possible scripts for populating database w/o migrations -- "../data/" can be bound and made available for both *data-preparation* and *database* service. This way the backend server is not needlessly burdened with dataloading on launch. This service is primarily meant for individual loads, and not to run continuously and concurrently with the database -- if there is need for cron jobs, they should primarily be run on the main backend or in a dedicated cron service. However, this is not set in stone:
 **Make the appropriate modifications to compose file if you use this as a cron service.**

The service can be run using profile `data-preparation` (depends on database and migrations).

**If dangling/orphan containers cause problems:** You can remove them by adding the `--remove-orphans` flag for compose. If you want to populate the database with your own scripts, you should start by tearing down (with the above flag), and then re-build. You can use a profile, or target the service with `-d data-preparation` argument for compose up.
