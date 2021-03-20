---
title: Using with Nextcloud/Owncloud
group: Usage
---

Photoview can be configured to grab media from [Nextcloud](https://nextcloud.com/).

## Locating Nextcloud/Owncloud files on the filesystem

All files uploaded to Nextcloud/Owncloud are located in the folder called `data/` at the location where Nextcloud/Owncloud is installed.
Inside that folder you will find another folder for each Nextcloud/Owncloud user.
All files uploaded by a user is located inside their respective folders.

Now find the path to where your Nextcloud/Owncloud media is located, and copy it as we will need it later.
The path could look somthing like this:

    ~/nextcloud/data/example_user/files/Photos

## Configure Photoview

The next step will be to add this path to the desired Photoview user.

### Adding path as a Docker volume

> If you are not running Photoview in Docker you can skip this step.

Before the Nextcloud or Owncloud files can be accessed by the Photoview container,
they must first be mounted as a [volume](https://docs.docker.com/storage/volumes/).

For docker-compose this can be done by adding the volume to the `docker-compose.yml` configuration file for Photoview.
Open it up and under `volumes:` add a new volume like so:

    - NEXTCLOUD_PATH:/nextcloud:ro

Replace `NEXTCLOUD_PATH` with the path you copied in step 1.
The `/nextcloud` path dictates where this mount can be accessed from within the container, this will be important for the next step.
The `:ro` in the end, instructs Docker to mount the folder in read-only mode.

Now restart the docker container.

## Add path to Photoview user

You can now add the new path the desired user from the Settings page,
by clicking on the `Edit` button next to the user.
From there you can add the new path.

If you mounted the volume like in the previous step, the path will be `/nextcloud`.
When the path has been added, you can click `Save`.
You can now scan the user and the pictures and videos from nextcloud will appear in Photoview.

## Keep Photoview updated automatically

If you don't want to press the `Scan` button manually each time you've added new files to Nextcloud/Owncloud, you can [configure a periodic scanner](/docs/usage-settings/#periodic-scanner) to automatically scan for changes.
