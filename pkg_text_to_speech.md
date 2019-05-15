---

copyright:
  years: 2017, 2019
lastupdated: "2019-05-15"

keywords: text to speech, watson, cognitive, functions, packages

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}



# Text to Speech
{: #pkg_text_to_speech}

This pre-installed package is not available in the Tokyo region. Please see the installable [Text to Speech](/docs/openwhisk?topic=cloud-functions-text-to-speech-package) package using IAM authentication.
{: tip}

The `/whisk.system/watson-textToSpeech` package offers a convenient way to call Watson APIs to convert the text into speech.
{: shortdesc}

The package includes the following actions.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | package | username, password | Package to convert text into speech |
| `/whisk.system/watson-textToSpeech/textToSpeech` | action | payload, voice, accept, encoding, username, password | Convert text into audio |

**Note**: The package `/whisk.system/watson` is deprecated including the action `/whisk.system/watson/textToSpeech`. See the [installable {{site.data.keyword.texttospeechshort}} package](/docs/openwhisk?topic=cloud-functions-text-to-speech-package) instead.

## Setting up the Watson Text to Speech package in {{site.data.keyword.Bluemix_notm}}

If you're using {{site.data.keyword.openwhisk}} from {{site.data.keyword.Bluemix_notm}}, the package bindings are automatically created for your {{site.data.keyword.Bluemix_notm}} Watson service instances.

1. Create a Watson Text to Speech service instance in your {{site.data.keyword.Bluemix_notm}} [dashboard](http://cloud.ibm.com).

  Be sure to remember the name of the service instance and the {{site.data.keyword.Bluemix_notm}} organization and space you're in.

2. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Watson service instance that you created.
  ```
  ibmcloud fn package refresh
  ```
  {: pre}

  Example output:
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  List packages to see that the package binding was created:
  ```
  ibmcloud fn package list
  ```
  {: pre}

  Example output:
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}

## Setting up a Watson Text to Speech package outside {{site.data.keyword.Bluemix_notm}}

If you're not using {{site.data.keyword.openwhisk_short}} in {{site.data.keyword.Bluemix_notm}} or if you want to set up your Watson Text to Speech outside of {{site.data.keyword.Bluemix_notm}}, you must manually create a package binding for your Watson Text to Speech service. You need the Watson Text to Speech service user name, and password.

Create a package binding that is configured for your Watson Speech to Text service.
```
ibmcloud fn package bind /whisk.system/watson-textToSpeech myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
```
{: pre}

## Converting some text to speech

The `/whisk.system/watson-textToSpeech/textToSpeech` action converts some text into an audio speech. The parameters are as follows:

- `username`: The Watson API user name.
- `password`: The Watson API password.
- `payload`: The text to convert into speech.
- `voice`: The voice of the speaker.
- `accept`: The format of the speech file.
- `encoding`: The encoding of the speech binary data.

Invoke the **textToSpeech** action in your package binding to convert the text.
```
ibmcloud fn action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
```
{: pre}

Example output:
```
{
  "payload": "<base64 encoding of a .wav file>"
}
```
{: screen}


# {{site.data.keyword.texttospeechshort}} package

The installable {{site.data.keyword.texttospeechfull}} service provides an API that uses IBM's speech-synthesis capabilities to synthesize text into natural-sounding speech in a variety of languages, dialects, and voices.
{:shortdesc}

The service supports at least one male or female voice, sometimes both, for each language. The audio is streamed back to the client with minimal delay. For more information about the service, see the [IBM Cloud documentation](/docs/services/text-to-speech?topic=text-to-speech-about).

The {{site.data.keyword.texttospeechshort}} package contains the following entities. You can find additional details in the {{site.data.keyword.texttospeechshort}} API reference by clicking the entity name.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| [`text-to-speech-v1`](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html) | package | username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,  | Work with the {{site.data.keyword.texttospeechshort}} service. |
| [get-voice](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#get-voice) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    voice,     customization_id,  | Get a voice. |
| [list-voices](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#list-voices) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url, | List voices. |
| [synthesize](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#synthesize) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,   text,     accept,     voice,     customization_id,  | Synthesize audio. |
| [get-pronunciation](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#get-pronunciation) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    text,     voice,     format,     customization_id,  | Get pronunciation. |
| [create-voice-model](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#create-voice-model) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,   name, language, description,  | Create a custom model. |
| [delete-voice-model](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#delete-voice-model) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,  | Delete a custom model. |
| [get-voice-model](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#get-voice-model) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,  | Get a custom model. |
| [list-voice-models](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#list-voice-models) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    language,  | List custom models. |
| [update-voice-model](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#update-voice-model) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,    name, description, words,  | Update a custom model. |
| [add-word](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#add-word) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,     word,    translation, part_of_speech,  | Add a custom word. |
| [add-words](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#add-words) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,    words,  | Add custom words. |
| [delete-word](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#delete-word) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,     word,  | Delete a custom word. |
| [get-word](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#get-word) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,     word,  | Get a custom word. |
| [list-words](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#list-words) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customization_id,  | List custom words. |
| [delete-user-data](https://www.ibm.com/watson/developercloud/text-to-speech/api/v1/curl.html?curl#delete-user-data) | action |  username, password,  iam_access_token, iam_apikey, iam_url,  headers, headers[X-Watson-Learning-Opt-Out], url,    customer_id,  | Delete labeled data. |

## Creating a {{site.data.keyword.texttospeechshort}} service instance
{: #service_instance_texttospeech}

Before you install the package, you must create a {{site.data.keyword.texttospeechshort}} service instance and service credentials.
{: shortdesc}

1. [Create a {{site.data.keyword.texttospeechshort}} service instance ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/text_to_speech).
2. When the service instance is created, auto-generated service credentials are also created for you.

## Installing the {{site.data.keyword.texttospeechshort}} package
{: #install_texttospeech}

After you have an {{site.data.keyword.texttospeechshort}} service instance, use the {{site.data.keyword.openwhisk}} CLI to install the {{site.data.keyword.texttospeechshort}} package into your namespace.
{: shortdesc}

### Installing from the {{site.data.keyword.openwhisk_short}} CLI
{: #texttospeech_cli}

Before you begin:
  1. [Install the {{site.data.keyword.openwhisk_short}} plugin for the {{site.data.keyword.Bluemix_notm}} CLI](/docs/openwhisk?topic=cloud-functions-cli_install).

To install the {{site.data.keyword.texttospeechshort}} package:

1. Clone the {{site.data.keyword.texttospeechshort}} package repo.
    ```
    git clone https://github.com/watson-developer-cloud/openwhisk-sdk
    ```
    {: pre}

2. Deploy the package.
    ```
    ibmcloud fn deploy -m openwhisk-sdk/packages/text-to-speech-v1/manifest.yaml
    ```
    {: pre}

3. Verify that the package is added to your package list.
    ```
    ibmcloud fn package list
    ```
    {: pre}

    Output:
    ```
    packages
    /myOrg_mySpace/text-to-speech-v1                        private
    ```
    {: screen}

4. Bind the credentials from the {{site.data.keyword.texttospeechshort}} instance you created to the package.
    ```
    ibmcloud fn service bind text_to_speech text-to-speech-v1
    ```
    {: pre}

    Depending on the region where you created the service instance, the service instance might be named differently because it is an IAM service. If the above command fails, use the following service name for the bind command:
    ```
    ibmcloud fn service bind text-to-speech text-to-speech-v1
    ```
    {: pre}
    Example output:
    ```
    Credentials 'Credentials-1' from 'text_to_speech' service instance 'Watson Text to Speech' bound to 'text-to-speech-v1'.
    ```
    {: screen}

5. Verify that the package is configured with your {{site.data.keyword.texttospeechshort}} service instance credentials.
    ```
    ibmcloud fn package get text-to-speech-v1 parameters
    ```
    {: pre}

    Example output:
    ```
    ok: got package text-to-speech-v1, displaying field parameters
    [
      {
        "key": "__bx_creds",
        "value": {
          "text_to_speech": {
            "credentials": "Credentials-1",
            "instance": "Watson Text to Speech",
            "password": "AAAA0AAAAAAA",
            "url": "https://gateway.watsonplatform.net/text_to_speech/api",
            "username": "00a0aa00-0a0a-12aa-1234-a1a2a3a456a7"
          }
        }
      }
    ]
    ```
    {: screen}

### Installing from the {{site.data.keyword.openwhisk_short}} UI
{: #texttospeech_ui}

1. In the {{site.data.keyword.openwhisk_short}} console, go to the [Create page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/openwhisk/create).

2. By using the **Cloud Foundry Org** and **Cloud Foundry Space** lists, select the namespace that you want to install the package into. 

3. Click **Install Packages**.

4. Click the **Watson** Package group.

5. Click the **Text To Speech** Package.

5. Click **Install**.

6. Once the package has been installed you will be redirected to the actions page and can search for your new package, which is named **text-to-speech-v1**.

7. To use the actions in the **text-to-speech-v1** Package, you must bind service credentials to the actions.
  * To bind service credentials to all actions in the package, follow steps 5 and 6 in the CLI instructions listed above.
  * To bind service credentials to individual actions, complete the following steps in the UI. **Note**: You must complete the following steps for each action that you want to use.
    1. Click an action from the **text-to-speech-v1** Package that you want to use. The details page for that action opens.
    2. In the left-hand navigation, click the **Parameters** section.
    3. Enter a new **parameter**. For the key, enter `__bx_creds`. For the value, paste in the service credentials JSON object from the service instance that you created earlier.

## Using the {{site.data.keyword.texttospeechshort}} package
{: #usage_texttospeech}

To use the actions in this package, run commands in the following format:

```
ibmcloud fn action invoke text-to-speech-v1/<action_name> -b -p <param name> <param>
```
{: pre}

Try out the `list-voices` action.
```
ibmcloud fn action invoke text-to-speech-v1/list-voices -b
```
{: pre}
