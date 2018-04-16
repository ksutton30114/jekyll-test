---
title:  "User Analytics & Tracking: Google Analytics & Tag Manager"
date:   2017-12-06 00:00:00 -0400
last_modified_at: 2017-12-06 00:00:00 -0400
categories:
  - Monitoring
tags: 
  - user tracking
  - google analytics
  - tag manager

author: Ken Shum
sidebar:
  title: ""
  nav: content-nav
toc: true
---
## Objective:
To gain further insight into Digital's Application Portfolio and how our users engage with it, we need to establish a common analytics and tracking platform that promotes easy adoption and maintenance.

## Description:
Most, if not all, of our applications are run in AppHub in Predix.  Tracking code injection into the Header tags is currently not supported in AppHub.  Tracking scripts/code will have to be injected at the MicroApp level.

In addition, most out of the box free web analytics/tracking solutions are designed to track web pages and have their own definitions of Users and Visits with typical session timeouts set for web browsing use cases.  MicroApps, per design, will be primarily SPA (single page applications) with long session timeouts.  Other apps, like Field Vision, runs on mobile devices and will not have connectivity at all times.  These requirements and more as we discover them will have to be accounted for in a universal solution.

## Requirements:
### Account Management:
Simple account hierarchy to provide Global view and management of all Properties (Apps).  Manage users to allow for consumers of data, dash boards, charts.

### Insights/Metrics:
The tracking/analytics platform must provide a minimum set of insights such as:
- Application usage
- User Count
- User Session Duration
- User Session Count
- Page Views
- User Demographics
- Browser and OS
- Screen Resolution
- New vs Returning User
- Most Actively viewed Screens(pages)
- Roll up metrics
- Event tracking
- TBD

### Adoption:
Minimal code changes to enable tracking across all applications.  Allow for targeting of user events as well as custom events to capture specific interactions or data for specific application needs with minimal effort.  For example, DAP will require the Search Term to be captured that is specific to the application.

First, there are a few requirements in order to be in compliance with GE and Google policies:
- Include a Privacy Policy on any page that uses Google Analytics. We just added a link to our footer that points to <a href="http://www.ge.com/privacy" target="blank">http://www.ge.com/privacy</a>.
- Make sure you are not collecting any PII (Personally-Identifiable Information). This includes the user's IP address, but Google has functionality to anonymize IP addresses (https://support.google.com/analytics/answer/2763052?hl=en). It's a matter of setting a field in the ga object (https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#anonymizeIp).
- Go through the compliance review process (http://itcompliance.digital.ge.com/) to explain what you are using Google Analytics for and that you are not collecting PII. Completing the above steps (privacy policy and IP address anonymization) should ensure you don't run into difficulty.

## Solution:
Google Analytics (GA), Managed by Google Tag Manager (GTM)

We will utilize Google Analytics as the analytics data store, reporting and discovery.  We will leverage GTM  to customize how and what GA will capture and track.  Account management will have to be done in both platforms.  Adoption and integration will have a very light foot print as well.

### Account Management and Structure
We will create an admin account in Google Analytics called "GE Digital Thread".  The master account will have Properties & Apps.  Each of our applications (CBM, DAP, etc) will be a property with a unique TrackingID.  For further drill down or refinement of reports, we can leverage Views and/or Segments from GA.  For example, DAP may want to segment the view by TenantID.  We can accomplish this using Views and/or advanced segments while all traffic at the Property Level will be all inclusive.

![GA Admin Console](/assets/images/article-resources/ga_admin.jpeg "GA Admin Console")

Each Property in GA will have a corresponding Container (unique ID) in GTM.  Since GTM is managing when GA Tags fire, the only script we need to integrate with our applications is the GTM tracking code.

### Metrics
GA will fulfill, out of the box, all the metrics mentioned above.  However, since we are tracking Single Page Applications (SPAs), we will need to do some work in GTM to make the Analytics in GA useful for our users.  GA is built for tracking how users engage with regular e-commerce websites.  As a typical user traverses through a site like amazon.com, you can imagine the following buyer flow:

> amazon.com --> amazon.com/searchResults?term=FuzzyBunnySlippers --> amazon.com/productPage?product=MensPinkBunnySlippers --> amazon.com/AddtoCart --> amazon.com/Checkout --> amazon.com/OrderConfirmation

If you take into account the number of customers going through the buyer flow as we traverse from left to right, we'll end up with a buyer funnel, laid on its side.  We need to capture similar actions on our SPAs using events, triggers, virtual pages and goals.  This will require us to look at the way our users engage with our SPAs as they click on buttons, lists, search and scroll and traverse through the application.

For more details on specific Metrics, see link.

### Adoption

To enable Analytics Tracking on your SPA, you need to add the GTM tracking script to the <HEAD> section of your SPA.  For example:

{% highlight js linenos %}
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-TZ111222');</script>
<!-- End Google Tag Manager -->
{% endhighlight %}

You will need to replace the example GTM container ID above (`GTM-TZ111222`) with the one assigned to your application.

To allow to quicker implementation of GA and GTM, developers need to follow the best practices for analytics guidelines.