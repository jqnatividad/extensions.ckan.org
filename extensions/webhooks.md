---
layout: extension
name: webhooks
title: Webhooks for CKAN
author: Denis Zgonjanin
homepage: https://github.com/deniszgonjanin/ckanext-webhooks
github_user: deniszgonjanin
github_repo: ckanext-webhooks
category: Extension
featured: 
permalink: /extension/webhooks/
---


ckanext-webhooks
================

Webhooks for your CKAN. For example, as an app developer you want to be notified when a dataset your app depends on is updated. This extension allows users and services to register to be notified for common CKAN events, such as:

-   Dataset Events - new, update, delete
-   Resource Events - new, update, delete

Subscribers provide a callback url when registering for an event, and CKAN will call that url when the desired event happens.

Installation
------------

Add webhooks to your CKAN plugins:

``` sourceCode
ckan.plugins = ... webhooks
```

The extension pushes webhook notifications onto the CKAN celery queue, so that the web app won't block executions while the webhooks are firing. For this reason you need to make sure the celery daemon is running:

``` sourceCode
paster --plugin=ckan celeryd -c development.ini
```

Or if you are using datacats:

Usage
-----

At the moment there is no web interface to create Webhooks. Please make one if you're up for it! For now, hooks must be registered through the action API. For example:

``` sourceCode
import ckanapi
ckan = ckanapi.RemoteCKAN('http://some.ckan.org')

#create webhook
hook = ckan.action.webhook_create(topic="dataset/create", address="http://example.com/callback")

#show webhook
ckan.action.webhook_show(id=hook)

#delete webhook
ckan.action.webhook_delete(id=hook)
```

Supported Topics
----------------

-   dataset/create
-   dataset/update
-   dataset/delete
-   resource/create
-   resource/update
-   resource/delete

Authentication
--------------

There is a minimal authentication as you may restrict creation of webhooks to users who are editors or administrators of organisations. You may add a config option to your CKAN file as below where the value is one of editor, admin, sysadmin or none, specifying the minimum roles required to be able to interact with webhooks.

> \# Only let sysadmins create hooks ckanext.webhooks.minimum\_auth = sysadmin
>
> \# Only let admins and editors create hooks ckanext.webhooks.minimum\_auth = editor

Some other notes:

-   Each webhook gets a random id that is sufficiently long to be impractical to guess.
-   A user needs to keep track of their webhook ids in order to delete a webhook. The id is returned on webhook creation, and it is also passed in the webhook execution call, so if the user loses it, they can fetch it next time the webhook is executed.

TODO/Wishlist
-------------

-   Access control: Make sure access-restricted events do not leak
-   API authentication for private events.
-   Retrieve a list of registered webhooks for a given API key.
-   Filter: subscribe by entity id, for selective dataset/resource/etc...
-   Retry failed hooks with exponential decay
-   Delete stale unresponsive hooks
-   More hooks!


