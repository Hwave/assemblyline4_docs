# Service manifest

Every service must have a `service_manifest.yml` file in its root directory. The manifest file presents essential
information about the service to the Assemblyline core system, information the Assemblyline core system must have before
it can run the service.

The table below shows all the elements that the manifest file can contain, including a brief description of each.

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| accepts | Keyword | No <br> Default: `.*` | Regexes applied to Assemblyline style file type string. For example, `.*` will allow the service to accept all types of files. |
| category | Keyword | No <br> Default: `Static Analysis` | Which category is the service part of? Must be one of `Antivirus`, `Dynamic Analysis`, `External`, `Extraction`, `Filtering`, `Networking`, or `Static Analysis`. |
| config | Mapping of Any | No | Dictionary of service configuration variables. The key names can be any Keyword and the value can be of Any type. |
| default_result_classification | Classification string | No <br> Default: `UNRESTRICTED` | The default classification for the results generated by the service. If no classification is provided for a result section, this default classification is used. |
| dependencies | Mapping of [Dependency Config](#dependency-config) | No | Refer to the [dependency config](#dependency-config) section. |
| description | Text | No <br> Default: `NA` | Detailed description of the service and its features. |
| disable_cache | Boolean | No <br> Default: `false` | Should the result cache be disabled for this service? Only disable caching for services that will always provide different results each run. |
| docker_config | [Docker Config](#docker-config) | Yes | Refer to the [Docker Config](#docker-config) section. |
| enabled | Boolean | No <br> Default: `false` | Should the service be enabled by default? |
| file_required | Boolean | | Does the service require access to the file to perform its task? If set to `false`, the service will only have access to the file metadata (e.g. hashes, size, type, etc.). |
| heuristics | List of [Heuristic](#heuristic) | No | List of heuristic(s) used in the service for scoring. Refer to the [heuristic](#heuristic) section. |
| is_external | Boolean | No <br> Default: `false` | Does the service make API calls to other products not part of the Assemblyline infrastructure (e.g. VirusTotal, ...)? |
| licence_count | Integer | No <br> Default: `0` | Number of concurrent services allowed to run at the same time. |
| name | Keyword | Yes | Name of the service. |
| privileged | Boolean | No <br> Default: `false` | Allow service to have direct access to core for processing. <br>  **Note: Should only be enabled on services that perform static analysis.** |
| rejects | Keyword | No <br> Default: <code>empty&#124;metadata/.\*</code>| Regexes applied to Assemblyline style file type string. For example, <code>empty&#124;metadata/.\*</code> will reject all empty and metadata files. |
| stage | Keyword | No <br> Default: `CORE` | At which stage should the service run. Must be one of: (1) `FILTER`, (2) `EXTRACT`,  (3) `CORE`, (4) `SECONDARY`, (5) `POST`. Note that stages are executed in the numbered order shown. |
| submission_params | List of [Submission Params](#submission-params) | No | List of submission param(s) that define parameters that the user can change about the service for each of its scans. Refer to the [submission_params](#submission-params) section. |
| timeout | Integer | No <br> Default: `60` | Maximum execution time the service has before the task is timed out. |
| update_config | [Update Config](#update-config) | No | Refer to the [update config](#update-config) section. |
| version<sup>1</sup>  | Keyword | Yes | Version of the service.|

<sup>1</sup> the version in the manifest **must** be the same as the image tag in order to successfully pass registration on service update/load.

## Dependency config

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| container | [Docker Config](#docker-config) | Yes | Refer to [Docker Config](#docker-config) section. |
| volumes | Mapping of [Persistent Volume](#persistent-volume) | No | Refer to the [persistent volume](#persistent-volume) section. |

## Docker config

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| allow_internet_access | Boolean | No <br> Default: `false` | Should the container be allowed to access the internet? |
| command | List\[Keyword\] | No | Command that should be run when the container launches. |
| cpu_cores | Float | No <br> Default: `1.0` | Amount of CPU that should be allocated to the container. |
| environment | List of [Environment Variable](#environment-variable)  | No | Refer to the [environment variable](#environment-variable) section.|
| image | Keyword | Yes | Image name always prepended by ${REGISTRY} or ${PRIVATE_REGISTRY} if image not on DockerHub. Append the rest of the image path. Do not put a / between the rest of the image path and registry var. Image name always ends in :$SERVICE_TAG|
| ports | List\[Keyword\] | No | List of ports to bind from the container. |
| ram_mb | Integer | No <br> Default: `1024` | Amount of RAM in MB that should be allocated to the container. |


## Environment variable

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| name | Keyword | Yes | Name of the variable.  |
| value | Keyword | Yes | Value of the variable. |

## Heuristic

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| attack_id | Enum | No | Mitre's Att&ck matrix ID. |
| classification | Classification | No <br> Default: `UNRESTRICTED` | |
| description | Text | Yes | Detailed description of the heuristic which addresses the technique used to score. |
| filetype | Keyword | Yes | Regex of the filetype which applies to this heuristic. |
| heur_id | Keyword | Yes | Unique ID for identifying the heuristic. |
| max_score | Integer | No | The maximum score the heuristic can have. |
| name | Keyword | Yes | Short name for the heuristic. |
| score | Integer | Yes | Score that should be applied when this heuristic is set. |

## Persistent volume

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| mount_path | Keyword | Yes | Path into the container to mount volume. |
| capacity | Keyword | Yes | Storage capacity required in bytes. |
| storage_class | Keyword | Yes | |

## Submission params

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| default | Any | Yes | Default value of the parameter. |
| name | Keyword | Yes | Variable name of the parameter. |
| type | Enum | Yes | Type of variable. Must be one of: `bool`, `int`, `list`, or `str`. |
| value | Any | Yes | Value of the variable as configured by the user or the default if not configured. |

## Update config

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| generates_signatures | Boolean | No <br> Default: `false` | Should the downloaded files be used to create signatures in the system? |
| sources | List of [Update Source](#update-source) | No | List of source(s) from which updates can be downloaded. Refer to the [update source](#update-source) section. |
| update_interval_seconds | Integer | Yes |  Interval in seconds at which the updater runs. |
| wait_for_update | Boolean | False | Should the service wait for its updater dependency to be running? |
| signature_delimiter | Enum | Must be of: `new_line`, `double_new_line`, `pipe`, `comma`, `space`, `none`, `file`, `custom` | Type of delimiter used for signaure downloads. |
| custom_delimiter | Keyword | Optional | Custom signature delimiter to use when `signature_delimiter: custom` |

## Update source

| Field name | Value type | Required? | Description |
|:---|:---|:---|:---|
| headers | List of [Environment Variable](#environment-variable) | No | Refer to the [environment variable](#environment-variable) section. |
| name | Keyword | Yes | Unique name of the source. |
| password | Keyword | No | The password required to access the file. |
| pattern | Keyword | No | Regex pattern to match against the file names of all downloaded files from this source. This is useful when you want to filter out some files from a repo which contains many files. |
| private_key | Keyword | No | Key for accessing file or Git repo. |
| uri | Keyword | Yes | URL of the update file. Some example URL formats are: `git@github.com:sample/sample-repo.git`, `https://file-examples.com/wp-content/uploads/2017/02/zip_2MB.zip`. |
| username | Keyword | No | The username required to access the file. |
