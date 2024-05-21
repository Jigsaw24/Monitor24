# Configuration Reference

I highly recommend using the iMazing Profile Editor app with the supplied profile manifest. Configuration must be deployed via MDM.

Domain - com.jigsaw24.Monitor24

| Key Name                    | Type    | Default                             | Function                                                                                      |
| :-------------------------- | :------ | :---------------------------------- | :-------------------------------------------------------------------------------------------- |
| RecordingEnabled            | Boolean | False                               | Set to True to enable recording of events.                                                    |
| DisableAll                  | Boolean | False                               | Set to True to disable all functionality                                                      |
| EnableArchive               | Boolean | False                               | Enable local archiving of events on the device.                                               |
| MaxArchiveAge               | Integer | 7                                   | Set the maximum age of events stored in the local archive                                     |
| DefaultFilterRules          | Boolean | False                               | Enable default filter rules. Default filters attempt to not log normal background operations. |
| DoNotLogHomeDirectoryWrites | Boolean | False                               | Do not log file write operations to files within the logged in user's Home directory          |
| filterRules                 | Array   | _None_                              | See [Filters](#filters)                                                                       |
| SelfProtectionRules         | Boolean | False                               | Enable Auth rules which attempts to stop the removal of Monitor24                             |
| FileOperationRules          | Array   | _None_                              | See [File Operation Rules]                                                                    |
| logAllEventTypes            | Boolean | False                               | Set to True to log all event types                                                            |
| EventsToLog                 | Array   | See [Events To Log](#Events To Log) |

Please see [Centralised Logging](./Logging.md) for logging configuration.

# Filters

Filters are definied using the `filterRules` key this is an array of dictionary objects (dict). If a value is left unset it will not be used for that rule.

| Key Name  | Type   | Default | Function                                                                                                  |
| :-------- | :----- | :------ | :-------------------------------------------------------------------------------------------------------- |
| eventType | String | _None_  | Event type the filter to be active on. Set to 'All' for all eventTypes ( see [Event Types](#event-types)) |
| path      | String | _None_  | File path to match. A trailing \* is supported.                                                           |
| signingId | String | _None_  | The siging id of the process causing the event.                                                           |

# File Operation Rules

Rules to restrict file operations. Allow rules can be used in conjunction with block rules to allow a process to execute under the specified conditions.
File open operations can be restricted to read only access where required.
If a value is left unset it will not be used for that rule.

| Key Name      | Type   | Default | Function                                                                                                                             |
| :------------ | :----- | :------ | :----------------------------------------------------------------------------------------------------------------------------------- |
| fileOperation | String | _None_  | The file operation this rule will apply to. Currently "file:open" or "file:unlink"                                                   |
| action        | String | _None_  | Set the action for the rule. Accepted values are `allow`/`block`/`readOnly`. Read only is only available for `file:open` operations. |
| signingID     | String | _None_  | The signing ID of the process making the request.                                                                                    |
| username      | String | _None_  | The username of the running process making the request.                                                                              |

# Execute Process Rules

Rules to allow or block the execution of processes based on specific conditions.
If a value is left unset it will not be used for that rule.
| Key Name | Type | Default | Function |
| :------------------------ | :----- | :------ | :----------------------------------------------------------------------------------------------------------------------------------- |
| action | String | _None_ | Set the action for the rule. Accepted values are `allow`/`block`. |
| processPath | String | _None_ | The path of the process to match. |
| signingID | String | _None_ | The signing ID of the process to match. |
| teamID | String | _None_ | The team ID of the process to match. |
| matchingArgumentsContaining | String | _None_ | Match processes where the argument contains txt supplied here. Multiple arguments can be comma seperated if needed. |

# Event Types

Supported Event Types are listed here.

| Event Type        |
| :---------------- |
| File:Write        |
| File:Unlink       |
| File:Clone        |
| File:CopyFile     |
| File:Create       |
| File:Rename       |
| User:Create       |
| User:Delete       |
| Profile:Add       |
| Profile:Remove    |
| LaunchItem:Add    |
| LaunchItem:Remove |
| Sudo              |
| Process:Exec      |

# Events To Log

Key - EventsToLog

Specifies the Event Types which will be logged. This configuration is made of an array of dictionary objects with a key set to `eventType` with the value set to one of the [Event Types](#event-types)

````
	<key>EventsToLog</key>
	<array>
		<dict>
			<key>eventType</key>
			<string>File:Write</string>
		</dict>
		<dict>
			<key>eventType</key>
			<string>File:Clone</string>
		</dict>
	</array>
    ```
````
