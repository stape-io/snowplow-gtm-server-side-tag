# Snowplow Tag for Google Tag Manager Server-side

[![early-release]][tracker-classification]
[![License][license-image]][license]
[![Release][release-image]][releases]

Snowplow is a scalable open-source platform for rich, high quality, low-latency data collection. It is designed to collect high quality, complete behavioral data for enterprise business.

**To find out more, please check out the [Snowplow website][website] and our [documentation][docs].**

## Overview

The Snowplow Tag for [Google Tag Manager Server-side][gtm-ss] is a server-side tag for forwarding events to a Snowplow collector, from the [Snowplow Google Tag Manager Server-side Client][snowplow-gtm-server-side-client] or other clients which populate the common event model.

## Events

When the Snowplow Tag is triggered, it receives the client event.

If the event is a Snowplow event collected and forwarded by the [Snowplow GTM Server-side client][snowplow-gtm-server-side-client], it forwards it to the Snowplow collector. For other client events, the Snowplow Tag will transform them to Snowplow events before sending them to the Snowplow collector.

By default, the Snowplow tag will tranform the following client events into self-describing Snowplow events:

1. The Google Tag Manager [Server-side events][gtm-ss-events].
2. The GA4 [enhanced-measurement events][ga4-enhanced-measurement-events].
3. The GA4 [automatically collected events][ga4-auto-events] for the web.

In addition, users can change the default or add custom event definitions according to their use case.

## Installation

### Installing from the Google Tag Manager Template Gallery

Coming Soon

### Manual Installation

To manually install this Tag:

1. Download `template.tpl`
2. Create a new Tag Template in the Templates section of a Google Tag Manager Server container
3. Click the More Actions menu in the Template editor and select Import
4. Import `template.tpl` downloaded in Step 1
5. Click Save.

Then, create a new Tag using the template just created.

## Configuration

In order to use the Snowplow Tag, you need to specify your Snowplow collector URL in the Tag Configuration.

Other available settings are:

### 1. Cookie Settings

Through the Cookie Settings you can configure the cookie name returned by your Snowplow collector or further override the collector cookie with your own settings. More specifically, besides the cookie name, the cookie attributes you can configure are:

- Domain
- Path
- SameSite
- Expiration
- HttpOnly
- Secure

### 2. Advanced Event Settings

Through the Advanced Event Settings, you can control and customize the Snowplow Tag's behaviour concerning client events' tranformations. More specifically, you can:

1. Add your custom event definitions for selected events to be sent as self-describing Snowplow events.

    After you enable this option, you can specify the event name, the event schema, and the event data mappings, that the Snowplow Tag will use to transform a client event into a Snowplow one. Self-describing events are a [data structure based on JSON Schemas][snowplow-self-desc-docs] and can have arbitrarily many fields. To define your own custom event, you must first create a JSON schema for that event and upload it to an Iglu Schema Repository, since Snowplow uses the schema to validate the event. Then:

    1. use the `Event Name to Schema` table to map that schema for a given client event name.
    2. use the `Event Definitions` table to define how each Snowplow data property maps to the client event.

2. Send selected events as structured Snowplow events.

    After you enable this option, just add the event names you want to be tranformed into structured Snowplow events. This option is better suited towards events that follow the category-action-label-value taxonomy. The Snowplow Tag will specifically look for the corresponding `event_category`(required), `event_action`, `event_label` and `event_value` properties in the [server-side event object][gtm-ss-event].

3. Set whether Base64 will be used to encode self-describing data

## Find out more

| Technical Docs                    | Setup Guide                 |
|-----------------------------------|-----------------------------|
| [![i1][techdocs-image]][techdocs] | [![i2][setup-image]][setup] |
| [Technical Docs][techdocs]        | [Setup Guide][setup]        |

## Contributing

Feedback and contributions are welcome - if you have identified a bug, please log an issue on this repo. For all other feedback, discussion or questions please open a thread on our [discourse forum][discourse].

| Contributing                              |
|-------------------------------------------|
| [![i3][contributing-image]][contributing] |
| [Contributing][contributing]              |

## Copyright and license

Snowplow Tag for Google Tag Manager Server-side is copyright 2021 Snowplow Analytics Ltd.

Licensed under the **[Apache License, Version 2.0][license]** (the "License");
you may not use this software except in compliance with the License.

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

[tracker-classification]: https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/tracker-maintenance-classification/
[early-release]: https://img.shields.io/static/v1?style=flat&label=Snowplow&message=Early%20Release&color=014477&labelColor=9ba0aa&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAeFBMVEVMaXGXANeYANeXANZbAJmXANeUANSQAM+XANeMAMpaAJhZAJeZANiXANaXANaOAM2WANVnAKWXANZ9ALtmAKVaAJmXANZaAJlXAJZdAJxaAJlZAJdbAJlbAJmQAM+UANKZANhhAJ+EAL+BAL9oAKZnAKVjAKF1ALNBd8J1AAAAKHRSTlMAa1hWXyteBTQJIEwRgUh2JjJon21wcBgNfmc+JlOBQjwezWF2l5dXzkW3/wAAAHpJREFUeNokhQOCA1EAxTL85hi7dXv/E5YPCYBq5DeN4pcqV1XbtW/xTVMIMAZE0cBHEaZhBmIQwCFofeprPUHqjmD/+7peztd62dWQRkvrQayXkn01f/gWp2CrxfjY7rcZ5V7DEMDQgmEozFpZqLUYDsNwOqbnMLwPAJEwCopZxKttAAAAAElFTkSuQmCC

[license]: https://www.apache.org/licenses/LICENSE-2.0
[license-image]: https://img.shields.io/badge/license-Apache--2-blue.svg?style=flat

[releases]: https://github.com/snowplow/snowplow-gtm-server-side-tag/releases
[release-image]: https://img.shields.io/github/v/release/snowplow/snowplow-gtm-server-side-tag

[website]: https://snowplowanalytics.com
[docs]: https://docs.snowplowanalytics.com
[snowplow]: https://github.com/snowplow/snowplow
[discourse]: https://discourse.snowplowanalytics.com

[techdocs]: https://docs.snowplowanalytics.com/docs/forwarding-events-to-destinations/forwarding-events/google-tag-manager-server-side/snowplow-tag-for-gtm-ss/snowplow-tag-configuration/
[techdocs-image]: https://d3i6fms1cm1j0i.cloudfront.net/github/images/techdocs.png
[setup]: https://docs.snowplowanalytics.com/docs/forwarding-events-to-destinations/forwarding-events/google-tag-manager-server-side/snowplow-tag-for-gtm-ss/
[setup-image]: https://d3i6fms1cm1j0i.cloudfront.net/github/images/setup.png

[contributing]: https://github.com/snowplow/snowplow-gtm-server-side-tag/blob/master/CONTRIBUTING.md
[contributing-image]: https://d3i6fms1cm1j0i.cloudfront.net/github/images/contributing.png

[snowplow-gtm-server-side-client]: https://github.com/snowplow/snowplow-gtm-server-side-client
[gtm-ss]: https://developers.google.com/tag-manager/serverside
[gtm-ss-event]: https://developers.google.com/tag-manager/serverside/intro#events
[gtm-ss-events]: https://developers.google.com/tag-manager/serverside/events
[ga4-enhanced-measurement-events]: https://support.google.com/analytics/answer/9216061?hl=en
[ga4-auto-events]: https://support.google.com/analytics/answer/9234069?hl=en&ref_topic=9756175
[snowplow-self-desc-docs]: https://docs.snowplowanalytics.com/docs/understanding-tracking-design/understanding-schemas-and-validation/
