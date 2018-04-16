---
title: "Guardrails Hackathon: DDK PoC"
date: 2017-10-30 00:00:00 -0400
last_modified_at: 
category: Announcements
tags: 
 - announcement
 - hackathon
 - ddk

author: Kevin Sutton
author_profile: true
sidebar:
  title: ""
  nav: content-nav
toc: true

header:
  image: /assets/images/article-resources/header-images/dth-aerial.jpg
---

## Introduction
The DT Guardrails team came together last week in the Detroit Tech Hub to coordinate a one-week hackathon geared towards software standards & best practices.  An ad-hoc software development mini-pod was pulled together from volunteer resources for the effort.  They brainstormed on ideas, built an expected outcome, and executed Agile ceremonies alongside the current AppStudio already underway for Ops Advisor.

### Hackathon Team
- **Kevin Sutton**, Product Owner & Software Architect / Engineer
- **Nick Stelter**, Fronend Software Engineer
- **Om Soni**, Backend Engineer
- **Brandon Moner**, UX Designer
- **Scott Paar**, Agile Coach

## Proof-Of-Concept Goal
The high-level objective was to create a tool that could help automate the implementation of the 'Non-negotiable Guardrails' that were declared for 2017 (by Anup Sharma):
1. CICADA
2. SonarCube
3. New Relic
4. Google Analytics & Google Tag Manager

### Scope
To meet the objective, the team chose to focus on implementation of CICADA into a new or existing software product.  If successful, anyone on a current dev pod should be able to generate the configuration files required to activate CICADA within their Github Repo.

### Assumptions
1. The Product would already be onboarded with the CICADA team.
2. Any required configuration tools would already be installed (standard installation procedures to be defined later) -- i.e. Node.js, homebrew, etc.

### Requirements
1. The PoC would reside in Predix (DTS Org)
2. CICADA would be used to deploy all components of the Product
3. Code-name would be selected for the Product, with big-picture branding capabilities

## Delivery
<img src="/assets/images/article-resources/ddk-logo.png" alt="Drone Deploy Kit" style="float: right; margin: 5px; border: 0px solid black;" />
During the Friday Sprint Review, the team successfully presented out both the concept as well as a working Product PoC (live software, no PPTs).  The Product was code-named **Drone Deploy Kit (DDK)** and presented a simplified UI where a user could walk through configuration screens for the CICADA-DDK package.  

1. The UI provides the User with a list of available packages for selection.
2. The UI communicates with a Backend API, which determines appropriate configuration options & requirements which are presented back to the User.
3. After configuration details are provided by the User, they are sent back to the API where they are translated into execution commands for the local configurator.
4. The commands are copied into the local clipboard & pasted into a Terminal window (Mac or Windows).
5. A yeoman generator is executed completing a CICADA template file with provided User inputs.
6. The .cicada folder and configuration files are automatically added to the local repo.

  <figure>
    <a href="/assets/images/article-resources/ddk-overview.jpg" tagret="_blank">
      <img src="/assets/images/article-resources/ddk-overview.jpg" alt="DDK Overview" />
    </a>
    <figcaption>Fig1. - A high-levek overview of the DDK components.</figcaption>
  </figure>

  <figure>
    <a href="/assets/images/article-resources/ddk-architecture.jpg" tagret="_blank">
      <img src="/assets/images/article-resources/ddk-architecture.jpg" alt="DDK Architecture" />
    </a>
    <figcaption>Fig2. - A deailed walkthrough of DDK transactions.</figcaption>
  </figure>

## Outcome
The event was a success and the PoC seemed to be well received by both Leadership and Developers alike.  There were requests from several teams to stay engaged as the DDK Product matured.

Look for more to come soon as a formal team is build around automation to our Software Development Standards & Best Practices!  

In the meantime, you can review the <a href="/assets/docs/article-resources/ddk-intro-presentation.pdf" target="_blank">DDK Leadership presentation</a> that was put together shortly after the hackathon.