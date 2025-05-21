---
layout: post
title:  "CLI commands to remove Windows bloatware"
author: matej
categories: [ cli, windows ]
#tags: [red, yellow]
image: assets/images/jumbotron.jpg
description: "r"
featured: false
hidden: true
---

Troughout the history, Microsoft has been moving to a different approach with their products - freemium with 

Some of these settings can be configured in settings app, but some can only be set using terminal.

# Disable telemetry 

    sc config DiagTrack start= disabled
    sc config dmwappushservice start= disabled

# Remove Start Menu Ads

    reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v Start_IrisRecommendations /t REG_DWORD /d 0 /f

# Disable Lock Screen Ads