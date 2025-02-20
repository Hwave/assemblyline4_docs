[comment]: # (AUTOGENERATED MARKDOWN CONTENT. UPDATES TO ODM DOCUMENTATION SHOULD BE DONE THROUGH ASSEMBLYLINE-BASE REPO!)
# Process
> Details about a process

| Field | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| objectid | [ObjectID](/assemblyline4_docs/odm/models/ontology/results/process/#objectid) | The object ID of the process object | :material-checkbox-marked-outline: Yes | `None` |
| image | Text | The image of the process | :material-checkbox-marked-outline: Yes | `<unknown_image>` |
| start_time | Date | The time of creation for the process | :material-checkbox-marked-outline: Yes | `None` |
| pobjectid | [ObjectID](/assemblyline4_docs/odm/models/ontology/results/process/#objectid) | The object ID of the parent process object | :material-minus-box-outline: Optional | `None` |
| pimage | Text | The image of the parent process that spawned this process | :material-minus-box-outline: Optional | `None` |
| pcommand_line | Text | The command line that the parent process ran | :material-minus-box-outline: Optional | `None` |
| ppid | Integer | The process ID of the parent process | :material-minus-box-outline: Optional | `None` |
| pid | Integer | The process ID | :material-minus-box-outline: Optional | `None` |
| command_line | Text | The command line that the process ran | :material-minus-box-outline: Optional | `None` |
| end_time | Date | The time of termination for the process | :material-minus-box-outline: Optional | `None` |
| integrity_level | Text | The integrity level of the process | :material-minus-box-outline: Optional | `None` |
| image_hash | Text | The hash of the file run | :material-minus-box-outline: Optional | `None` |
| original_file_name | Text | The original name of the file | :material-minus-box-outline: Optional | `None` |


[comment]: # (AUTOGENERATED MARKDOWN CONTENT. UPDATES TO ODM DOCUMENTATION SHOULD BE DONE THROUGH ASSEMBLYLINE-BASE REPO!)
## ObjectID
> Details about the characteristics used to identify an object

| Field | Type | Description | Required | Default |
| :--- | :--- | :--- | :--- | :--- |
| tag | Text | The normalized tag of the object | :material-checkbox-marked-outline: Yes | `None` |
| ontology_id | Keyword | Deterministic identifier of ontology. This value should be able to be replicable between services that have access to similar object details, such that it can be used for relating objects in post-processing. | :material-checkbox-marked-outline: Yes | `None` |
| service_name | Keyword | Component that generated this section | :material-checkbox-marked-outline: Yes | `unknown` |
| guid | Text | The GUID associated with the object | :material-minus-box-outline: Optional | `None` |
| treeid | Text | The hash of the tree ID | :material-minus-box-outline: Optional | `None` |
| processtree | Keyword | Human-readable tree ID (concatenation of tags) | :material-minus-box-outline: Optional | `None` |
| time_observed | Date | The time at which the object was observed | :material-minus-box-outline: Optional | `None` |
| session | Keyword | Unifying session name/ID | :material-minus-box-outline: Optional | `None` |


