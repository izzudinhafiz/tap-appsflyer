# singer-tap-appsflyer

This is a fork of [Singer](https://singer.io) [tap-appsflyer](https://github.com/singer-io/tap-appsflyer) tap that produces JSON-formatted data following the [Singer spec](https://github.com/singer-io/getting-started/blob/master/SPEC.md).

This tap:
- Pulls raw data from AppFlyer's [Raw Data Reports V5 API](https://support.appsflyer.com/hc/en-us/articles/208387843-Raw-Data-Reports-V5-)
- Outputs the schema for each resource
- Incrementally pulls data based on the input state

# Config

## Sample config
```json
{
    "app_id": "string",                     # required
    "api_token": "string",                  # required
    "start_date": "2022-01-01T00:00:00Z",   # optional
}
```

| Key              | Type   | Value                                              | Required |
| ---------------- | ------ | -------------------------------------------------- | -------- |
| app_id           | string | Application id                                     | True     |
| api_token        | string | Appsflyer API token                                | True     |
| start_date       | string | "%Y-%m-%dT%H:%M:%SZ" format                        | False    |
| organic_installs | bool   | true -> Downloads organic installs event           | False    |
| table_prefix     | string | rename stream from 'installs' to 'table_installs'  | False    |
| schema_prefix    | string | rename stream from 'installs' to 'schema-installs' | False    |

## Notes
- `table_prefix` and `schema_prefix` useful for renaming stream to be used by a postgres target, such as the [pipelinewise-target-postgres](https://github.com/transferwise/pipelinewise-target-postgres) and used with `schema_mapping`
- `start_date` is a suggestion. Actual start date will depend on data availability from Appsflyer. See [data availability window](https://support.appsflyer.com/hc/en-us/articles/4415473374865-Raw-data-availability-window).
- Be careful of [rate limit](https://support.appsflyer.com/hc/en-us/articles/207034366-API-Policy) for the pull API
- End date is always `datetime.now()`

---

Copyright &copy; 2017 Stitch, Inc. & Izzudin Hafiz