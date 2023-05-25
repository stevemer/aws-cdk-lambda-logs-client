# AWS CDK Lambda Logs Client
Simpler Cloudwatch logs access for AWS CDK stacks.

Using AWS CDK to manage Lambda means your Lambda instance continually changes, and so does the log group you need to watch. This script wraps the AWS client to look up (by prefix) the log group with the most recent logging activity, while still supporting reasonable search, filter and time-window operations. 

This script is not packaged as a library, because your CDK setup will affect the formatting of the prefix used for lookup. The current format is appropriate for my stack.

## Usage

- Basic

- Watch
    ```sh
    # Watch all log events from most recently active log group,
    # for production environment that matches prefix thingservice
    ./log2 watch prod thingservice

    # Same as above, but filter for "error"
    ./log2 watch prod thingservice --filter error
    ```

- Get
    ```sh

    # Get all log events from most recently active log group,
    # for production environment that matches prefix thingservice
    # over the last 2 hours
    ./log2 get prod thingservice --start -2h

    # Same as above, but filter for "error"
    ./log2 get prod thingservice --start -2h --filter error

    # Same as above, but instead, filter for "bobby", to find all events for bobby@mail.com
    ./log2 get prod thingservice --start -2h --filter bobby

    # Same as above, but instead, filter for "bobby" and strip out all lines with "frank"
    ./log2 get prod thingservice --start -2h --filter "bobby -frank"

    # Same as above, but get activity from 2022-03-20 until 2022-03-23 
    ./log2 get prod thingservice --start 2022-03-20 --stop 2022-03-23 --filter error
    ```
