# Centralised Logging

Monitor 24 can upload logs via HTTPS POST request to an endpoint, we also support uploading to Microsoft Azure monitor logs.

## Upload to HTTPS Endpoint

Set the following keys.

| Key Name             | Type                    | Function                                                                                                                          |
| -------------------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| siemUploadURL        | String                  | URL to upload data to                                                                                                             |
| siemUploadHeaders    | Array of Dictionaries   | Each dictionary made up of 2 key values `Header` and `Value`                                                                      |
| siemNewLineSeperated | Boolean (default false) | By default events are uploaded in JSON format as an array of events. Some systems require events to be seperated with a new line. |
| MaxDataUploadSize    | Integer (1MB Default)   | The maximum size of the data to be sent in 1 request (uncompressed)                                                               |
| UploadOnHotSpot      | Boolean (default false) | Set to true to upload data when the mac detects it is connected to a mobile hotspot                                               |

```
<dict>
	<key>MaxDataUploadSize</key>
	<integer>1000000</integer>
	<key>UploadOnHotspot</key>
	<false/>
	<key>siemNewLineSeperated</key>
	<true/>
	<key>siemUploadHeaders</key>
	<array>
		<dict>
			<key>Header</key>
			<string>x-api-key</string>
			<key>Value</key>
			<string>123455432112345</string>
		</dict>
	</array>
	<key>siemUploadURL</key>
	<string>https://example.com/upload</string>
</dict>
```

## Upload to Microsoft Azure

The following tutorial may be useful for configuring Azure Monitor Logs - https://learn.microsoft.com/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-portal

Set the following keys.

| Key Name             | Type   | Function                         |
| -------------------- | ------ | -------------------------------- |
| SentinelTennantId    | String | Tennant ID                       |
| SentinelClientId     | String | Client ID                        |
| SentinelClientSecret | String | Client Secret                    |
| SentinelUploadURL    | String | The data collection endpoint URL |
