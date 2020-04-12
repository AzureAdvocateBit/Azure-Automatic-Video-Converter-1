---
services: media-services,functions,logic-app
platforms: dotnet
author: shigeyf
---

# Functions documentation

This section lists the functions available and describes the input and output parameters.
This Functions example is based on AMS REST API v3 and pre-compiled functions.

# Functions List

- [CreateEmptyAsset](#createemptyasset)
- [CreateTransform](#createtransform)
- [GetAssetUrls](#getasseturls)
- [MonitorBlobContainerCopyStatus](#monitorblobcontainercopystatus)
- [MonitorMediaJob](#monitormediajob)
- [PublishAsset](#publishasset)
- [StartBlobContainerCopyToAsset](#startblobcontainercopytoasset)
- [SubmitMediaJob](#submitmediajob)


## CreateEmptyAsset

This function creates an empty asset.

```c#
Input:
    {
        // [Required] The name of the asset
        "assetNamePrefix": "TestAssetName",

        // The name of attached storage account where to create the asset
        "assetStorageAccount":  "storage01"
    }
Output:
    {
        // The name of the asset created
        "assetName": "TestAssetName-180c777b-cd3c-4e02-b362-39b8d94d7a85",

        // The identifier of the asset created
        "assetId": "nb:cid:UUID:68adb036-43b7-45e6-81bd-8cf32013c810",

        // The name of the destination container name for the asset created
        "destinationContainer": "destinationContainer": "asset-4a5f429c-686c-4f6f-ae86-4078a4e6139e"
    }

```

[Back to List](#functions-list)

## CreateStreamingPolicy

This function creates a new transform.

```c#
Input:
    {
        // [Required] The name of the streaming policy.
        "streamingPolicyName": "SharedStreamingForClearKey",

        // [Required] The mode for creating the transform.
        // Allowed values: "simple" or "advanced".
        // Default value: "simple".
        "mode": "simple",

        // Default Content Key used by current streaming policy.
        "defaultContentKeyPolicyName": "SharedContentKeyPolicyForClearKey",

        //
        // [mode = simple]
        //
        // Semi-colon-separated list of enabled protocols for NoEncryption.
        // Allowed values: Download, Dash, HLS, SmoothStreaming.
        "noEncryptionProtocols": "Dash;HLS;SmoothStreaming"

        //
        // [mode = simple]
        //
        //
        // Common Encryption CBCS Arguments
        //
        // The JSON representing which tracks should not be encrypted.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#trackselection.
        "cbcsClearTracks": {},
        // Label to specify Default Content Key for an encryption scheme.
        "cbcsDefaultKeyLabel": "cbcsKeyDefault",
        // Policy used by Default Content Key.
        "cbcsDefaultKeyPolicyName": null,
        // The JSON representing a list of StreamingPolicyContentKey.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#streamingpolicycontentkey.
        "cbcsKeyToTrackMappings": {},
        // Allows the license to be persistent or not.
        // Allowed values: false, true.
        "cbcsFairPlayAllowPersistentLicense": false,
        // The custom license acquisition URL template for a customer service to deliver keys to end users.
        // Not needed when using Azure Media Services for issuing keys.
        "cbcsFairPlayTemplate": null,
        // Custom attributes for PlayReady.
        "cbcsPlayReadyAttributes": null,
        // The custom license acquisition URL template for a customer service to deliver keys to end users.
        // Not needed when using Azure Media Services for issuing keys.
        "cbcsPlayReadyTemplate": null,
        // The custom license acquisition URL template for a customer service to deliver keys to end users.
        // Not needed when using Azure Media Services for issuing keys.
        "cbcsWidevineTemplate": null,
        // Semi-colon-separated list of enabled protocols for CommonEncryption CBCS.
        // Allowed values: Dash, HLS, SmoothStreaming.
        "cbcsProtocols": "Dash;HLS;SmoothStreaming",

        //
        // [mode = simple]
        //
        //
        // Common Encryption CENC Arguments
        //
        // The JSON representing which tracks should not be encrypted.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#trackselection.
        "cencClearTracks": {},
        // Label to specify Default Content Key for an encryption scheme.
        "cencDefaultKeyLabel": "cencKeyDefault",
        // Policy used by Default Content Key.
        "cencDefaultKeyPolicyName": null,
        // The JSON representing a list of StreamingPolicyContentKey.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#streamingpolicycontentkey.
        "cencKeyToTrackMappings": {},
        // Custom attributes for PlayReady.
        "cencPlayReadyAttributes": null,
        // The custom license acquisition URL template for a customer service to deliver keys to end users.
        // Not needed when using Azure Media Services for issuing keys.
        "cencPlayReadyTemplate": null,
        // The custom license acquisition URL template for a customer service to deliver keys to end users.
        // Not needed when using Azure Media Services for issuing keys.
        "cencWidevineTemplate": null,
        // Semi-colon-separated list of enabled protocols for CommonEncryption CENC.
        // Allowed values: Dash, HLS, SmoothStreaming.
        "cencProtocols": "Dash;HLS;SmoothStreaming",

        //
        // [mode = simple]
        //
        //
        // Envelope Encryption Arguments
        //
        // The JSON representing which tracks should not be encrypted.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#trackselection.
        "envelopeClearTracks": {},
        // Label to specify Default Content Key for an encryption scheme.
        "envelopeDefaultKeyLabel": "cencKeyDefault",
        // Policy used by Default Content Key.
        "envelopeDefaultKeyPolicyName": null,
        // The JSON representing a list of StreamingPolicyContentKey.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streamingpolicies/create#streamingpolicycontentkey.
        "envelopeKeyToTrackMappings": {},
        // The KeyAcquistionUrlTemplate is used to point to user specified service to delivery content keys.
        "envelopeTemplate": null,
        // Semi-colon-separated list of enabled protocols for CommonEncryption CENC.
        // Allowed values: Dash, HLS, SmoothStreaming.
        "envelopeProtocols": "Dash;HLS;SmoothStreaming",

        //
        // [mode = advanced]
        //
        // Streaming Configuration option of Common Encryption CBCS
        "jsonCommonEncryptionCbcs": {
            "enabledProtocols": {
                "download": false,
                "dash": false,
                "hls": true,
                "smoothStreaming": false
            },
            "contentKeys": {
                "defaultKey": {
                    "label": "cbcsDefaultKey"
                }
            },
            "drm": {
                "fairPlay": {
                    "allowPersistentLicense": true
                }
            }
        }
        // Streaming Configuration option of Common Encryption CENC
        "jsonCommonEncryptionCenc": {
            "enabledProtocols": {
                "download": false,
                "dash": true,
                "hls": false,
                "smoothStreaming": true
            },
            "contentKeys": {
                "defaultKey": {
                    "label": "cencDefaultKey"
                }
            },
            "drm": {
                "playReady": {},
                "widevine": {}
            }
        }
        // Streaming Configuration option of Envelope Encryption
        "jsonEnvelopeEncryption": {}
        // Streaming Configuration option of No Encryption
        "jsonNoEncryption": {}
    }
Output:
    {
        // The name of the streaming policy.
        "streamingPolicyName": "SharedStreamingForClearKey",

        // The identifier of the streaming policy.
        "streamingPolicyId": "9d6a2b92-d61a-4e87-8348-7155c137f9ca",
    }

```

[Back to List](#functions-list)

## CreateTransform

This function creates a new transform.

```c#
Input:
    {
        // [Required] The name of the transform.
        "transformName": "TestTransform",

        // [Required] The mode for creating the transform.
        // Allowed values: "simple" or "advanced".
        // Default value: "simple".
        "mode": "simple",

        // The description of the transform.
        "description": "Transform for testing",

        //
        // [mode = simple]
        //
        // [Required] Preset that describes the operations
        // that will be used to modify, transcode, or extract insights
        // from the source file to generate the transform output.
        // Allowed values:
        //  H264SingleBitrateSD, H264SingleBitrate720p, H264SingleBitrate1080p,
        //  AdaptiveStreaming, AACGoodQualityAudio,
        //  H264MultipleBitrate1080p, H264MultipleBitrate720p, H264MultipleBitrateSD,
        //  AudioAnalyzer, VideoAnalyzer,
        //  CustomPreset.
        "preset": "AdaptiveStreaming",

        //
        // [mode = simple]
        //
        // The JSON representing a custom preset.
        // See https://docs.microsoft.com/rest/api/media/transforms/createorupdate#standardencoderpreset
        // for further details on the settings to use to build a custom preset.
        "customPresetJson": { ... },

        //
        // [mode = simple]
        //
        // A Transform can define more than one output.
        // This property defines what the service should do when one output fails -
        // either continue to produce other outputs, or, stop the other outputs.
        // The overall Job state will not reflect failures of outputs that are specified with 'ContinueJob'.
        // The default is 'StopProcessingJob'.
        // Allowed values: ContinueJob, StopProcessingJob.
        "onError": "StopProcessingJob",

        //
        // [mode = simple]
        //
        // Sets the relative priority of the transform outputs within a transform.
        // This sets the priority that the service uses for processing TransformOutputs.
        // The default priority is Normal.
        // Allowed values: High, Low, Normal.
        "relativePriority": "Normal",

        //
        // [mode = simple & preset = AudioAnalyzer | VideoAnalyzer]
        //
        // The language for the audio payload in the input using the BCP-47 format of "language tag-region" (e.g: en-US).
        // If not specified, automatic language detection would be employed.
        // This feature currently supports English, Chinese, French, German,
        // Italian, Japanese, Spanish, Russian, and Portuguese.
        // The automatic detection works best with audio recordings with clearly discernable speech.
        // If automatic detection fails to find the language, transcription would fallback to English.
        // Allowed values: en-US, en-GB, es-ES, es-MX, fr-FR, it-IT, ja-JP, pt-BR, zh-CN, de-DE, ar-EG, ru-RU, hi-IN.
        "audioLanguage": "en-US",

        //
        // [mode = simple & preset = VideoAnalyzer]
        //
        // The type of insights to be extracted.
        // If not set then the type will be selected based on the content type.
        // If the content is audio only then only audio insights will be extracted
        // and if it is video only video insights will be extracted.
        // Allowed values: AllInsights, AudioInsightsOnly, VideoInsightsOnly.
        "insightsToExtract": "AllInsights",

        //
        // [mode = advanced]
        //
        // [Required] The array of custom presets for the transform.
        "transformOutputs": [
            {
                "onError": "StopProcessingJob",
                "relativePriority": "Normal",
                "preset": {
                    "@odata.type": "#Microsoft.Media.BuiltInStandardEncoderPreset",
                    "presetName": "AdaptiveStreaming"
                }
            },
            {
                "onError": "StopProcessingJob",
                "relativePriority": "Normal",
                "preset": {
                    "@odata.type": "#Microsoft.Media.VideoAnalyzerPreset",
                    "audioLanguage": "en-US",
                    "audioInsightsOnly": false
                }
            }
        ]
    }
Output:
    {
        // The name of the created TransformName
        "transformName": "TestTransform",

        // The resource identifier of the created Transform
        "transformId": "/subscriptions/694d5930-8ee4-4e50-917b-9dcfeceb6179/resourceGroups/AMSdemo/providers/Microsoft.Media/mediaservices/amsdemojapaneast/transforms/TestTransform"
    }

```

[Back to List](#functions-list)


## GetAssetUrls

This function provides URLs for the asset.

```c#
Input:
    {
        // [Required] The name of the streaming locator.
        "streamingLocatorName": "streaminglocator-911b65de-ac92-4391-9aab-80021126d403",

        // The name of the streaming endpoint; "default" is used by default
        "streamingEndpointName": "default",

        // The scheme of the streaming URL; "http" or "https", and "https" is used by default
        "streamingUrlScheme": "https"
    }
Output:
    {
        // The path list of Progressive Download
        "downloadPaths": [],

        // The path list of Streaming
        "streamingPaths": [
            {
                // Streaming Protocol
                "StreamingProtocol": "Hls",
                // Encryption Scheme
                "EncryptionScheme": "EnvelopeEncryption",
                // Streaming URL
                "StreamingUrl": "https://amsv3demo-jpea.streaming.media.azure.net/6c4bb037-6907-406d-8e4d-15f91e44ac08/Ignite-short.ism/manifest(format=m3u8-aapl,encryption=cbc)"
            },
            {
                "StreamingProtocol": "Dash",
                "EncryptionScheme": "EnvelopeEncryption",
                "StreamingUrl": "https://amsv3demo-jpea.streaming.media.azure.net/6c4bb037-6907-406d-8e4d-15f91e44ac08/Ignite-short.ism/manifest(format=mpd-time-csf,encryption=cbc)"
            },
            {
                "StreamingProtocol": "SmoothStreaming",
                "EncryptionScheme": "EnvelopeEncryption",
                "StreamingUrl": "https://amsv3demo-jpea.streaming.media.azure.net/6c4bb037-6907-406d-8e4d-15f91e44ac08/Ignite-short.ism/manifest(encryption=cbc)"
            }
        ]
    }

```

[Back to List](#functions-list)

## MonitorBlobContainerCopyStatus

This function monitors blob copy.
[blobCopyStatus](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.copystatus?view=azure-dotnet) is returned with the following values:

- 0 : Invalid - The copy status is invalid.
- 1 : Pending - The copy operation is pending.
- 2 : Success - The copy operation succeeded.
- 3 : Aborted - The copy operation has been aborted.
- 4 : Failed - The copy operation encountered an error.

```c#
Input:
    {
        // [Required] The name of the asset for copy destination
        "assetName": "TestAssetName-180c777b-cd3c-4e02-b362-39b8d94d7a85",
        // The file names for monitoring
        //      all blobs in the destination container will be monitored if no fileNames
        "fileNames": [ "filename.mp4" , "filename2.mp4" ]
    }
Output:
    {
        // BlobCopy Action Status: true or false
        "copyStatus": true|false,
        // CopyStatus for each blob
        "blobCopyStatusList": [
            {
                // Name of blob
                "blobName": "filename.mp4",
                // Blob CopyStatus code (see below)
                "blobCopyStatus": 2
            }
        ]
    }

```

[Back to List](#functions-list)

## MonitorMediaJob

This function monitors media job.
[jobState](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.media.models.jobstate?view=azure-dotnet) is returned with the following values:

| JobState Name | Description   |
| ------------- | ------------- |
| Canceled | The job was canceled. This is a final state for the job. |
| Canceling | The job is in the process of being canceled. This is a transient state for the job. |
| Error | The job has encountered an error. This is a final state for the job. |
| Finished | The job is finished. This is a final state for the job. |
| Processing | The job is processing. This is a transient state for the job. |
| Queued | The job is in a queued state, waiting for resources to become available. This is a transient state. |
| Scheduled | The job is being scheduled to run on an available resource. This is a transient state, between queued and processing states. |

If jobState is "Error", the output will contain the job error information: [ErrorCode](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.media.models.joberrorcode?view=azure-dotnet) and ErrorMessage.

```c#
Input:
    {
        // [Required] The name of the media job
        "jobName": "amsv3function-job-24369d2e-7415-4ff5-ba12-b8a879a15401",

        // [Required] The name of the Transform for the media job
        "transformName": "TestTransform"
    }
Output:
    {
        // The status name of the media job
        "jobStatus": "Finished",

        // The status of each task/output asset in the media job
        "jobOutputStateList": [
            {
                // Name of the Output Asset
                "AssetName": "out-testasset-efbf71e8-3f80-480d-9b92-f02bef6ad4d2",
                // Status of the media task for the Output Asset
                "State": "Finished",
                // Progress of the media task for the Output Asset
                "Progress": 100
            },
            ...
        ]
    }

```

[Back to List](#functions-list)

## PublishAsset

This function publishes the asset (creates a StreamingLocator for the asset).
Pre-defined Streaming Policy which you can use by default are as below:

- Predefined_ClearKey
- Predefined_ClearStreamingOnly
- Predefined_DownloadAndClearStreaming
- Predefined_DownloadOnly
- Predefined_MultiDrmCencStreaming
- Predefined_MultiDrmStreaming

```c#
Input:
    {
        // [Required] The name of the asset used by the streaming locator.
        "assetName": "TestAssetName-180c777b-cd3c-4e02-b362-39b8d94d7a85",

        // [Required] The name of the streaming policy used by the streaming locator.
        // You can either create one with `CreateStreamingPolicy` or use any of the predefined policies:
        //  Predefined_ClearKey,
        //  Predefined_ClearStreamingOnly,
        //  Predefined_DownloadAndClearStreaming,
        //  Predefined_DownloadOnly,
        //  Predefined_MultiDrmCencStreaming,
        //  Predefined_MultiDrmStreaming.
        "streamingPolicyName": "Predefined_ClearStreamingOnly",

        // An alternative media identifier associated with the streaming locator.
        "alternative-media-id": "cid-0001",

        // The default content key policy name used by the streaming locator.
        "contentKeyPolicyName": "defaultContentKeyPolicy",

        // JSON string with the content keys to be used by the streaming locator.
        // For further information about the JSON structure please refer to swagger documentation on
        // https://docs.microsoft.com/en-us/rest/api/media/streaminglocators/create#streaminglocatorcontentkey.
        "contentKeys": null,

        // The start time (Y-m-d'T'H:M:S'Z') of the streaming locator.
        "startDateTime": "2018-07-01T00:00Z",

        // The end time (Y-m-d'T'H:M:S'Z') of the streaming locator.
        "endDateTime": "2018-12-31T23:59Z",

        // The identifier (UUID) of the streaming locator. "streamingLocatorName" will be "streaminglocator-{UUID}".
        "streamingLocatorId": "911b65de-ac92-4391-9aab-80021126d403"
    }
Output:
    {
        // The name of the created StreamingLocatorName
        "streamingLocatorName": "streaminglocator-911b65de-ac92-4391-9aab-80021126d403",

        // The name of the created StreamingLocatorId
        "streamingLocatorId": "911b65de-ac92-4391-9aab-80021126d403"
    }

```

[Back to List](#functions-list)


## StartBlobContainerCopyToAsset

This function starts copying blob container to the asset.

```c#
Input:
    {
        // [Required] The name of the Asset for media job input
        "inputAssetName": "TestAssetName-180c777b-cd3c-4e02-b362-39b8d94d7a85",

        // [Required] The name of the Transform for media job
        "transformName": "TestTransform",

        // [Required] The name of the Assets for media job outputs
        "outputAssetNamePrefix": "TestOutputAssetName",

        // The name of attached storage account where to create the Output Assets
        "assetStorageAccount": "storage01"
    }
Output:
    {
        // The name of media Job
        "jobName": "amsv3function-job-24369d2e-7415-4ff5-ba12-b8a879a15401",

        // The name of Encdoer Output Asset
        "encoderOutputAssetName": "out-testasset-e389de79-3aa5-4a5a-a9ca-2a6fd8c53968",

        // The name of Video Analyzer Output Asset
        "videoAnalyzerOutputAssetName": "out-testasset-00cd363b-5fe0-4da1-acf8-ebd66ef14504"
    }

```

[Back to List](#functions-list)

## SubmitMediaJob

This function submits media job.

```c#
Input:
    {
        // Name of the Asset for media job input
        "inputAssetName": "TestAssetName-180c777b-cd3c-4e02-b362-39b8d94d7a85",
        // Name of the Transform for media job
        "transformName": "TestTransform",
        // Name of the Assets for media job outputs
        "outputAssetNamePrefix": "TestOutputAssetName",
        // (Optional) Name of attached storage account where to create the Output Assets
        "assetStorageAccount": "storage01"
    }
Output:
    {
        // Name of media Job
        "jobName": "amsv3function-job-24369d2e-7415-4ff5-ba12-b8a879a15401",
        // Name of Encdoer Output Asset
        "encoderOutputAssetName": "out-testasset-e389de79-3aa5-4a5a-a9ca-2a6fd8c53968",
        // Name of Video Analyzer Output Asset
        "videoAnalyzerOutputAssetName": "out-testasset-00cd363b-5fe0-4da1-acf8-ebd66ef14504"
    }

```

[Back to List](#functions-list)
