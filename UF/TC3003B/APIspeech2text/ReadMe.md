# Quick tutorial to create speech 2 text API

1. Go to (as of 05/2024) : https://console.cloud.google.com/apis/api/speech.googleapis.com
2. Credentials Tab
3. Click on _+ CREATE CREDENTIALS_
4. Generate the APIkey
5. Go to : https://console.cloud.google.com/storage/
6. Create a new bucket and enable public access (allUsers / Storage Object User)
7. Drag you audio file to the bucket (audio.flac)
8. Call the API as

```bash
curl -s -H "Content-Type: application/json" https://speech.googleapis.com/v1/speech:recognize?key=<APIkey> -d @sync-request.json
```

sync-request.json
```json
{
  "config": {
      "encoding":"FLAC",
      "sampleRateHertz": 44100,
      "languageCode": "en-US",
      "audio_channel_count" : 2,
      "enableWordTimeOffsets": false
  },
  "audio": {
      "uri":"gs://<bucket>/audio.flac"
  }
}
```
