---
layout: single 
classes: wide
title: "eLikas (College Capstone)"
excerpt: "A Progressive Web App (PWA) designed to provide real-time flood data and safe routing for communities."
header:
  overlay_image: /assets/images/elikas-banner.png
  overlay_filter: 0.5
  teaser: /assets/images/elikas-teaser.png
author_profile: true
---

**eLikas** is a crowdsourced flood and evacuation mapping Progressive Web App (PWA) designed to address urban flooding in the Philippines. It combines crowdsourced reports with real-time IoT sensor data to provide flood-level information and safer evacuation routes.

<div class="notice--info">
  <strong>🌐 Explore eLikas</strong><br>
  <a href="https://elikas.solarflare-tilapia.ts.net/" target="_blank" rel="noopener noreferrer">
    Visit the live application →
  </a>
</div>

<img src="/assets/images/elikas-page.png">

As a senior capstone team member for this **Best Capstone-Nominated project**, I worked across backend development, database engineering, IoT, networking, infrastructure, and DevOps: 

### Technical Contributions
* Designed, deployed, and administered a normalized **MariaDB** database supporting GIS data, polymorphic relationships, and high-frequency sensor logs; used **DBeaver** for database management and development
* Developed **RESTful APIs with Laravel/PHP** for application, crowdsourced reporting, and IoT data workflows
* Built **ESP32**-based ultrasonic flood sensors using Arduino IDE, enabling real-time water-level collection and HTTP transmission
* Administered a private **Tailscale** network, managing access control and secure communication across services and development environments; used **Tailscale Funnel** for secure service exposure
* Built and self-hosted a BRouter routing engine and developed a custom routing profile for evacuation routing
* Configured **Nginx** as a reverse proxy and web server for the main eLikas site and self-hosted media services
* Deployed and maintained services on self-managed **Proxmox** infrastructure using **Docker** and **Linux Containers**
* Built **CI/CD pipelines with GitHub Actions** and **automated end-to-end testing with Playwright**
* Authored developer guides and technical documentation to support team knowledge transfer
* Authored the project's Data Use and Privacy Policy, documenting how platform data is collected, processed, stored, and used
* Provided technical troubleshooting and infrastructure support throughout the project lifecycle


<div style="position: relative; width: 100%; height: 0; padding-top: 56.2500%;
 padding-bottom: 0; box-shadow: 0 2px 8px 0 rgba(63,69,81,0.16); margin-top: 1.6em; margin-bottom: 0.9em; overflow: hidden;
 border-radius: 8px; will-change: transform;">
  <iframe loading="lazy" style="position: absolute; width: 100%; height: 100%; top: 0; left: 0; border: none; padding: 0;margin: 0;"
    src="https://www.canva.com/design/DAHJUf_2tqU/nbWwuY9dw9XrZZkh-To6oQ/view?embed" allowfullscreen="allowfullscreen" allow="fullscreen">
  </iframe>
</div>

### The Idea Behind eLikas

The idea behind eLikas started from a problem I had experienced myself. As a student commuting to class, I had more than a few occasions where I ended up late because of unpredictable weather and flooding. My everyday route could become impassable after just an hour or two of heavy rain, leaving me to figure out which detours were still accessible. I would often turn to Facebook for reports from other people or Waze to look for alternate routes (or when all hope is lost, I'd have to ask strangers starting their morning on the flooded roads), but neither was really designed around helping me make decisions to get where I need to go.

When we started exploring ideas for our capstone, we wanted to build something that could make this kind of information more accessible and useful. What started as a concept for crowdsourced flood reporting gradually expanded into a broader platform for responding to flooding. We added evacuation routing and emergency hotlines, giving users not only information about where flooding was happening but also possible ways to respond to it.

Eventually, we added another layer: physical flood sensors (more on that [here](https://alex-carreon.github.io/projects/esp32-sensor/)). Crowdsourced reports could provide information from people on the ground, while sensors could continuously provide measurements from fixed locations. eLikas ultimately became a combination of these ideas, as a platform that could bring together community reports, real-time environmental data, maps, and emergency information in one place.


### Designing the Infrastructure

One of my first major responsibilities was designing the database that would hold everything together. We were recommended to use MariaDB for the project, particularly because of its performance and suitability for the relational and geographic data we needed to manage. Most of our prior database experience had been with SSMS, so working with MariaDB also meant adapting some of the tools and workflows we were already familiar with.

I designed and deployed the database around the application's different data requirements, including user-generated reports, geographic information, polymorphic relationships, and the high-frequency measurements eventually produced by our sensors. I decided to use DBeaver for database development and administration, which gave me a different workflow from the SSMS environment I was more accustomed to, but also allowed me to explore some powerful and incredibly useful tools and features (*Thank you, open source*). 

From there, we built the backend around the database using Laravel/PHP and RESTful APIs. The overall architecture was deliberately modular: the React-based PWA communicates with the backend through the API, while the backend handles authentication, application logic, and data processing. External services such as Firebase Identity Management, OpenStreetMap, BRouter, OpenAI Moderation, and IPROG SMS provide specialized functionality without putting those responsibilities directly into the application.

<img src="/assets/images/elikas-architecture.png">


### Connecting Everything Together

I deployed eLikas on self-managed Proxmox infrastructure, using Docker and Linux Containers to run its different services. I also administered our private Tailscale network for secure communication between development environments and services, configured Nginx as a reverse proxy, and self-hosted the BRouter routing service with custom routing behavior for evacuation use cases.

Since there were multiple of us working on different things, I also built the project's GitHub Actions CI/CD pipelines and Playwright end-to-end tests to make deploying and maintaining the system more manageable. This allowed us to continuously deploy new features and improvements while reducing regressions as we built more and more.

Because eLikas was a team project, I also took the opportunity to make my work understandable and maintainable beyond my own development environment. I practiced how to write developer guides and technical documentation in markdown for knowledge transfer, as well as authored the project's Data Use and Privacy Policy as an application of concepts I learned in my security electives, including IT audit, governance, and compliance.

For me, this became one of the more important parts of the project. eLikas wasn't simply an application we needed to make work for a demonstration. It was a full-fledged, living system with a database, backend, physical devices, networks, external services, and infrastructure all depending on one another. At every turn, I tried to keep the perspective of the end user in mind, asking myself how I would want the system to behave if I were the person relying on it to guide our decisions. Working across those layers taught me to think less about individual technologies and more about how an entire system needs to be designed, deployed, and maintained as a whole.