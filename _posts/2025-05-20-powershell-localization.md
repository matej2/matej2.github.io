---
layout: post
title:  "Windows Powershell: Localization guide"
author: john
categories: [ windows, cli ]
#tags: [red, yellow]
image: assets/images/jumbotron.jpg
description: ""
featured: false
hidden: true
---

Windows enables us to tailor experience by customizing datetime format, region, locales and other content. One can do this using settings or control panel. However, changing config this way is often confusing as Windows updates user interface for settings. Alternatively, ther is also a way to change these settings using Powershell.

Below you can find example command for SI localization. In order to customize it, you will need [two letter code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2), [geographical location identifier](https://learn.microsoft.com/en-us/windows/win32/intl/table-of-geographical-locations). Optionally, you can also further customize datee / time and number formats. 

These commands were tested in Windows 11.

## Code

  
    # Set Slovenian locale for non-Unicode programs (system locale)
    Set-WinSystemLocale -SystemLocale sl-SI

    # Set Slovenian regional format (date, time, currency, etc.)
    Set-WinHomeLocation -GeoId 212  # Slovenia's GeoID is 212
    Set-Culture -CultureInfo sl-SI

    # Set Slovenian date/time formats for current user
    Set-WinUILanguageOverride -Language sl-SI
    Set-WinUserLanguageList sl-SI -Force

    # (optional) Set short date format to Slovenian standard (d.M.yyyy)
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sShortDate -Value "d.M.yyyy"
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sLongDate -Value "d. MMMM yyyy"

    # (optional) Set time format to 24-hour format (H:mm:ss)
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sTimeFormat -Value "H:mm:ss"

    # (optional) Set number format to Slovenian standard (decimal comma, thousand dot)
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sDecimal -Value ","
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sThousand -Value "."
    Set-ItemProperty -Path "HKCU:\Control Panel\International" -Name sList -Value ";"

    # Refresh the settings
    $null = [System.Globalization.CultureInfo]::CurrentCulture.ClearCachedData()

