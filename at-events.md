---

copyright:
  years: 2020, 2025
lastupdated: "2025-02-05"

keywords: IBM,activity tracker,event,security,text to speech

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Activity Tracking events for {{site.data.keyword.texttospeechshort}}
{: #at-events}

[IBM Cloud]{: tag-ibm-cloud}

As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with {{site.data.keyword.texttospeechfull}} in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the tutorial [Getting started with {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

## Locations where activity tracking events are generated
{: #at-locations}

### Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}

{{site.data.keyword.texttospeechfull}} in {{site.data.keyword.cloud}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

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

## Tune by Example events
{: #at-events-tbe}

The following tables list the {{site.data.keyword.texttospeechshort}} actions for the Tune by Example feature that generate events.

### Create events
{: #at-events-tbe-create}

| Action | Description |
|--------|-------------|
| `text-to-speech.speaker.create` | Create a speaker (`POST /v1/speakers/{speaker_name}`). |
| `text-to-speech.custom-model-prompt.create` | Create a prompt for a custom model (`POST /v1/customizations/{customization_id}/prompts/{prompt_id}`). |
{: caption="Tune by Example .create actions that generate events"}

### Read events
{: #at-events-tbe-read}

| Action | Description |
|--------|-------------|
| `text-to-speech.speaker-list.read` | Read a list of speakers (`GET /v1/speakers`). |
| `text-to-speech.speaker-prompt-list.read` | Read a list of prompts for a speaker (`GET /v1/speakers/{speaker_id}`). |
| `text-to-speech.custom-model-prompt-list.read` | Read a list of prompts for a custom model (`GET /v1/customizations/{customization_id}/prompts`). |
| `text-to-speech.custom-model-prompt.read` | Read a prompt for a custom model (`GET /v1/customizations/{customization_id}/prompts/{prompt_id}`). |
{: caption="Tune by Example .read actions that generate events"}

### Delete events
{: #at-events-tbe-delete}

| Action | Description |
|--------|-------------|
| `text-to-speech.speaker.delete` | Delete a speaker (`DELETE /v1/speakers/{speaker_id}`). |
| `text-to-speech.custom-model-prompt.delete` | Delete a prompt from a custom model (`DELETE /v1/customizations/{customization_id}/prompts/{prompt_id}`). |
{: caption="Tune by Example .delete actions that generate events"}

## GDPR event
{: #at-events-gdpr}

The following table lists the {{site.data.keyword.texttospeechshort}} action for General Data Protection Regulation (GDPR) that generates an event.

| Action | Description |
|--------|-------------|
| `text-to-speech.gdpr-user-data.delete` | Delete information for a user (`DELETE /v1/user_data`). |
{: caption="GDPR .delete action that generates an event"}

## Where to view events
{: #at-ui}

Events that are generated by an instance of the {{site.data.keyword.texttospeechshort}} service are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web user interface (UI) of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Navigating to the UI](/docs/activity-tracker?topic=activity-tracker-launch).
