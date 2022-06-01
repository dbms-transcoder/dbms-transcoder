---
layout: home
title: About dbms-transcoder
permalink: /about/
---
## Goal
The purpose of this website is to share information on concepts that have similarities across DBMS platforms. Many DBAs have deep knowledge in one platform, but need to be able to use other platforms. Many other technicians may need to be able to understand very specific concepts in more general terms. It is hoped that this site can provide some of that translation and allow many to collaborate to provide useful content.
## Organization
Since things are barely commonly named within a platform, much less across platforms, I've grouped concepts into several categories to make it more possible to find things.
The categories are implemented as tags, and are generally:
* dbms-software - installing, updgrading, and patching the database software
* dbms-architecture - architectural and implementation details of database management software.
* dbms-settings - settings at whatever level for the database. May often be in conjunction with other tags
* db-objects - tables, indexes, stored procedures, etc - all of the objects that database software uses
* sql - sql language details and syntax, including optimization and explain
* data - data types, character sets, and related concepts
* db-security - security, users, authorization, and authentication
* db-logs - transaction logging  and other kinds of logging not covered in other tags
* db-acid - ACID-compliant transactions and concepts of avoiding ACID compliance
* db-errors - error messages, error handling
* db-backup - backup, restore, and recovery
* db-maintenance - collecting statistics, rebuilding/reindexing/reorganizing and related concepts
* db-scalability - partitioning, sharding, and clustering in any dimension
* db-ha - high-availability, disaster recovery
* replication - data replication
* db-perfromance - database and sql performance

## Contributing
The github repo for this content is [https://github.com/dbms-transcoder/dbms-transcoder](https://github.com/dbms-transcoder/dbms-transcoder)
This content is published from the netlify branch of that repository, not from main.
Pull requests are welcome. This site is published using Jekyll. This means that anyone can clone the repository and add their own content via a pull request. At this time, Ember Crooks must read and approve all content. Content needs to meet the following standards:
1. Each concept/term must be correctly tagged, and must include content from at least two DBMS platforms. Tags are really important to get right, feel free to ask if you are unsure. If information is not available for at least two different platforms, perhaps the content does not belong on this site.
1. Not all platforms have to be represented on each post. Often authors don't know all of them. Pull Requests are also welcome adding content for a platform to an existing post.
1. Please provide links to official documentation and other blog entries or sources so readers may explore.
1. When adding a post in the _posts folder, it is best to copy an existing one to get all of the right header information. Post format is generally markdown, but please use tabs to separate dbms-specific content. File name for posts MUST be `YYYY-MM-DD-title-without-spaces.md`.
1. Adding a new tag requires a new page in the tag folder.
1. Adding a new author requires a new page in the people folder. Please include a basic bio, and any links, social media profiles, or contact information you would like to share.

If you have issues with existing content or organization, please feel free to open an issue, with the understanding that this is a site maintained in our free time, and no response is guaranteed.

The license should provide you with details about how this content should and should not be used.
