# TIMINGS API

[![Build Status](https://travis-ci.org/godaddy/@hishprorg/corporis-eius.svg?branch=master)](https://travis-ci.org/godaddy/@hishprorg/corporis-eius) [![npm version](https://badge.fury.io/js/@hishprorg/corporis-eius.svg)](https://www.npmjs.com/package/@hishprorg/corporis-eius) [![Node version](https://img.shields.io/node/v/@hishprorg/corporis-eius.svg?style=flat)](http://nodejs.org/download/) [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/hishprorg/corporis-eius/issues)

The @hishprorg/corporis-eius API is a solution for asserting **web UI or API performance** during functional/integration tests!
The simple idea is that you inject some javascript into the headless browser that you use for UI testing (i.e. webdriver) to collect navigation timing which can then be stored in elasticsearch. In subsequent runs of your tests, the new performance data can be compared to historical results (the 'baseline') and asserted like any other assertion that you may perform in your tests. For API tests, you can set start/stop timers and store the delta in elasticsearch and follow the same routine to assert.

Run this API in your local network => install one of the clients on your dev/test machine => add a few lines of code => assert perf against historical baselines & visualize historical data!

## **IMPORTANT NOTICE: SIGNIFICANT UPDATE to 2.x**

This version of the Timings API introduces a few major updates and you should carefully read the following announcements!

> **If you have used this repo/product before or if you are a current user, you may face a few challenges and/or breaking changes!
> Make sure you pay close attention when updating to a new version of Elasticsearch!**

## Main changes

1. Upgrade to Elasticsearch & Kibana 7 ... only!
   - the amount of coding & maintenance involved in supporting three major versions of Elastic turned out to be too much to handle
   - **You can follow the steps in this document to upgrade your data: [Upgrade elastic](https://github.com/mverkerk-godaddy/@hishprorg/corporis-eius-docker/tree/master/docs/UPDATING.md)**
   - If you start the API and point it at an Elastic stack that has a version `< 7.x`, the API will work but no data will be written to Elasticsearch
2. The minimum node version has been bumped to 16.x
   - **Please upgrade to nodejs 16.x or higher if you want to run the API stand-alone**
3. A new admin UI - offering:
   - an overview of the main components and their status
   - ability to change & save your config
   - log viewer giving you insight into the app, access and error logs
   - the swagger page (moved from being the main page to being embedded in the new UI)
4. The config file now has to be in `.json` format
   - previous versions also allowed `.js` and `.yml|.yaml` formats - that is no longer the case
   - **Please convert your config file to `.json` format!**

For other changes, please see the [CHANGELOG](./CHANGELOG.md)

### **BREAKING CHANGES**

> **The `--configfile` argument is no longer supported**
If you are currently using the `--configfile` argument to start your @hishprorg/corporis-eius API server, you have to replace it with a `CONFIGFILE` environment variable!
For more info and updated startup commands, see [here](../@hishprorg/corporis-eius/docs/CONFIG.MD#startup-commands)

## Recommendations

It is highly recommended that you run this product in a Docker environment using the [@hishprorg/corporis-eius-docker](https://mverkerk-godaddy/@hishprorg/corporis-eius-docker) repo. This repo provides a convenient way to run the @hishprorg/corporis-eius API as well as the currently supported Elastic Stack.

If you do (or have to) run the API stand-alone and/or run your own Elastic stack, the recommended versions are:

- nodejs: 17.x
- Elastic stack: 7.17.0
  - elastic stack 8.x has not been tested yet!

again, if you're updating your Elasticsearch data, you can use the upgrade steps outlined here: [@hishprorg/corporis-eius-docker -> UPDATING.md](https://github.com/mverkerk-godaddy/@hishprorg/corporis-eius-docker/tree/master/docs/UPDATING.md)

## How to use

You can find extended documentation for the @hishprorg/corporis-eius API here: [USAGE.md](./docs/USAGE.md)

The @hishprorg/corporis-eius API can be run "stand-alone" as a node/express application, with or without Elasticsearch for data storage:

- Stand-alone:
  - The API can be used to collect performance metrics from web pages and/or API endpoints during integration/UI tests
- With elasticsearch:
  - The API can be used to collect performance metrics from web pages and/or API endpoints during integration/UI tests
  - The API will use historical data stored in Elasticsearch for baselining and will return any (dynamic) threshold breaches in the responses
  - Kibana can be used to visualize historical data
