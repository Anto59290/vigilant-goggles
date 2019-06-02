---
published: true
layout: post
title: "Django 2.1 is out !"
category: jekyll
---

Last week a brand new version of one the most popular framework on the web was revealed. Let’s dive into the change-log.

Django is one of the most popular web frameworks around the world, and this is a millestone for the Django ecosystem as the latest version of Django (aka Django 2.1) as just been released. Let’s take a look at some of the changes that were made, stuff that were added and things that were removed. For a complete changelog fell fee to have a look to the official Django release notes: [https://docs.djangoproject.com/en/dev/releases/2.1/](https://docs.djangoproject.com/en/dev/releases/2.1/)

## Django, Python, and life-cycle

After the release in December 2017 of Django 2.0, the Django Core team and all the contributors started a new development cycle to release version 2.1. For each version of Django, the dev team follows the same process:

* An integration phase with new features, bug fixes, and tweaks.

* A first alpha version (Alpha 1). From this version all the features are frozen, only bug fixes will be accepted.

* A beta version, correcting all the bugs that were found during Alpha version.

* One or many release candidates version. Those are the closest versions to the final one. At this time only the critical bug fixes are accepted to be sure the framework is stabilized before the official release.

* The final, “stable” release.

This cycle continues since 2015 and enables to have a major release every eight months, and a long-term support (LTS) every two years. Indeed one version out of three is an LTS version. This life-cycle is designed to keep new features flowing-in while providing stable releases frequently. As the LTS version is supported for three years, the Django community as one year to bump from an LTS version to another in the case they don’t want to use the intermediate versions.

The 2.0 version of the Django framework was the first version to drop support for Python 2.7. With Django 2.1 support for Python 3.4 is now dropped.

![The Django life-cycle — Source:[Django documentation](https://www.djangoproject.com/download/#supported-versions) — Unknown author](https://cdn-images-1.medium.com/max/2060/1*6ETbCGEOv805Bz57dy0G5A.png)*The Django life-cycle — Source:[Django documentation](https://www.djangoproject.com/download/#supported-versions) — Unknown author*

## What was changed?

Now that we had at look to the Django life-cycle let’s have a look at some changes that were made.

### The new model view permission

Django models come with three base permissions that can be given to specific users. These permissions are to add, to edit, and to delete an object. This latest 2.1 release introduces the new view permission. This permission allows a specific user (or group of user) to view an object without the possibility to make any action on it. This can be used in a couple of different ways, two of them are particularly useful:

* Restricting access to a view using the PermissionRequiredMixin.

* Giving a read-only access to the Django Admin, for example for a few specific power users.

### Tweak of management commands

In the Django ecosystem, management command is a great interface to operate tasks on a server using all of the Django features (app loading, logger, ORM, etc.). At [BackMarket](https://www.backmarket.fr/) we use them for periodic tasks via cron or to execute unusual tasks on a server. In the last release, a little tweak was made inside the BaseCommand class that is used for management commands. It now uses a specific formatter that sort the help output so that your custom options are on top of the standard options (such as — verbosity or — settings).

### Models and databases

Since Django 1.8, database functions were added. They enable to make very powerful queries using the ORM. For example the following snippet retrieves all the authors with a name longer than seven characters:

    Author.objects.filter(name__length__gt=7)

No less than eleven new text functions were added, which enables even more powerful queries. For example why can now get only the five last characters of a name using Right text function:

    author = Author.objects.annotate(last_letter=Right('name', 5))

Here is the full list of the new text functions : **Chr, Left, LPad, LTrim, Ord, Repeat, Replace, Right, RPad, RTrim, and Trim**. See [the documentation](https://docs.djangoproject.com/en/2.1/ref/models/database-functions/#module-django.db.models.functions) for more details.

Another nice addition concerning the database is the introduction of an explain method for querysets. For example this query:

    Choice.objects.filter(question__pk=1).explain()

Will result in this output:

    SEARCH TABLE polls_choice USING INDEX polls_choice_question_id_c5b4b260 (question_id=?)

I believe this is a nice way to compare two different approaches or two get an under the hood view of what is going on when we are using the ORM.

A few backward incompatibilities were also added, in particular support was dropped for MySQL 5.5 and PostgreSQL 9.3. These latter will both get deprecated upstream by the end of 2018.

## Django 2.2 is already on the way!

That’s all for the latest changes made in Django! As we’ve seen, no major changes here, but the team is still improving the framework. If you wonder what is going to be included in the next version of Django, well the development has already started and [the future release notes are available](https://docs.djangoproject.com/fr/2.1/releases/2.1.1/). The version 2.1.1 of the Django framework is expected around September 1, in the meantime, happy coding!

