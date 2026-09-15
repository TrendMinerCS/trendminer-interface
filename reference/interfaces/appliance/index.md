# `client.appliance`

## trendminer_interface.\_client.appliance.ApplianceFacade

Facade to TrendMiner appliance information

### get_version

```
get_version() -> str
```

Get the version of the TrendMiner appliance

Returns:

| Name      | Type  | Description                                              |
| --------- | ----- | -------------------------------------------------------- |
| `version` | `str` | Version of the TrendMiner appliance, e.g. "2025.R4.0-12" |

### get_index_resolution

```
get_index_resolution() -> Timedelta
```

Get the index resolution of the TrendMiner appliance

Returns:

| Name         | Type        | Description                                                             |
| ------------ | ----------- | ----------------------------------------------------------------------- |
| `resolution` | `Timedelta` | Index resolution of the TrendMiner appliance, e.g. pd.Timedelta("1min") |

### get_index_horizon

```
get_index_horizon() -> Timestamp
```

Get the index horizon of the TrendMiner appliance

Returns:

| Name      | Type        | Description                                                                                        |
| --------- | ----------- | -------------------------------------------------------------------------------------------------- |
| `horizon` | `Timestamp` | Index horizon of the TrendMiner appliance, i.e. the starting point of the stored time series data. |
