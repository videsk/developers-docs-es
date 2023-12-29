# Metadata

Once the integration to synchronize the recordings is completed and correct, they will start to be sent with metadata associated with the call, which will allow you to search for recordings in an enriched manner.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

By default, we attach:

| Key         | Value  | Description                                              |
| ----------- | ------ | -------------------------------------------------------- |
| duration    | Number | Duration of the recording in minutes                     |
| checkSum    | String | CheckSum of the recording with SHA-1                     |
| startedAt   | Date   | Timestamp when the recording started                     |
| endedAt     | Date   | Timestamp when the recording ended                       |
| user        | String | Executive's ID                                           |
| extension   | String | File extension, by default: _webm_                       |
| uploadDate  | Date   | Date when the sync with cloud storage was attempted     |
| recordingId | String | ID of the tracks (not call)                              |
| size        | Number | File size in bytes                                       |
| identifier  | String | ID of the call                                           |
| contentType | String | MIME type of the file, by default: _video/webm_          |