---
description: >-
  Next, we will explain the best way to debug errors whether using our SDKs or APIs.
---

# Devtools

This guide will help you identify errors that may arise while using any of our products, whether these are legitimate implementation errors or browser incompatibilities.

{% hint style="success" %}
In general, our products try to be as descriptive as possible and mostly have the ability to handle errors and report them to our systems.
{% endhint %}

The first thing you should know as the best browser tool for debugging either in development or production stage is **Devtools** or **Element Inspector**.



## How to access Devtools?

There are several ways to access it, depending on the browser:

| Browser            | Shortcut                                              | Through Menu                                                                                            |
| ------------------ | ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Chrome/Edge/Firefox| <ul><li>Ctrl + Shift + i</li></ul><ul><li>F12</li></ul>| Right-click + Inspect                                                                                   |
| Safari             | Option + ⌘ + C                                        | Safari > Preferences > Advanced, and select the option “Show Develop menu in menu bar”                  |

{% hint style="info" %}
**You can right-click anywhere on the website.**
{% endhint %}

![Right-click context menu on the site](<../.gitbook/assets/image (66).png>)

{% hint style="info" %}
If we have asked you to keep Devtools open for errors that our monitoring systems have not been able to capture, read on.
{% endhint %}

If you need to capture information about code errors, network, etc., we suggest resizing the Devtools window so it does not interfere with the interface, or use the option to undock it in a separate window.

### Docked View

![Docked view](<../.gitbook/assets/image (27).png>)

### Undocked View

To access the undocked view, click on the three dots ![](<../.gitbook/assets/image (53).png>) located in the upper right corner, and then select the icon ![](<../.gitbook/assets/image (58).png>).

After this, the window will be completely undocked and you can minimize it.

![View as an undocked window](<../.gitbook/assets/image (57) (1).png>)

## Visualizing Errors

The best way to get the errors is by clicking on the **Console** tab, located in the upper left part. Then you will see the list of potential errors that have occurred during the session.

{% hint style="info" %}
If our technical team has asked you to open Devtools or Element Inspector, go to the error log export section.
{% endhint %}

![Console view with errors and warnings](<../.gitbook/assets/image (54).png>)

There are messages with different background colors, the most common being red and yellow, representing errors and warnings, respectively.

Mostly, warning messages are not relevant, while red messages are errors which need attention. In the previous image, most of the visible errors are resource blocking by ad blocker extensions, but when something is wrong you will see more extensive messages with information in English about what has happened.

## Exporting Logs

It is likely that our technical team will ask you to download the error logs that have occurred during the session of a tab, because sometimes certain errors are not recorded by our systems, like network, firewall, etc.

For this, you should be in the [Console view](devtools.md#visualizing-errors) and then right-click anywhere in the console (Console), finally click on the **`Save as...`** option.

![Context menu when right-clicking in console](<../.gitbook/assets/image (67).png>)

The file you download should be sent to [support@videsk.io](mailto:support@videsk.io), with the subject **Error Logs**, attaching the file with logs usually called **{website}-{date}.log**.

[Click here to automatically create an email](mailto:support@videsk.io?subject=Error%20Logs\&body=Company:%20XXXXX,%20User:%20XXXX).
