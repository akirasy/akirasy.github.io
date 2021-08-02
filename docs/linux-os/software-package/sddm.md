---
layout : default
grand_parent : Linux OS
parent : Software & Packages
title  : SDDM
---

# {{ page.title }}
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Simple Desktop Display Manager

## Enable autologin in [SDDM](https://packages.debian.org/stable/sddm)

1. Generate current `sddm.conf` file.
    ```
    sddm --example-config > sddm.conf
    mkdir -p /usr/lib/sddm/sddm.conf.d/
    mv sddm.conf /usr/lib/sddm/sddm.conf.d/
    ```
2. Open the newly generated file. Keep other settings as is and only change these parameters accordingly.
    ```
    [Autologin]
    # Whether sddm should automatically log back into sessions when they exit
    Relogin=true
    
    # Name of session file for autologin session (if empty try last logged in)
    Session=
    
    # Username for autologin session
    User={username}
    ```
