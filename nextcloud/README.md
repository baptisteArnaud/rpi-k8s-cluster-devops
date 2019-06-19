# Nextcloud Chart

| Parameter                  | Description                         | Default                                                 |
|----------------------------|-------------------------------------|---------------------------------------------------------|
| `hostname`         | Reverse proxy Hostname | `cloud.example.com` |
| `persistData`      | If you want the data to be persisted. Ortherwise, Nextcloud has not much interest | true |
| `nodeLabel`         | Label corresponding to the node you want to deploy your service in (the one where your disk drive is plugged). See below how to add a label to a specific node. | `disktype: hdd` |
| `volumes.configDir`      | The host directory for config files | "/path/to/config/dir" |
| `volumes.dataDir`      | The host directory where you want your data to be stored. | "/path/to/data/dir" |
| `volumes.appsDir`      | The host directory where to store installed apps | "/path/to/apps/dir" |
| `volumes.themesDir`      | The host directory where to store installed themes | "/path/to/themes/dir" |
| `volumes.databaseDir`      | The host directory where to store mysql database | "/path/to/database/dir" |
| `mariaDb.rootPassword`      | MariaDB root password. It isn't really important | "mariadbrootpasswd" |
| `mariaDb.username`      | MariaDB username | "mariadbusername" |
| `mariaDb.password`      | MariaDB password | "mariadbpasswd" |
| `mariaDb.database`      | MariaDB db name | "databasename" |