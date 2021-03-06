# Value Functions

## Overview

This document describes functions, which can be referenced in the `value` setting in order to calculate values of a derived series.

The `value` setting is specified by the `series` section.

```ls
# Define the original series, which values will be used in creating a derived (computed) series.
# The original series must exist in the database
[series]
  metric = cpu_busy
  entity = nurswgvml007
  # Specify an alias so that the derived series can refer to the original series by name
  alias = s-1
  # Optionally, hide the original series, so that only the derived series is displayed
  display = false

# Define the derived series by specifying an expression in the "value" setting
[series]
  label = My New Series
  # Specify an expression that will be called for each "time:value" sample in the original series
  value = 2 * value("s-1")
```

[ChartLab Example](https://apps.axibase.com/chartlab/ae6323aa)

The expression specified in the `value` setting is invoked for each "time:value" sample in the original series. The expression must return a numeric value or null of the value cannot be calculated.

## Lookup Functions

| Function | Arguments | Description |
|----------|-----------|-------------|
| value | alias | Value of the series at the current timesamp. |
| previous | alias, count | Value of series `count` samples ago. |
| time |  | Timestamp in Unix milliseconds for which the expression is invoked. |

## Statistical Functions

| Function | Arguments | Description |
|----------|-----------|-------------|
| movavg | alias, count, minCount | Average value of `count` last samples. If `minCount` parameter is specified, the function returns `null` unless the number of samples exceeds this parameter. |
| percentile | percentage, alias, period |  Value, which is greater than the `percentage` of samples in the current `period`.  |
| max<br>maximun | alias, period | Maximum in the current `period`. |
| min<br>minimum | alias, period | Minimum in the current `period`. |
| avg<br>average | alias, period | Average in the current `period`. |
| sum | alias, period | Sum of values in the current `period`. |
| delta | alias, period | Difference between last values of the current and previous periods. |
| counter | alias, period  | Sum of positive differences between subsequent values in the current period. |
| count | alias, period | Number of samples in the current `period`. |
| last | alias, period | Value of the last sample. in the current period. |
| first | alias, period | Value of the first sample in the current period. |
| min_value_time | alias, period | Timestamp of the maximum value in the current period. |
| max_value_time | alias, period | Timestamp of the minimum value in the current period. |
| median | alias, period | Same as `percentile(50)`. |

## Ranking Functions

| Function | Arguments | Description |
|----------|-----------|-------------|
| bottom | rank, getValue | Sort current values in increasing order and return the position index (1 = smallest). |
| top | rank, getValue | Sort current values in decreasing order and return the position index (1 = largest). |

## Metadata Functions

| Function | Arguments | Description |
|----------|-----------|-------------|
| meta | alias | Metadata object. |
| entityTag | alias, tagName | Entity tag. |
| metricTag | alias, tagName | Metric tag. |

