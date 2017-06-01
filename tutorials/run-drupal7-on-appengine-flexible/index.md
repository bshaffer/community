---
title: Run Drupal on Google App Engine Flexible Environment
description: Learn how to deploy a Drupal app to Google App Engine flexible environment.
author: bshaffer
tags: App Engine, Drupal, PHP
date_published: 2017-03-15
---
## Drupal

> [Drupal 7][drupal] the friendly and powerful content management platform for
> building nearly any kind of website: from blogs and micro-sites to
> collaborative social communities.
>
> – drupal.org

You can check out [PHP on Google Cloud Platform][php-gcp] to get an
overview of PHP itself and learn ways to run PHP apps on Google Cloud
Platform.

## Prerequisites

1. [Create a project][create-project] in the Google Cloud Platform Console
   and make note of your project ID.
1. [Enable billing][enable-billing] for your project.
1. Install the [Google Cloud SDK](https://cloud.google.com/sdk/).
1. Create a [Google Cloud SQL instance][3]. You will use this as your Drupal
   MySQL backend.

## Prepare

Follow the installation instructions to install [Drush CLI][drush].

The recommended way is to install via composer in the directory of your future
Drupal project.

    composer require drush/drush

Drush will then be executable from `vendor/bin/drush` in that
directory.

## Install

    1. Once Drush is installed, you can download Drupal 7:

        /path/to/drush dl drupal-7.x

    1. You can also try setting up your Drupal 7 instance using [Drush][4]
    ```sh
    /path/to/drush site-install \
        --locale=en \
        --db-path=mysql://YOUR_DB_USER@YOUR_DB_PASS:YOUR_DB_HOST/YOUR_DB_NAME \
        --site-name='My Drupal Site On Google' \
        --site-mail=you@example.com \
        --account-name admin \
        --account-mail you@example.com \
        --account-pass admin
    ```

    Be sure to replace `YOUR_DB_USER`, `YOUR_DB_PASS`, `YOUR_DB_HOST`, and
    `YOUR_DB_NAME` with the values you received when creating your CloudSQL
    instance.

## Deploy

1. Create an `app.yaml` file with the following contents:

        runtime: php
        env: flex
1. Run the following command to deploy your app:

        gcloud app deploy

1. Visit `http://YOUR_PROJECT_ID.appspot.com` to see the Drupal welcome page!

    ![Drupal welcome page][drupal-welcome]

[create-project]: https://cloud.google.com/resource-manager/docs/creating-managing-projects
[enable-billing]: https://support.google.com/cloud/answer/6293499?hl=en
[php-gcp]: https://cloud.google.com/php
[drupal]: https://www.drupal.org/about/drupal-7
[drupal-install]: http://drupal.com/doc/current/setup.html
[drupal-welcome]: http://drupal.com/doc/current/_images/welcome.png
[drush]: http://docs.drush.org/en/master/install/#install-a-site-local-drush
