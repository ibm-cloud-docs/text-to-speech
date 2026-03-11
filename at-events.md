---

copyright:
  years: 2020, 2026
lastupdated: "2026-03-06"

keywords: IBM,activity tracker,event,security,text to speech

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Activity Tracking events for {{site.data.keyword.texttospeechshort}}
{: #at_events}

[IBM Cloud]{: tag-ibm-cloud}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.texttospeechshort}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

## Locations where activity tracking events are generated
{: #at-locations}

### Locations where activity tracking events are sent to {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}

{{site.data.keyword.texttospeechfull}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (us-south)            | Washington (us-east)                         | Toronto (ca-tor)      | Sao Paulo (br-sao) |
|-------------------|-------------------------------------|------------------------------------|------------------------------------|
| [Yes]{: tag-green}           | [Yes]{: tag-green}   | [No]{: tag-red} | [No]{: tag-red}|                                                  |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1} 
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"} 
{: row-headers}

| Tokyo (jp-tok)           | Sydney (au-syd)                    |  Osaka (jp-osa)     | Chennai (in-che) |
|-------------------|-------------------------------------|------------------------------------|------------------------------------|
| [Yes]{: tag-green}           | [Yes]{: tag-green}   | [No]{: tag-red} | [No]{: tag-red}|                                                  |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"} 
{: #at-table-2} 
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (eu-de)        | London (eu-gb)                 |  Madrid (eu-es)    | 
|-------------------|-------------------------------------|------------------------------------|
| [Yes]{: tag-green}       | [Yes]{: tag-green}   | [No]{: tag-red} |                              |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}  
{: tab-title="Europe"}
{: tab-group="at"} 
{: class="simple-tab-table"} 
{: row-headers}

## Viewing activity tracking events for {{site.data.keyword.texttospeechshort}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch).

## Customization events
{: #at-events-custom}

The following tables list the {{site.data.keyword.texttospeechshort}} actions for model customization that generate events.

The names of the actions for the customization events have changed. The old names are deprecated. Use the names in the following tables instead. For more information, see [Updates to Activity Tracker actions for customization](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-12april2021) in the release notes for {{site.data.keyword.cloud_notm}}.
{: note}

### Create events
{: #at-events-custom-create}

| Action | Description |
|--------|-------------|
| `text-to-speech.custom-model.create` | Create a custom model (`POST /v1/customizations`).                                           |
| `text-to-speech.custom-model-word-list.create` | Create a word list for a custom model (`POST /v1/customizations/{customization_id}/words`).  |
| `text-to-speech.custom-model-word.create` | Create a word for a custom model (`PUT /v1/customizations/{customization_id}/words/{word}`). |
{: caption="Customization .create actions that generate events"}

### Read events
{: #at-events-custom-read}

| Action | Description |
|--------|-------------|
| `text-to-speech.custom-model-list.read` | Read a list of custom models created by a user (`GET /v1/customizations`).                 |
| `text-to-speech.custom-model.read` | Read a custom model (`GET /v1/customizations/{customization_id}`).                         |
| `text-to-speech.custom-model-word-list.read` | Read a word list for a custom model (`GET /v1/customizations/{customization_id}/words`). |
| `text-to-speech.custom-model-word.read` | Read a word for a custom model (`GET /v1/customizations/{customization_id}/words/{word}`). |
{: caption="Customization .read actions that generate events"}

### Update event
{: #at-events-custom-update}

| Action | Description |
|--------|-------------|
| `text-to-speech.custom-model.update` | Update a custom model (`POST /v1/customizations/{customization_id}`). |
{: caption="Customization .update action that generates an event"}

### Delete events
{: #at-events-custom-delete}

| Action | Description |
|--------|-------------|
| `text-to-speech.custom-model.delete` | Delete a custom model (`DELETE /v1/customizations/{customization_id}`).                          |
| `text-to-speech.custom-model-word.delete` | Delete a word from a custom model (`DELETE /v1/customizations/{customization_id}/words/{word}`). |
{: caption="Customization .delete actions that generate events"}

## GDPR event
{: #at-events-gdpr}

The following table lists the {{site.data.keyword.texttospeechshort}} action for General Data Protection Regulation (GDPR) that generates an event.

| Action | Description |
|--------|-------------|
| `text-to-speech.gdpr-user-data.delete` | Delete information for a user (`DELETE /v1/user_data`). |
{: caption="GDPR .delete action that generates an event"}
