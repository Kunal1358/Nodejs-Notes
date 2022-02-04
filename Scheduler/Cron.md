# [Cron](https://www.npmjs.com/package/node-cron)

The node-cron module is tiny task scheduler in pure JavaScript for node.js based on GNU crontab. This module allows you to schedule task in node.js using full crontab syntax.

<br>

Syntax

    var cron = require('node-cron');

    cron.schedule('* * * * *', () => {
      console.log('running a task every minute');
    });

<br>

## Cron Syntax

<br>

      ┌────────────── second (optional)
      │ ┌──────────── minute
      │ │ ┌────────── hour
      │ │ │ ┌──────── day of month
      │ │ │ │ ┌────── month
      │ │ │ │ │ ┌──── day of week
      │ │ │ │ │ │
      │ │ │ │ │ │
      * * * * * *

<br>

## Allowed values

<br>

| field        | value                             |
| ------------ | --------------------------------- |
| second       | 0-59                              |
| minute       | 0-59                              |
| hour         | 0-23                              |
| day of month | 1-31                              |
| month        | 1-12 (or names)                   |
| day of week  | 0-7 (or names, 0 or 7 are sunday) |

<br>

## Using multiples values

    var cron = require('node-cron');

    cron.schedule('1,2,4,5 * * * *', () => {
      console.log('running every minute 1, 2, 4 and 5');
    });

<br>

## Using ranges

    var cron = require('node-cron');

    cron.schedule('1-5 * * * *', () => {
      console.log('running every minute to 1 from 5');
    });

<br>

## Using step values

    var cron = require('node-cron');

    cron.schedule('*/2 * * * *', () => {
      console.log('running a task every two minutes');
    });

<br>

# Using names

For month and week day you also may use names or short names. e.g:

var cron = require('node-cron');

    cron.schedule('* * * January,September Sunday', () => {
      console.log('running on Sundays of January and September');
    });

Or with short names:

    var cron = require('node-cron');

    cron.schedule('* * * Jan,Sep Sun', () => {
      console.log('running on Sundays of January and September');
    });

<br>

# ScheduledTask methods

<br>

## Start

Starts the scheduled task.

    var cron = require('node-cron');

    var task = cron.schedule('\* \* \* \* \*', () => {
    console.log('stopped task');
    }, {
    scheduled: false
    });

    task.start();

<br>

## Stop

The task won't be executed unless re-started.

    var cron = require('node-cron');

    var task = cron.schedule('\* \* \* \* \*', () => {
    console.log('will execute every minute until stopped');
    });

    task.stop();

<br>

## Destroy

The task will be stopped and completely destroyed.

    var cron = require('node-cron');

    var task = cron.schedule('\* \* \* \* \*', () => {
    console.log('will not execute anymore, nor be able to restart');
    });

    task.destroy();

<br>

## Validate

Validate that the given string is a valid cron expression.

    var cron = require('node-cron');

    var valid = cron.validate('59 \* \* \* _');
    var invalid = cron.validate('60 _ \* \* \*');
