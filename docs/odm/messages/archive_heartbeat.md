[comment]: # (AUTOGENERATED MARKDOWN CONTENT. UPDATES TO ODM DOCUMENTATION SHOULD BE DONE THROUGH ASSEMBLYLINE-BASE REPO!)
# ArchiveMessage
> Model for Archive Heartbeat Messages

| Field | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| msg | [Heartbeat](/assemblyline4_docs/odm/messages/archive_heartbeat/#heartbeat) | Heartbeat message | :material-checkbox-marked-outline: Yes | `None` |
| msg_loader | Enum | Loader class for message<br>Values:<br>`"assemblyline.odm.messages.archive_heartbeat.ArchiveMessage"` | :material-checkbox-marked-outline: Yes | `assemblyline.odm.messages.archive_heartbeat.ArchiveMessage` |
| msg_type | Enum | Message type<br>Values:<br>`"ArchiveHeartbeat"` | :material-checkbox-marked-outline: Yes | `ArchiveHeartbeat` |
| sender | Keyword | Sender of message | :material-checkbox-marked-outline: Yes | `None` |


[comment]: # (AUTOGENERATED MARKDOWN CONTENT. UPDATES TO ODM DOCUMENTATION SHOULD BE DONE THROUGH ASSEMBLYLINE-BASE REPO!)
## Heartbeat
> Archive Heartbeat Model

| Field | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| instances | Integer | Number of instances | :material-checkbox-marked-outline: Yes | `None` |
| metrics | [Metrics](/assemblyline4_docs/odm/messages/archive_heartbeat/#metrics) | Archive metrics | :material-checkbox-marked-outline: Yes | `None` |
| queued | Integer | Number of documents to be archived | :material-checkbox-marked-outline: Yes | `None` |


[comment]: # (AUTOGENERATED MARKDOWN CONTENT. UPDATES TO ODM DOCUMENTATION SHOULD BE DONE THROUGH ASSEMBLYLINE-BASE REPO!)
### Metrics
> Archive Metrics

| Field | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| file | Integer | Number of files archived | :material-checkbox-marked-outline: Yes | `None` |
| result | Integer | Number of results archived | :material-checkbox-marked-outline: Yes | `None` |
| submission | Integer | Number of submissions archived | :material-checkbox-marked-outline: Yes | `None` |
| received | Integer | Number of received archive messages | :material-checkbox-marked-outline: Yes | `None` |
| exception | Integer | Number of exceptions during archiving | :material-checkbox-marked-outline: Yes | `None` |
| invalid | Integer | Number of invalid archive type errors during archiving | :material-checkbox-marked-outline: Yes | `None` |
| not_found | Integer | Number of submission not found failures during archiving | :material-checkbox-marked-outline: Yes | `None` |


