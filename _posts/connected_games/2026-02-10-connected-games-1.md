---
layout: post
title:  "Connected Games #1 - Research"
date:   2026-02-10 00:00:00 +0000
categories: Connected Games
tags: [agones, unreal, multiplayer]
excerpt_separator: <!--more-->
---
This is a post in a series of devlogs I'll be doing for a Multiplayer Game project I'm working on as part of my Master's Program at Kingston University. In this post, we'll cover some initial planning done towards implementing a Dedicated Server Architecture using Unreal Engine and Agones for Server Orchestration.
<!--more-->

<br>Yeesh, this blog is covered in cobwebs. But hopefully this series of posts will get me into a habit of actually writing posts regularly and sharing them here so that I can justify having this domain name and not using it for anything other than my Projects page.

# Background
---
As mentioned above, I've recently started working on a Multiplayer game project as part of a group of other students from the Game Design and Game Development programs. This project expects us to implement various multiplayer and social features that are expected from modern offerings in the industry, like User identity management, Friends, Match-making, etc.

We've settled on an idea pitched by one of our designers that combines PvP and PvE experiences in tournament style matches between 4 teams of 3 through alternating rounds where the teams first fight against Computer-controlled opponents and then face off against another team to progress further. This gives us fertile ground in terms of experimenting with Lobby management and Matchmaking, owing to the number of players needed per match, the expected server load and match length.

In this post, I'll go over the initial research we did into the combinations of Server Hosting and Backend Services that we'd be using to power our game and some of the implementation steps we've made during the first two weeks of this project.

The main technical pillars we're aiming for this project include:
    - Dedicated Servers for Matches
    - Automated Server Orchestration with a Matchmaker Integration
    - Friends Interface and Party Matchmaking Support
    - Player Identity Authentication, Management and Data Storage

# Server Hosting and Management
---
Since we were targeting a PvP experience with a strong competitive aspect, Dedicated Servers were a foregone conclusion in keeping latency for Players low. For Server hosting, I looked at a few of the major Cloud Computing platforms and their gaming focused products to assess their technical feasibility and what was offered in their free tiers for this student project.

## <u>AWS GameLift</u>
By far the most popular offering in this space, [AWS GameLift](https://aws.amazon.com/gamelift/servers/) was my first pick when looking at hosting/compute providers. It's used in many popular titles like *Player Unknown's Battlegrounds*, *Warhammer 40K: Darktide* and has many resources for newer Game developers to take advantage of features like Fleet Management and their in-house matchmaking service called FlexMatch. Unfortunately their free tier only offered their basic compute products without any of the server orchestration tools.

## <u>Microsoft PlayFab Multiplayer Servers</u>
[PlayFab](https://playfab.com/multiplayer/) offered Real-time Game Server hosting along with many LiveOps and Game services, handling aspects like User Identity and Data Management, Lobby Management and WebRTC Voice Chat. While this provided a toolset with many of our requirements met, we wanted to handle more of the implementation ourselves as a learning experience and to challenge ourselves. Their Server SDK and their integrations with Unreal Engine also seemed to be more stale in development activity compared to the other options.

## <u>Google Cloud Platform</u>
This is the option we ended up going forward with. GCP powered titles like *Apex Legends* and offered the most Free Tier credits for evaluation purposes. Another big draw to this platform was [Agones](https://agones.dev/site/), an open-source server orchestration tool powered by Kubernetes that was primarily developed by a Google employee with resources for deploying to Google cloud. It provides us with enough infrastructure to meet our project timelines while still leaving enough implementation details for us to handle on our end.

# Backend Services
---
From our planned pillars, User Identity Management was one of the most important features to implement outside of the core gameplay loop. This includes storing User Identity on our servers and handling Authentication using e-mail or other identity providers. We also want to store some data associated with our Users on our backend to implement progression features like Player Levels and Unlockable Items. We also want to use this storage to keep track and make visible to Players their Gameplay Statistics and performance.

We decided to use the [Nakama Server](https://heroiclabs.com/nakama/) from Heroic Labs to help us implement this. Nakama handles Identity Authentication in a multitude of ways and provides a Storage interface powered by CockroachDB by default while still allowing us to configure and specialize them for our game.

# Planned Architecture
---
All of our Backend will run on a Kubernetes Cluster with backing Database storage, all provided by Google Cloud. We will deploy a Nakama Server instance in this cluster with a reserved static IP. This will be the entrypoint for Game Clients to connect to our network. This cluster will also have an instance of Agones running in it, which can then spin up new pods on-demand for our Dedicated Server processes handling individual matches.

The entire process, once fully implemented, will be as follows:
    - The Player (Client) connects to the Nakama Server instance to load Player Account information and requests to find a match
    - The Nakama Server finds a group of Players that are searching for a match and requests Agones for a Game Server
    - Agones spins up a new pod in the Kubernetes Cluster from Google Cloud with our Dedicated Server running on it
    - Agones passes the IP and port information for the new server to Nakama which passes it to the connected Players

While in a production environment, using a single static IP for the Nakama server and directly connecting the clients to our dedicated servers and revealing our IP addresses might be security concerns, we'll be ignoring this since this is a student project.

# Current Progress
---
As of right now, we've deployed simple Dedicated Server executables to Kubernetes clusters hosted on Google Cloud orchestrated by an Agones instance. The next step in this process is to deploy a Nakama Server instance and set things up so that it can communicate with Agones to spin up new Dedicated Server processes on demand.

On the Gameplay side, we're still waiting for the design to solidify further to start implementing features but we will be starting with basic Player and AI Controllers and Sample maps to help test Server load and get a better picture of our high-level architecture. Hopefully I'll have more interesting screenshots in the next blog post.
