---
description: >-
  Below, we explain how to integrate Videsk Webhooks with PowerBI.
---

# Power BI

{% hint style="info" %}
If you are not familiar with how our Webhooks work, we suggest reading our [introduction](../introduccion.md).
{% endhint %}

{% hint style="warning" %}
Currently, it is only possible to connect Videsk with Power BI in its Pro version, which can be professional or educational.
{% endhint %}

{% hint style="warning" %}
You must have authorization to add data sets to your PowerBI account.
{% endhint %}

{% hint style="success" %}
This tutorial is based on the **web version of PowerBI**.
{% endhint %}

## 1. Create Data Set

To make the connection, we will use the Power BI API called [Real-time streaming](https://docs.microsoft.com/es-es/power-bi/connect-data/service-real-time-streaming).

You should go to the side menu, select **Browse > Recent**, and then select the workspace you want to add the data set to.

![](<../../.gitbook/assets/image (12) (1).png>)

Then in your workspace, you should click New and select the **Streaming dataset** option.

![](<../../.gitbook/assets/image (17).png>)

Subsequently, a right side menu will be displayed, where you should select the **API** option and click on the next button located at the bottom.

![](<../../.gitbook/assets/image (45).png>)

Next, it will show you a form which we must fill out with the data we need to export. Enter a reference name which can be whatever you want.

![](<../../.gitbook/assets/image (30).png>)

## 2. Data Model

To load data automatically in PowerBI, it is necessary to indicate which data will be stored in this set.

To do this, leave PowerBI open for a few minutes, open a new tab, and access your dashboard account ([click here](https://app.videsk.io)), then select **Webhooks** from the menu.

![](<../../.gitbook/assets/image (63).png>)

In Webhooks, you should click on the blue button ![](<../../.gitbook/assets/image (26) (1).png>)located at the top right. Subsequently, you should select the **Custom** option.

![](<../../.gitbook/assets/image (40).png>)

Then, you should select what type of event you want to send to PowerBI.

{% hint style="info" %}
**For this example, we will use the data from the created call event,** but remember that the instructions apply to any other event.
{% endhint %}

![](<../../.gitbook/assets/image (35).png>)

After clicking on the event, you will enter the Webhook editor.



In the editor, go to the right sidebar; at the top, you will find a tab called **Example data**. There you can find an example of the event data, which in this case is from a call.

{% hint style="info" %}
The data you see are completely random and not associated with your clients or business.
{% endhint %}

![](<../../.gitbook/assets/image (19).png>)

{% hint style="info" %}
We suggest making a list of the data you want to load into PowerBI.
{% endhint %}

For this example, we will use data such as **agent name, segment, time in queue, start date, duration, and country**.

## 3. Model in PowerBI

The next step is to define the data model to load in PowerBI, so we must return to the tab where PowerBI is open.

In the form, you will see the **Streaming values** section; this is where we will define the field names. For this example, we will define the following structure:

| Value Name      | Value Type    |
| --------------- | ------------- |
| Agent           | Text          |
| Segment         | Text          |
| Time in queue   | Number        |
| Start date      | DateTime      |
| Duration        | Number        |
| Country         | Text          |

You should get a streaming values structure similar to this:

```json
[
  {
    "Agent" :"AAAAA555555",
    "Segment" :"AAAAA555555",
    "Time in queue" :98.6,
    "Start date" :"2022-07-07T01:59:39.724Z",
    "Duration" :98.6,
    "Country" :"AAAAA555555"
  }
]
```

![](<../../.gitbook/assets/image (14).png>)

{% hint style="warning" %}
Value names are sensitive to uppercase, lowercase, spaces, special characters, etc.
{% endhint %}

{% hint style="info" %}
Remember to correctly select the value type; otherwise, the data may not be used for calculations.
{% endhint %}

You must activate the **Historical data analysis** option. This allows storing the data we send, creating a data history.

![](<../../.gitbook/assets/image (2) (1).png>)

To finish, click on the **Create** button. Subsequently, it will show us integration data that we will use in Videsk.

## 4. Model in Videsk

Now with the integration data provided by PowerBI, we will go to the Webhooks settings in Videsk.

* Copy the PowerBI insertion URL, and paste it into the Method and URL field.

![](<../../.gitbook/assets/image (34).png>)

![](<../../.gitbook/assets/image (11).png>)

* Copy the **Raw** content from PowerBI and paste it into the Webhook code editor at the end of the editor.

![](<../../.gitbook/assets/image (39).png>)

![](<../../.gitbook/assets/image (8) (1).png>)

Now the last and most important step corresponds to extracting the dynamic data using our markup language.

{% hint style="info" %}
This process is known as ETL, being a function incorporated in Videsk which allows reducing technological work, costs, and maintenance.
{% endhint %}

## 5. Assign Data to Values

Now we only need to assign the data to the values in the structure we obtained from PowerBI, which is called JSON.

For this, we will use the markup language `{{}}`in this way you can assign the data.

{% hint style="info" %}
In this example, we are only using 6 types of data, but you can extract more than 30 from a call.
{% endhint %}



| Value           | Data                                     |
| --------------- | ---------------------------------------- |
| Agent           | `"{{agent.firstname}}{{agent.lastname}}"`|
| Segment         | `{{parser segment.name}}`                |
| Time in queue   | `{{parser queue.duration}}`              |
| Start date      | `{{parser startedAt}}`                   |
| Duration        | `{{parser duration}}`                    |
| Country         | `{{parser extraData.countryName}}`       |

{% hint style="info" %}
In this case, we used `"{{agent.firstname}} {{agent.lastname}}"` in  quotes because it is a composite data. When it's a simple structure, we suggest using the [parser](../helpers/parser.md) helper.
{% endhint %}

![](<../../.gitbook/assets/image (10).png>)

```javascript
[
  {
    "Agent": "{{agent.firstname}} {{agent.lastname}}",
    "Segment": {{parser segment.name}},
"Time in queue": {{parser queue.duration}},
"Start date": {{parser startedAt}},
"Duration": {{parser duration}},
"Country": {{parser extraData.countryName}}
}
]
```

Once the structure is ready, you can see in the viewer (text in green) the live changes and what the data output would look like.

Ensuring that the structure resembles what PowerBI expects to receive, the only thing left would be to assign a name to this Webhook which is only so your team can differentiate between multiple Webhooks.

![](<../../.gitbook/assets/image (36).png>)

Don't forget to click on **Save**.

![](<../../.gitbook/assets/image (61).png>)

Done! Your Videsk account is now integrated with PowerBI. You can now make calls, and they will load in real time! :tada:

{% hint style="info" %}
Remember to assign the data set created to a new or existing report.
{% endhint %}

![Example of a report in PowerBI with data sent via Webhooks](<../../.gitbook/assets/image (48).png>)

## Example webhook

```javascript
[
  {
    "segment": {{parser segment.name}},
"agent": "{{agent.firstname}} {{agent.lastname}}",
  "start_date" : {{parser startedAt}},
"end_date": {{parser endedAt}},
"customer_hangs_up": {{parser customerLeave}},
"comment": {{parser comment.text}},
"agent_form": {{parser agentForm}},
"customer_form": {{parser baseForm}},
"operating_system_name": {{parser extraData.osName}},
"operating_system_version": {{parser extraData.osVersion}},
"browser_name": {{parser extraData.browserName}},
"browser_version": {{parser extraData.browserVersion}},
"device": {{parser extraData.deviceType}},
"website": {{parser extraData.referrer}},
"timezone": {{parser extraData.timezone}},
"language": {{parser extraData.langName}},
"region": {{parser extraData.regionName}},
"city": {{parser extraData.cityName}},
"latitude": {{parser extraData.coordinates.[0]}},
"longitude": {{parser extraData.coordinates.[1]}},
"duration": {{parser duration}},
"id" :{{parser id}},
"acw_duration": {{parser acwDuration}},
"effective_duration": {{parser effectiveDuration}},
"day": {{#date startedAt}}{ "day": "numeric" }{{/date}},
  "month": {{#date startedAt}}{ "month": "numeric" }{{/date}},
    "year": {{#date startedAt}}{ "year": "numeric" }{{/date}}
    }
    ]
```
