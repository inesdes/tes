## Mid Task

## A)

### Prerequisite:

* Redshift (https://aws.amazon.com/redshift/free-trial/)
* Required CSV files are in folder `./data`, import into Redshift in three diffrent tables as mentioned below. (Redshift's free trial should be enough for this exercise)


## B) Analyse HTTP Log for User Sessions

### Use Case

Client X would like to find out about the campaign performance for a certain time frame from HTTP log.

A campaign may result in http requests including:

* GET request to `/campaigns/{{id}}`
* POST request to `/rewards/{{id}}` (get a reward issued to the user)

A session window for a user is defined as: within which there's activity for a user (http request for the user) and gap between each activity is less than 5 mins.

Need to provide a report that has following fields:

* user_id
* session_start (timestamp)
* session_end (timestamp)
* campaigns: list of campaigns the user viewd
* rewards_issued: list of rewards the user got issued
* reward_driven_by_campaign_view: true if user got a reward issued after viewing a campaign that contains the reward within the session

### Tasks

1. Create an avro schema for the HTTP log and convert the http log data provided to avro format
2. Load the avro data into a Redshift table
3. Load the campaign and reward mapping csv into a redshift table
4. Do the processing to create the result

#### Data Provided

HTTP log is provided as text file with each line as one entry, it's saved in `data/http_log.txt`. Fields in the log entry are delimited by space with following format:

```
timestamp http_method http_path user_id
```

The following list describes the fields of an access log entry.

* timestamp: iso8601 timestamp (exmaple: `2019-06-01T18:00:00.829+08:00`)
* http_method
* http_path: The http request path
* user_id: User identifier

Mapping of campaign and reward is provided as a csv file in `data/campaign_reward_mapping.csv`.

Campaign and reward is many to many relationship.

### Deliverable

The avro schema needs to be created manually as avsc file. All other tasks need to be encapsulated in a jupyter notebook

Within jupyter notebook, you are free to use any python library.

Even though the provided dataset is small, writing code that can accommodate very large dataset is preferred. Using frameworks like apache beam is encouraged.
