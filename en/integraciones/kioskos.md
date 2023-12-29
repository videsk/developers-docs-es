---
description: Discover how to integrate with physical kiosks
---

# Kiosks

## Kiosk Mode in Chrome

Activating Google Chrome's kiosk mode will prevent users from minimizing or closing the browser.

{% hint style="info" %}
The following commands work in any Chromium-based browser like Chrome, Edge, Opera, Brave, etc.
{% endhint %}

The following command is an example that contains arguments such as:

* `--kiosk`, will open Chrome with limited interaction features
* `--fullscreen`, will open Chrome in full screen
* `-tab`, will indicate which website to open

{% code title="Example" %}
```
[path or chrome command] --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

{% hint style="warning" %}
Remember to replace `https://example.com` with the URL of the site where the integration is located.
{% endhint %}

{% hint style="danger" %}
Do not include links to external sites, as they will open in another tab making it difficult to return to the original site.
{% endhint %}

### Windows

```
start chrome.exe --kiosk --fullscreen -tab https://example.com
```

#### Run at Windows Startup (Optional)

If you want Chrome to open every time Windows starts, you should add this file as follows:

1. Open the Windows menu and open "Run" or press the Windows + R keys.
2. Type `Shell:startup`.
3. Download this file to the opened folder:

{% file src="../.gitbook/assets/kiosk.cmd" %}

{% hint style="info" %}
If you can't download the file due to network security blocks, open a notepad, paste the following content, and save it as `kiosk.cmd`.



**Make sure to save with the "All Files" extension, not as `.txt`**
{% endhint %}

{% code title="Content of .CMD file" %}
```batch
@echo off
start chrome --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

4\. Open the file with notepad, change the URL to your website, and save the changes.

5\. Done! Restart Windows and Chrome will automatically open at startup.

{% hint style="info" %}
To eliminate automatic opening, you will need to delete the file from the startup folder.
{% endhint %}

### Linux

```
google-chrome --kiosk --fullscreen -tab https://example.com
```

#### Run at Linux Startup (Optional)

If you want Chrome to open every time Linux starts, you should add this file as follows:

1. Download this file to any location

{% file src="../.gitbook/assets/kiosk.service" %}

{% hint style="info" %}
If you can't download the file due to network security blocks, copy the following content and paste it into a file called `kiosk.service`
{% endhint %}

{% code title="Content of .service file" %}
```bash
[Unit]
Description=Open Google Chrome after reboot

[Service]
Type=simple
ExecStart=/bin/bash google-chrome --kiosk --fullscreen -tab https://example.com
```
{% endcode %}

2\. Open the terminal with the key combination <mark style="background-color:blue;">Ctrl</mark> + <mark style="background-color:blue;">Alt</mark> + <mark style="background-color:blue;">T</mark>&#x20;

3\. Execute the following commands, one after the other:

```
$ cd /etc/systemd/system
$ sudo mv /{REPLACE_DOWNLOAD_FILEPATH} ./
$ sudo chmod 644 ./kiosk.service
$ sudo service enable kiosk.service
```

4\. Done! Now when Linux restarts, Google Chrome will automatically open.

{% hint style="info" %}
If you want more details on other available arguments to open Google Chrome or Chromium-based browsers, go to [this link](https://peter.sh/experiments/chromium-command-line-switches/).
{% endhint %}