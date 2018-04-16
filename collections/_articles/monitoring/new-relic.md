---
title:  "Application Performance Monitoring: New Relic"
date:   2017-08-11 00:00:00 -0400
last_modified_at: 2017-08-11 00:00:00 -0400
categories:
  - Monitoring
tags: 
  - new relic
  - performance
  - dashboard

author: Kevin Sutton
sidebar:
  title: ""
  nav: content-nav
toc: true
---
## Introduction
New Relic's digital intelligence platform lets developers & operations (DevOps), and tech teams measure and monitor the performance & availability of their applications, micro-services, and infrastructure. It has many modules like APM, Browser, Synthetics, Mobile, Insights, Infrastructure, Servers...etc.  We will be leveraging the following primary features/modules for our DT monitoring needs.

- <a href="https://newrelic.com/application-monitoring" target="_blank">Application Performance Monitoring (APM)</a>: Application Monitoring in one place allows you to see your application performance trends at a glance – from page load times, to error rates, slow transactions, and a list of servers running the app.
- <a href="https://newrelic.com/synthetics" target="_blank">Synthetics</a>: Simulate user behavior with global monitors to catch problems before your customers do.
- <a href="https://newrelic.com/insights" target="_blank">Insights</a>: Real-time analytics to better understand the end-to-end business impact of your software performance.
- <a href="https://newrelic.com/mobile-monitoring" target="_blank">Mobile</a>: Understand how the user’s experience is affected by performance issues with visibility to code-level inefficiencies, crash logs, etc. – for iOS and Android.
- <a href="https://newrelic.com/alerts" target="_blank">Alerts & Notifications</a>: Full stack alerting through a single tool with integration to third party plugins like PagerDuty, Slack, etc.

## Enablement
### Pre-Requisites
1. You will need a Product-specific New Relic account to enable monitoring.  The same account can be shared between Dev, QA, and Production instances, if desired.  If an account is not currently available, you will need BUC/ADN details for charge-back and can request a New Relic account.
2. When a New Relic account is available, you will need to collect the license-key (can be found under "Account settings", "License key" sections of your profile.
3. Review agent installation instructions for the appropriate tech stacks within your Product.

#### Requesting for New Relic account
Follow this link to request a New Relic account: [Raise a support ticket](https://devcloud.swcoe.ge.com/devspace/display/MFOXY/Monitoring#Monitoring-RequestingforNewRelicaccount) 

### Installation Steps for New Relic APM Agent
- <a href="https://docs.newrelic.com/docs/agents/java-agent/installation/install-java-agent" target="_blank">Install New Relic for Java</a>
- <a href="https://docs.newrelic.com/docs/agents/go-agent/get-started/install-new-relic-go" target="_blank">Install New Relic for Go</a>
- <a href="https://docs.newrelic.com/docs/agents/nodejs-agent/installation-configuration/install-maintain-nodejs" target="_blank">Install New Relic for Node.js</a>
- <a href="https://docs.newrelic.com/docs/agents/php-agent/installation/php-agent-installation-overview" target="_blank">Install New Relic for PHP</a>
- <a href="https://docs.newrelic.com/docs/agents/python-agent/getting-started/new-relic-python#installation" target="_blank">Install New Relic for Python</a>
- <a href="https://docs.newrelic.com/docs/agents/ruby-agent/installation-configuration/ruby-agent-installation" target="_blank">Install New Relic for Ruby</a>

### Installation Steps for New Relic Mobile
- <a href="https://docs.newrelic.com/docs/mobile-monitoring/new-relic-mobile-ios/get-started/ios-installation-configuration" target="_blank">iOS Installation & Configuration</a>
- <a href="https://docs.newrelic.com/docs/mobile-monitoring/new-relic-mobile-android/get-started/android-installation-configuration" target="_blank">Android Installation & Configuration</a>

### Connecting Predix Applications to New Relic
Applications hosted within the Predix platform require a connection through a back-end Custom User Provided Service (CUPS).  Follow these steps to create this service and bind your application(s):

1. Ensure you have a New Relic account license key handy (can be found under "Account settings," and "License key" within your New Relic profile.
2. Create your Custom User Provided Service – Always append "-newrelic" to the service name for appropriate tagging.  *Note, ensure you include the escape character (\\) for windows.
3. Update your application manifest-<ENV>.yml configuration file to include a binding to the new service.
4. Deploy, or redeploy, your application to Predix/CF.

{% highlight bash %}
Step 2:
-------
cf cups YOUR_CUSTOM_SERVICE_NAME-newrelic -p '{"licenseKey":"<YOUR_NEW_RELIC_LICENSE_KEY>"}'

Step 3: (manifest.yml file)
-------
services:
- YOUR_CUSTOM_SERVICE_NAME-newrelic
NEW_RELIC_APP_NAME:  YOUR_CUSTOM_APPLICATION_OR_API_NAME
NEW_RELIC_KEY: YOUR_NEW_RELIC_LICENSE_KEY
ENABLE_NEWRELIC_MONITORING: true

Step 4:
-------
cf push <your-service-or-app-name>
{% endhighlight %}

If you are logged into your New Relic dashboard, you will need to log out and back in to see the updated content.  Once the application has been bound, you should see reporting listed in the Custom Application Name used in Step 3 above.

## Steps for Synthetics
### Ping Monitoring
Ping monitoring is a simple ping to a given URL.  With configuration parameters like name, locations, and frequency, one can setup a monitor to ping the given URL and validate results on the returning content.

### API Test Monitoring
API Test monitoring uses an http client to monitor and emulate on the remote API endpoints by having configuration parameters like name, locations, frequency.  Additionally, you have flexibility to provide API scripts as well.  A sample script is provided below for reference.

{% highlight js linenos %}
/**
* Feel free to explore, or check out the full documentation
* https://docs.newrelic.com/docs/synthetics/new-relic-synthetics/scripting-monitors/writing-api-tests
* for details.
*/
 
var assert = require('assert');
 
$http.post('http://httpbin.org/post',
// Post data
{
        json: {
        widgetType: 'gear',
        widgetCount: 10
    }
},
// Callback
function (err, response, body) {
        assert.equal(response.statusCode, 200, 'Expected a 200 OK response');
 
        console.log('Response:', body.json);
        assert.equal(body.json.widgetType, 'gear', 'Expected a gear widget type');
        assert.equal(body.json.widgetCount, 10, 'Expected 10 widgets');
    }
);
{% endhighlight %}

## Standards
Here are a few guidelines & standards while doing enablement of New Relic for your application or services, resources, etc.
- While creating cups service (create-user-provided-service) for New Relic using the license key, make sure to have the name as `<DT-Product-Name>-newrelic`.  For example, for DAP it is `dap-newrelic`.
- Make sure to have environment specific configuration files (`manifest-<ENV>.yml`) and have the `NEW_RELIC_APP_NAME` as per the environment `<DT-Product-Name>-<ENV>-<Application-or-API-Name>-<App-or-API>`.  For example, the DAP Asset service in the DEV environment is set to monitor as:  `DAP-DEV-Asset-API`.
- Use the flag `ENABLE_NEWRELIC_MONITORING: true` to enable/disable monitoring for your applications.
- Follow the similar above approach even for the Synthetics as well and adhere something like this `<DT-Product-Name>-<ENV>-<Application-or-API-Name-or-UI-App-Resource-Name>-<API-or-UI-or-Resource>`.  For example, the DAP Asset service in the DEV environment is set to monitor as:  `DAP-DEV-Asset-API`.
- Use a selection of locations or regions reasonable for Synthetics monitoring according to your user-base.
- Use the time time frequency on your Ping or API Test monitoring configurations wisely.  For example, use larger wait periods (like 30 mins) to reduce the number of calls.
- Get NFR SLAs for your applications/services from the Product Owner and use them to set Apdex thresholds against your Synthetic monitors or APM apps.

#### Reference App
One of the DAP micro services (dap-asset-service) that has been enabled with the above steps can be found at the following github with its sample APM app link New Relic:
- DAP Asset Service <a href="https://github.build.ge.com/Digital-Asset-Passport/dap-asset-service" target="_blank">Github</a>
- DAP Asset Service <a href="https://rpm.newrelic.com/accounts/1603198/applications/45307719" target="_blank">New Relic Dashboard</a>

## Resources
### Internal
- GE Digital's license related information for Predix apps monitoring can be found at: <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB0011291" target="_blank">License and Pricing</a>
- <a href="http://sc.ge.com/*NewRelicSetup" target="_blank">New Relic Account Request Form</a>
- <a href="https://devcloud.swcoe.ge.com/devspace/display/KKQTL/New+Relic+Integration" target="_blank">New Relic Integration for enablement for Node.js apps</a>
- <a href="https://devcloud.swcoe.ge.com/devspace/display/PTIQX/How+to+setup+New+Relic+for+CF+apps" target="_blank">How to setup New Relic for Cloud Foundry</a> or <a href="https://devcloud.swcoe.ge.com/devspace/display/PTIQX/How+to+setup+New+Relic+for+CF+apps" target="_blank">How to Setup New Relic for Predix App enablement for Java</a>
<a href="" target="_blank"></a>

#### Useful KB Articles for New Relic
- <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB0011286" target="_blank">What is New Relic?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0011802" target="_blank">What Are Services In New Relic?</a>
- <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB0011290" target="_blank">How do I add new users to my account in New Relic?</a>
- <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB001129" target="_blank">How am I charged for a New Relic Account?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0011803" target="_blank">What is the pricing for all New Relic Services?</a>
- <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB0011292" target="_blank">Where can I learn more about using New Relic?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0011804" target="_blank">Why are my charts missing or not rendering?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0011809" target="_blank">What are the minimum support browser versions?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0011806" target="_blank">Why Is There A CPU usage mismatch or usage over 100%?</a>
- <a href="https://gesoftware.service-now.com/kb_view.do?sysparm_article=KB0012143" target="_blank">What is considered a host in New Relic?</a>
- <a href="https://gesoftware.service-now.com/kb_view_customer.do?sysparm_article=KB0010802" target="_blank">How to delete an app from New Relic APM console</a>

### External
- <a href="https://learn.newrelic.com" target="_blank">Learn More About New Relic</a>
- <a href="https://docs.newrelic.com" target="_blank">New Relic Documentation</a>
- <a href="https://newrelic.com/application-monitoring" target="_blank">New Relic APM</a>
- <a href="https://newrelic.com/synthetics" target="_blank">New Relic Synthetics</a>
- <a href="https://docs.newrelic.com/docs/agents" target="_blank">New Relic Supported Agents List</a>
- <a href="https://docs.newrelic.com/docs/agents/go-agent" target="_blank">New Relic and Go</a>
- <a href="https://blog.newrelic.com/2016/08/23/go-agent-apm" target="_blank">Go and New Relic</a>
- <a href="https://github.com/newrelic/go-agent" target="_blank">Go Agent for New Relic</a>
- <a href="https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measuring-user-satisfaction" target="_blank">Apdex Guidelines</a>
- <a href="https://newrelic.com/apm-best-practices" target="_blank">New Relic APM Best Practices</a>