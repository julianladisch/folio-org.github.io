---
layout: page
title: How to obtain reference environment module logs
titleLeader: "FAQ |"
menuTopTitle: Guides
categories: development-tips
faqOrder: 13
---

Developers can obtain the Docker logfiles for backend modules from the [reference environment](/guides/automation/#reference-environments) daily builds.

Visit the Jenkins job [collect-reference-env-logs](https://jenkins-aws.indexdata.com/job/Automation/job/collect-reference-env-logs/) (and ensure Jenkins [login](/guides/automation/#jenkins)).
Select "Build with Parameters" from its left-hand panel.

Define which host. Declare the list of modules for which to gather their logs. Declare the Slack channel or Slack user to notify.
For example notify yourself, or another person, or notify your team channel.

All members of folio-org are configured to run this job. The job creates a tar file containing the specified logs (and also the Okapi log) and uploads to an S3 bucket. A URL to fetch the logs is returned via a Slack notification.
