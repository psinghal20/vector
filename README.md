<p align="center">
  <strong><a href="https://vectorproject.io/mailing_list">Join our mailing list!<a/> Simple monthly updates. No spam, ever.</strong>
</p>

<p align="center">
  <img src="./docs/assets/readme_diagram.svg" alt="Vector">
</p>

<p align="center">
  <a href="https://github.com/timberio/vector/releases"><img src="https://img.shields.io/github/release/timberio/vector.svg"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/timberio/vector.svg"></a>
  <a href="https://circleci.com/gh/timberio/vector"><img src="https://circleci.com/gh/timberio/vector/tree/master.svg?style=shield"></a>
  <a href="https://chat.vectorproject.io/badge.svg"><img src="https://chat.vectorproject.io/badge.svg"></a>
</p>

Vector is a [high-performance][performance] observability data router. It makes
[collecting][sources], [transforming][transforms], and [sending][sinks] logs, metrics, and events
easy. It decouples data collection & routing from your services, giving you data ownership and
control, among [many other benefits][use_cases].

Built in [Rust][rust], Vector places high-value on [performance], [correctness], and
[operator friendliness][administration]. It compiles to a single static binary and is designed
to be [deployed][deployment] across your entire infrastructure, serving both as a
light-weight [agent] and a highly efficient [service], making it the single tool you need to
get data from A to B.


## [Documentation](https://docs.vectorproject.io/)

#### About

* [**Use cases**][use_cases]
* [**Concepts**][concepts]
* [**Data model**][data_model]
* [**Guarantees**][guarantees]

#### Setup

* [**Installation**][installation]
* [**Getting started**][getting_started]
* [**Deployment**][deployment] - [topologies], [roles]

#### Usage

* [**Configuration**][configuration] - [sources], [transforms], [sinks]
* [**Administration**][administration] - [cli], [starting], [stopping], [reloading], [updating]
* [**Guides**][guides]

#### Resources

* [**Community**][community] - [forum], [slack chat][slack], [mailing list][mailing_list]
* [**Roadmap**][roadmap] - [vote on new features][vote_feature]

## Features

* ***Fast*** - Built in [Rust][rust], Vector is [fast and memory efficient][performance]. There is no runtime or garbage collector.
* **Correct** - Obsessed with [getting the details right][correctness].
* **Vendor Neutral** - Does not favor a specific storage. Fair, open, with the user's best interest in mind.
* **Agent Or Service** - One simple tool to get data from A to B. Deploys as an [agent] or [service].
* **Logs, Metrics, or Events** - Logs, metrics, and events. Collect, unify, and ship all observability data.
* **Clear Guarantees** - A [guarantee support matrix][guarantees] helps you understand your tradeoffs.
* **Easy To Deploy** - Cross-compiles to a single static binary with no runtime.
* **Hot Reload** - [Reload configuration on the fly][reloading], without skipping a beat.


## Performance

| Test | Vector | Filebeat | FluentBit | FluentD | Logstash | SplunkUF | SplunkHF |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [TCP to Blackhole](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_blackhole_performance) | _**86mib/s**_ | n/a | 64.4mib/s | 27.7mib/s | 40.6mib/s | n/a | n/a |
| [File to TCP](https://github.com/timberio/vector-test-harness/tree/master/cases/file_to_tcp_performance) | _**76.7mib/s**_ | 7.8mib/s | 35mib/s | 26.1mib/s | 3.1mib/s | 40.1mib/s | 39mib/s |
| [Regex Parsing](https://github.com/timberio/vector-test-harness/tree/master/cases/regex_parsing_performance) | 13.2mib/s | n/a | _**20.5mib/s**_ | 2.6mib/s | 4.6mib/s | n/a | 7.8mib/s |
| [TCP to HTTP](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_http_performance) | _**26.7mib/s**_ | n/a | 19.6mib/s | <1mib/s | 2.7mib/s | n/a | n/a |
| [TCP to TCP](https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_tcp_performance) | 69.9mib/s | 5mib/s | 67.1mib/s | 3.9mib/s | 10mib/s | _**70.4mib/s**_ | 7.6mib/s |

To learn more about our performance tests, please see the [Vector test harness][test_harness].


## Correctness

| Test | Vector | Filebeat | FluentBit | FluentD | Logstash | Splunk UF | Splunk HF |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [Disk Buffer Persistence](https://github.com/timberio/vector-test-harness/tree/master/cases/disk_buffer_persistence_correctness) | ✅ | ✅ | ❌ | ❌ | ⚠️* | ✅ | ✅ |
| [File Rotate (create)](https://github.com/timberio/vector-test-harness/tree/master/cases/file_rotate_create_correctness) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| [File Rotate (copytruncate)](https://github.com/timberio/vector-test-harness/tree/master/cases/file_rotate_truncate_correctness) | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ |
| [File Truncation](https://github.com/timberio/vector-test-harness/tree/master/cases/file_truncate_correctness) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| [Process (SIGHUP)](https://github.com/timberio/vector-test-harness/tree/master/cases/sighup_correctness) | ✅ | ❌ | ❌ | ❌ | ⚠️* | ✅ | ✅ |
| [JSON (wrapped)](https://github.com/timberio/vector-test-harness/tree/master/cases/wrapped_json_correctness) | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |

To learn more about our performance tests, please see the [Vector test harness][test_harness].


## Sources

| Name  | Description |
| :---  | :---------- |
| [**`file`**](https://docs.vectorproject.io/usage/configuration/sources/file) | Ingests data through one or more local files and outputs log events.<br />`guarantee: best_effort` |
| [**`statsd`**](https://docs.vectorproject.io/usage/configuration/sources/statsd) | Ingests data through the StatsD UDP protocol and outputs log events.<br />`guarantee: best_effort` |
| [**`stdin`**](https://docs.vectorproject.io/usage/configuration/sources/stdin) | Ingests data through standard input (STDIN) and outputs log events.<br />`guarantee: at_least_once` |
| [**`syslog`**](https://docs.vectorproject.io/usage/configuration/sources/syslog) | Ingests data through the Syslog 5424 protocol and outputs log events.<br />`guarantee: best_effort` |
| [**`tcp`**](https://docs.vectorproject.io/usage/configuration/sources/tcp) | Ingests data through the TCP protocol and outputs log events.<br />`guarantee: best_effort` |
| [**`vector`**](https://docs.vectorproject.io/usage/configuration/sources/vector) | Ingests data through another upstream Vector instance and outputs log events.<br />`guarantee: best_effort` |

[+ request a new source](https://github.com/timberio/vector/issues/new?labels=Type%3A+New+Feature%2C%7B%3Atitle%3D%3E%22New+%60%3Cname%3E%60+source%22%7D&title=New+%60%3Cname%3E%60+source)


## Transforms

| Name  | Description |
| :---  | :---------- |
| [**`add_fields`**](https://docs.vectorproject.io/usage/configuration/transforms/add_fields) | Accepts log events and allows you to add one or more fields. |
| [**`field_filter`**](https://docs.vectorproject.io/usage/configuration/transforms/field_filter) | Accepts log and metric events and allows you to filter events by a field's value. |
| [**`grok_parser`**](https://docs.vectorproject.io/usage/configuration/transforms/grok_parser) | Accepts log events and allows you to parse a field value with Grok. |
| [**`json_parser`**](https://docs.vectorproject.io/usage/configuration/transforms/json_parser) | Accepts log events and allows you to parse a field value as JSON. |
| [**`lua`**](https://docs.vectorproject.io/usage/configuration/transforms/lua) | Accepts log events and allows you to transform events with a full embedded Lua engine. |
| [**`regex_parser`**](https://docs.vectorproject.io/usage/configuration/transforms/regex_parser) | Accepts log events and allows you to parse a field's value with a Regular Expression. |
| [**`remove_fields`**](https://docs.vectorproject.io/usage/configuration/transforms/remove_fields) | Accepts log and metric events and allows you to remove one or more event fields. |
| [**`sampler`**](https://docs.vectorproject.io/usage/configuration/transforms/sampler) | Accepts log events and allows you to sample events with a configurable rate. |
| [**`tokenizer`**](https://docs.vectorproject.io/usage/configuration/transforms/tokenizer) | Accepts log events and allows you to tokenize a field's value by splitting on white space, ignoring special wrapping characters, and zipping the tokens into ordered field names. |

[+ request a new transform](https://github.com/timberio/vector/issues/new?labels=Type%3A+New+Feature%2C%7B%3Atitle%3D%3E%22New+%60%3Cname%3E%60+transform%22%7D&title=New+%60%3Cname%3E%60+transform)


## Sinks

| Name  | Description |
| :---  | :---------- |
| [**`aws_cloudwatch_logs`**](https://docs.vectorproject.io/usage/configuration/sinks/aws_cloudwatch_logs) | Batches and flushes log events to AWS CloudWatch Logs via the `PutLogEvents` API endpoint.<br />`guarantee: at_least_once` |
| [**`aws_kinesis_streams`**](https://docs.vectorproject.io/usage/configuration/sinks/aws_kinesis_streams) | Batches and flushes log events to AWS Kinesis Data Stream via the `PutRecords` API endpoint.<br />`guarantee: at_least_once` |
| [**`aws_s3`**](https://docs.vectorproject.io/usage/configuration/sinks/aws_s3) | Batches and flushes log events to AWS S3 via the `PutObject` API endpoint.<br />`guarantee: at_least_once` |
| [**`blackhole`**](https://docs.vectorproject.io/usage/configuration/sinks/blackhole) | Streams log and metric events to a blackhole that simply discards data, designed for testing and benchmarking purposes.<br />`guarantee: best_effort` |
| [**`console`**](https://docs.vectorproject.io/usage/configuration/sinks/console) | Streams log and metric events to the console, `STDOUT` or `STDERR`.<br />`guarantee: best_effort` |
| [**`elasticsearch`**](https://docs.vectorproject.io/usage/configuration/sinks/elasticsearch) | Batches and flushes log events to Elasticsearch via the `_bulk` API endpoint.<br />`guarantee: best_effort` |
| [**`http`**](https://docs.vectorproject.io/usage/configuration/sinks/http) | Batches and flushes log events to a generic HTTP endpoint.<br />`guarantee: at_least_once` |
| [**`kafka`**](https://docs.vectorproject.io/usage/configuration/sinks/kafka) | Streams log events to Apache Kafka.<br />`guarantee: at_least_once` |
| [**`splunk_hec`**](https://docs.vectorproject.io/usage/configuration/sinks/splunk_hec) | Batches and flushes log events to a Splunk HTTP Event Collector.<br />`guarantee: at_least_once` |
| [**`tcp`**](https://docs.vectorproject.io/usage/configuration/sinks/tcp) | Streams log events to a TCP connection.<br />`guarantee: best_effort` |
| [**`vector`**](https://docs.vectorproject.io/usage/configuration/sinks/vector) | Streams log events to another downstream Vector instance.<br />`guarantee: best_effort` |

[+ request a new sink](https://github.com/timberio/vector/issues/new?labels=Type%3A+New+Feature%2C%7B%3Atitle%3D%3E%22New+%60%3Cname%3E%60+sink%22%7D&title=New+%60%3Cname%3E%60+sink)


## License

Copyright 2019, Vector Authors. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use these files except in compliance with the License. You may obtain a copy
of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations under
the License.

---

<p align="center">
  Developed with ❤️ by <strong><a href="https://timber.io">Timber.io</a></strong>
</p>

[administration]: https://docs.vectorproject.io/usage/administration
[agent]: https://docs.vectorproject.io/setup/deployment/roles/agent
[backups]: https://docs.vectorproject.io/about/use_cases/backups
[cli]: https://docs.vectorproject.io/administration/cli
[community]: https://vectorproject.io/community/
[configuration]: https://docs.vectorproject.io/usage/configuration
[concepts]: https://docs.vectorproject.io/about/concepts
[cost]: https://docs.vectorproject.io/about/use_cases/cost
[correctness]: https://docs.vectorproject.io/comparisons
[data_model]: https://docs.vectorproject.io/about/data_model
[deployment]: https://docs.vectorproject.io/setup/deployment
[forum]: https://forum.vectorproject.io
[getting_started]: https://docs.vectorproject.io/setup/getting_started
[governance]: https://docs.vectorproject.io/about/use_cases/governance
[guarantees]: https://docs.vectorproject.io/about/guarantees
[guides]: https://docs.vectorproject.io/usage/guides
[installation]: https://docs.vectorproject.io/setup/installation
[lock-in]: https://docs.vectorproject.io/about/use_cases/lock-in
[mailing_list]: https://vectorproject.io/mailing_list
[multi-cloud]: https://docs.vectorproject.io/about/use_cases/multi-cloud
[performance]: https://docs.vectorproject.io/performance
[releases]: https://github.com/timberio/vector/releases
[reloading]: https://docs.vectorproject.io/usage/administration/reloading
[roadmap]: https://github.com/timberio/vector/milestones?direction=asc&sort=title&state=open
[roles]: https://docs.vectorproject.io/setup/deployment/roles
[rust]: https://www.rust-lang.org/
[security]: https://docs.vectorproject.io/about/use_cases/security-and-compliance
[service]: https://docs.vectorproject.io/setup/deployment/roles/service
[sinks]: https://docs.vectorproject.io/usage/configuration/sinks
[slack]: https://chat.vectorproject.io
[sources]: https://docs.vectorproject.io/usage/configuration/sources
[starting]: https://docs.vectorproject.io/usage/administration/starting
[stopping]: https://docs.vectorproject.io/usage/administration/stopping
[test_harness]: https://github.com/timberio/vector-test-harness
[test_harness_how_it_works]: https://github.com/timberio/vector-test-harness#how-it-works
[topologies]: https://docs.vectorproject.io/setup/deployment/topologies
[transforms]: https://docs.vectorproject.io/usage/configuration/transforms
[updating]: https://docs.vectorproject.io/usage/administration/updating
[use_cases]: https://docs.vectorproject.io/use_cases
[vote_feature]: https://github.com/timberio/vector/issues?q=is%3Aissue+is%3Aopen+sort%3Areactions-%2B1-desc+label%3A%22Type%3A+New+Feature%22