# Settings

Our widget has a configuration or a setting that contains components like header colors, body, buttons, and texts. Each of these components can be configured separately.

By default, the widget setting that you have configured in your account is fetched using our API.

{% hint style="info" %}
Remember that this feature allows you to overwrite the settings and designs that you have configured from your account.
{% endhint %}

But it is also possible to force your own setting by adding a bit of code to your website. To do this you must take into account that the structure is as follows:

```json
{
"logo": {
"url": "...",
"height": 180
},
"colors": {
"background": "rgb(255,255, 255, 1)",
"font": "rgb(255,255, 255, 1)",
"gradient": "linear-gradient(to right, rgb(23, 54, 189) 0%, rgb(0, 99, 255) 100%)"
},
"texts": {
"title": "My title",
"subtitle": "My subtitle.",
"segmentsTitle": "Segment title",
"segmentsSubtitle": "Segment subtitle."
},
"settings": { "defaultChannel": "video" },
"orgName": "Company Name",
"services": ["on-demand"]
}
```

This structure allows you to modify logos, colors, texts, settings, and services to be made visible.

{% hint style="warning" %}
Read below before modifying the structure of the setting.
{% endhint %}

### Logo

* `url` you need to place a valid URL of your logo.
* `height` you need to enter the size of the logo as a number (without units)

### Colors

{% hint style="info" %}
It is possible in HEX, HSL, but it is not recommended.
{% endhint %}

* `background` you need to enter a color in RGB format.
* `font` you need to enter a color in RGB format.
* `gradient` you need to enter a gradient in RGB format or a single RGB color.

### Texts

{% hint style="info" %}
If you want to hide a title or subtitle, you can simply leave it blank, i.e., **`""`**.
{% endhint %}

* `title` you need to enter the title of the header of the widget.
* `subtitle` you need to enter the subtitle of the header of the widget.
* `segmentTitle` you need to enter the title that will be above the list of segments.
* `segmentSubtitle` you need to enter the subtitle that will be above the list of segments.

### Settings

* `defaultChannel` allows you to select the default value between `video` or `audio`.

{% hint style="info" %}
This option will only set a default option (microphone or camera), but your client will still be able to choose the one they want.
{% endhint %}

### OrgName

Enter the name of your business in this field.

### Services

You will need to choose which types of services are active for your widget, either between `on-demand` which represents your segments and `schedule` for calendars. You can choose between one or the other.

{% hint style="danger" %}
**Do not add a service to the list if you do not have at least 1 segment or active calendar in your account.**

The behavior of the widget could be unexpected.
{% endhint %}

## Apply styles

Once you have modified the parameters of the widget you will need to apply this change by adding some code to your website.

{% hint style="info" %}
The technique to use below can be applied from Devtools in your browser to preview the design before applying it to your site.
{% endhint %}

```javascript
const widgetStyle = {...};
window.localStorage.setItem('widget-custom-style', JSON.stringify(widgetStyle));
```

`widgetStyle` corresponds to the parameters previously configured. If you get a `parsing` error verify that you have written correctly in `JSON` format or as an object.

{% hint style="info" %}
Refresh your site and you will see the changes.
{% endhint %}

{% hint style="warning" %}
Do not modify the key name `widget-custom-style`, this is how we identify the custom parameters.
{% endhint %}

## Example

{% embed url="https://codesandbox.io/s/widget-settings-docs-pgebyg?file=/main.js" %}