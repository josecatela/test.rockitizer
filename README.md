# test.rockitizer - keep your integration tested!  
[![N|Solid](http://www.rockit.consulting/images/logo-fixed.png)](http://www.rockit.consulting)

Easy-to-use junit based framework for the integration testing of any complexity. It is based on record/reply/assert logic and basically compares the current system/interface snapshot with the recorded master results using the numerous predefined or user-defined assertions. Therefore it keeps you informed on any suspicious change of system behavior.

![Lifecycle test.rockitizer](http://www.rockit.consulting/images/github/test_rockitizer_lifecycle.PNG "Lifecycle test.rockitizer;IBM Integration Bus; Integration testing; Test framework;test.rockitizer")

Furthermore, the framework enables the "test first" approach, thus developing against pre-defined "target" interface until the replay snapshot matches.

*Originally developed for ESB, especially for IBM Message Broker/IBM Integration Bus (used in examples), but can be used for any integration platform.* 

## Core features: 
  - declarative `test-plan` concept, [see details](#declarativetestplan)
  - separation of `test-plan` and `connector configuration` concept, [see details](#testdataseparation)
  - extendable connector/plugin architecture
  - `Record`/`Replay with post Assertion` Modes
  - `MQGET`/`MQPUT`, `DBGET`/`DBPUT`, `HTTPGET`, `SCPPUT` connectors available
  - `DB`, `File`, `XMLUnit` assertion plugins
  - regression testing and continuous integration
  
## Skill level
  Basic understanding of following Java frameworks: 
  - Maven - used for build and configuration of runtime and used in example for test project. 
  - Junit - used as test starter
  - XMLUnit - used for assertions
  
  *To run the sample ESB project you will need the basic IBM Integration Bus know-how for import and deployment.


## Main Concepts
According to the maven conventions the following folders of  your test.project are important:
- `src/test/resources/` - location of the test plans
- `src/test/java/` - location of the junit test runner

Junit serves as glue and looks for the test plan with the same name starting its execution from the root folder.
Dependent on mode record/replay it keeps the test outputs in xml format and starts the preconfigured assertions between the recorded and replayed payloads, writing the test protocol to the console. 

For the complete understanding including junit starter and project layout, please refer to  [basic execution flow](docs/USAGE.md#basicexecutionflow)

### <a name="declarativetestplan"></a> Concept of declarative test plan

<img alt="Concept of test data separation from environment configuration" src="docs/img/test_plan_sample.png" width="400"  width="250" align="right"/> 
 	
1. The test plans are folders stored under `src/test/resources/` and must have the same arbitrary name as corresponding junit starter
2. Each **test plan** has one or more test steps (subfolders) with arbitrary names. The `0BEFORE` is an optional and will be automatically executed as first in order to prepare the environment for the test, i.e. clean the DB. 
3. Each **test step** has multiple subfolders (connectors), with the strict naming convention `<ConnectorType>@<ID>`. The `ID` will be looked up in configuration. 
4. All **connectors** processed automatically based on `<ConnectorType>`: PUT/GET i.e.: 
    - MQGET@ - reads all messages in Queue with `<ID>`
    - MQPUT@ - submits the payloads from connector folder into Queue with `<ID>` 

For the test plan reference check [docu](docs/USAGE.md#testplan)


### <a name="testdataseparation"></a> Test data separation from environment configuration

<img alt="Concept of test data separation from environment configuration" src="docs/img/test_data_separation.png" width="450"  width="250" align="right"/> 

The following parts of the test.project supposed to be  environment independent:
- junit starter with assertions
- test-plan with payloads 
- recorded test output (master record)


**That's why they shall be committed in the source repository** and will be shared across users and environments. Write test onces and start it anywhere.  

* replay output is also environment neutral but generated during the test execution, thus not checked in.

All the environment dependent properties belong to the test.project configuration files and basically contain the connector configurations, [see configuration](docs/USAGE.md#configuration).


## Getting started
<img alt="test rockitizer architecture" src="docs/img/architecture_with_dependency_new.png" width="200" height="200" align="right"/>

1. Build the test.rockitizer framework with dependencies, [see framework build instructions](docs/BUILD.md)
2. Create and configure your maven test project having the test.rockitizer as dependency, [see test project configuration](docs/USAGE.md#configuration)
3. Write your test scenario using the step/connector/payload convention [see testplan manual](docs/USAGE.md#testplan)
4. Whrite the JUnit and create the record "master" output [see junit manual](docs/USAGE.md#junit)
5. Reconfigure the test project to replay mode and execute replay with following asssertion



## Examples
[Examples Readme](examples/README.md)



License
----

MIT

