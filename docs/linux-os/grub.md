---
layout : default
parent : Linux OS
title  : Grub Bootloader
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

## Word of advise

- Always, always create backup of config file.
- Make sure you have bootable usb drive to fix if anything goes wrong.

To create backup of original setting file, run:
```
cp /etc/default/grub /etc/default/grub.orig
```

## Hide or edit timer on GRUB bootloader

1. Edit `/etc/default/grub` to these setting
    ```
    GRUB_TIMEOUT=0 
    # Change the number (in seconds) to shorten or prolong grub screen.
    ```
2. Then update grub bootloader
    ```
    sudo update-grub
    ```

## Boot to last-used OS

1. Edit `/etc/default/grub` to these setting
    ```
    GRUB_DEFAULT=saved
    GRUB_SAVEDEFAULT=true
    ```
2. Then update grub bootloader
    ```
    sudo update-grub
    ```

## Rename OS menuentry

Either way is fine, it depends on one's preference actually.<br>
However, do note that changing these setting will prevent `grub` to update `kernel`.<br>
If you want to update `kernel`, just give the file its execution right and run `sudo update-grub`.

### Easy way

1. Edit file `/boot/grub/grub.cfg`
    ```
    menuentry "Something" {
        set root=(hdX,Y)
        -- boot parameters --
    }
    ```
2. Change that `Something` to your desired name.
3. Do not run `sudo update-grub`. Otherwise `grub.cfg` will be regenerated to `grub-script` setting.

### A bit complicated way

1. Open file `/boot/grub/grub.cfg` and look for these headers.
    ```
    ### BEGIN /etc/grub.d/10_linux ###
        ***
        ***
    
    ### BEGIN /etc/grub.d/30_os-prober ###
        ***
        ***
    ```
2. Copy your desired menuentry and paste-append it to `/etc/grub.d/40_custom`.<br>
The `grub man` says to be sure to not leave empty line at the end of file. I haven't tried it, so I don't know what happen if we ignore the warning.
3. Then revoke executable right for these files.
    ```
    /etc/grub.d/10_linux
    /etc/grub.d/30_os-prober
    ```
4. And lastly, update grub to make changes.
    ```
    sudo update-grub
    ```
