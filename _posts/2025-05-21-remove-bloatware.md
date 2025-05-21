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

Disable Windows Telemetry (Basic level)

    Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection" -Name "AllowTelemetry" -Value 0 -Force

Disable Diagnostic Tracking Service (DiagTrack)

    Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\DiagTrack" -Name "Start" -Value 4 -Force

    Stop-Service -Name "DiagTrack" -Force
    Set-Service -Name "DiagTrack" -StartupType Disabled

# Remove Start Menu Ads

Disable Start Menu ads (recommendations)

    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name "Start_IrisRecommendations" -Value 0 -Force

# Disable Lock Screen Ads

Disable Lock Screen tips and ads

    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" -Name "RotatingLockScreenEnabled" -Value 0 -Force

    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" -Name "SubscribedContent-338387Enabled" -Value 0 -Force

# Disable Personalized Ads (PowerShell)
 Turn off ad tracking

    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\AdvertisingInfo" -Name "Enabled" -Value 0 -Force

# Disable Tailored Experiences (PowerShell)

Stop Microsoft from using your data for "tailored experiences"

    Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Privacy" -Name "TailoredExperiencesWithDiagnosticDataEnabled" -Value 0 -Force
    
# Disable Data Collection (PowerShell)

Disable data collection (Windows 10/11)

    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value 0 -Force

# Apply changes

Restart Explorer to apply Start Menu changes

    Stop-Process -Name "Explorer" -Force -ErrorAction SilentlyContinue