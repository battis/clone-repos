# clone-repos

The accompanying `Dockerfile` builds a simple image that can be used to package `greg` to run in a virtualized container (useful on, say, a Synology NAS). This image is also maintained at [sbattis/clone-repos](https://hub.docker.com/repository/docker/sbattis/clone-repos).

## Synology Setup

1. Create 2 directories to store `clone-repos` files: `config`, `repos`
2. Acquire a GitHub personal access token and store it in `config/token.txt`
3. Store a password-less SSH key with access to your GitHub account in `config/id_rsa`
4. Install Docker (if not already installed) in the Package center
5. In Docker, search the registry for `sbattis/clone-repos` and download
6. Select the `sbattis/clone-repos:latest` image that has been downloaded and click Launch
7. Give the container a reasonable name (e.g. `clone-repos`) and click Advanced Settings
8. Add 2 volumes, to map to your `config` and `repos` directories as mount paths `/config` and `/repos` respectively and click Apply
9. Click Next
10. **Uncheck** the option to run the container after the wizard is finished and click Done
11. In the Task Scheduler control panel, create a new scheduled task that is a user-defined script.
12. Set the user to `root` and give the task a reasonable name (e.g. `Clone GitHub Repos`)
13. Set the schedule (e.g. 11:59pm every day)
14. Under Task Settings, configure any desired email notifications and set the script to `dock start clone-repos` (assuming that's what you named your container) and click OK
15. Accept the scary warning about modifying system configurations etc. (it's about running as the root user)
16. If you want, give the task a trial Run

Log files can be viewed by opening the container in Docker.

## Future improvements

- A (smaller) Synology-specific image
- Easier configuration
- Better err-handling

When will this happen? Who knows.
