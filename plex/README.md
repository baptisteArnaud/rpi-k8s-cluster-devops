# Plex Chart

| Parameter                  | Description                         | Default                                                 |
|----------------------------|-------------------------------------|---------------------------------------------------------|
| `hostname`         | Reverse proxy Hostname | `plex.example.com` |
| `nodeLabel`         | Label corresponding to the node you want to deploy your service in (the one where your disk drive is plugged). See below how to add a label to a specific node. | `disktype: hdd` |
| `volumes.configDir`      | The host directory for config files | "/path/to/config/dir" |
| `volumes.dataDir`      | The host directory where you want your media files to be stored. | "/path/to/data/dir" |
| `volumes.transcodeDir`      | The host directory where to store transcoder | "/path/to/transcode/dir" |