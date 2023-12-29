# 🖼 Iframes

If you need to embed a site on which the widget is present through an `iframe`, you must take into account that there are security requirements to be met so that there are no conflicts in the use of the camera, microphone, full screen, GPS, etc.

## Attributes

The first thing you should consider is that you must add two mandatory attributes `allow` and `allowfullscreen`, otherwise the embedding will not work correctly.

```html
<iframe src="..." allow="camera;microphone" allowfullscreen="true"></iframe>
```

### Extra Permissions

If you require other permissions such as GPS, gyroscope, light sensor, etc., you must add them to the `allow` attribute based on the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Permissions\_Policy).

## Using Libraries

We also suggest you to avoid cross-domain problems using our open source library [iFrameX](https://github.com/videsk/iFrameX), which will allow you to create iframes without the need of a source different from the current one, injecting the JavaScript, CSS and HTML content dynamically.

{% embed url="https://github.com/videsk/iFrameX" %}