# Instances

* [List Your Instances](#list-your-instances)
* [Get Instance Detail](#get-instance-detail)
* [Edit Instance](#edit-instance)
* [Run Instance](#run-instance)
* [List the Tasks of Instance](#list-the-tasks-of-instance)
* [Get Task Detail](#get-task-detail)

## List Your Instances

List instances created by authenticated user.

    GET /instances

### Parameters

| Name     | Type     | Required | Description                              | Default |
| -------- | -------- | -------- | ---------------------------------------- | ------- |
| `status` | `string` | `false`  | Can be one of: `all`, `running` or `idle` | `all`   |

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": [
        {
          "id": "instance id",
          "title": "instance title",
          "status": "idle/error/running",
          "createdAt": 1492593196000,
          "totalExecution": 1,
          "totalFetchingRows": 1
        }
      ],
      "msg": ""
    }

## Get Instance Detail 

Get detail of single instance.

    GET /instance/:instance_id

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": {
        "id": "instance id",
        "title": "instance title",
        "status": "idle/error/running",
        "createdAt": 1494844957000,
        "totalExecution": 1,
        "totalFetchingRows": 1
      },
      "msg": ""
    }


## Get the Schema of Instance

Get the latest schema of instance.

    GET /instance/:instance_id/schema

### Response 

    Status: 200 OK

    {
        "code": 0,
        "data": {
            "schemas": [
                {
                    "title": "name",
                    "id": "C339",
                    "type": "string"
                },
                {
                    "title": "class",
                    "id": "C337",
                    "type": "string"
                },
                {
                    "title": "ID",
                    "id": "C341",
                    "type": "string"
                },
            ]
        },
        "msg": ""
    }

## Edit Instance

Edit meta-data and configuration of instance.

    PATCH /instance/:instance_id

### Parameters

| Name                | Type     | Required | Description                          | Default |
| ------------------- | -------- | -------- | ------------------------------------ | ------- |
| `title`             | `string` | `false`  | The title of instance                | `null`  |
| `result_notify_uri` | `string` | `false`  | The result notification webhook uri. | `null`  |

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": null,
      "msg": ""
    }

## Run Instance 

Run instance with optional configurations.

    POST /instance/:instance_id

### Parameters

| Name                | Type           | Required | Description                          | Default                        |
| ------------------- | -------------- | -------- | ------------------------------------ | ------------------------------ |
| `target_sources`    | `object array` | `false`  | Crawl & Parse target config.         | `[{"urls": [${DEFAULT_URL}]}]` |
| `result_notify_uri` | `string`       | `false`  | The result notification webhook uri. | `null`                         |

#### Example

To run a instance, you can set up the crawl & parse target by `target_source` whose object contains the following fields:

| Name      | Type     | Required | Description                              | Default            |
| --------- | -------- | -------- | ---------------------------------------- | ------------------ |
| `urls`    | `array`  | `false`  |                                          | `[${DEFAULT_URL}]` |
| `method`  | `string` | `false`  | HTTP method                              | `GET`              |
| `headers` | `object` | `false`  | Key/value pairs for `HTTP Request Headers` | `null`             |

Default URL rule you set in [Dashboard](https://dashboard.zaoshu.io) will be used when field `urls` found omitted.

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": {
          "taskID":"8d9709b7ab024fa3b1f6b0e474fc56b0"
      },
      "msg": ""
    }

## List the Tasks of Instance 

List all tasks of specific instance.

    GET /instance/:instance_id/tasks

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": [
        {
          "id": "task id",
          "status": "done/error",
          "createdAt": 1494810771000
        }
      ],
      "msg": ""
    }

## Get Task Detail 

Get detial of single task.

    GET /instance/:instance_id/task/:task_id

### Response

    Status: 200 OK

    {
      "code": 0,
      "data": {
        "id": "task id",
        "status": "done/error",
        "createdAt": 1494810771000,
        "totalUrlCount": 1,
        "failedUrlCount": 0
      },
      "msg": ""
    }
