# Simple Worker that can process DMN as part of Zeebe Workflows
Zeebe task worker for DMN. It uses the Camunda DMN to evaluate decisions. The decisions are read from local directory.

* register for tasks of type 'DMN'
* required task header 'decisionRef' => id of the decision to evaluate
* completes task with payload 'dmn-result' which contains the complete decision result

```xml
<bpmn:serviceTask id="decisionTask" name="Eval DMN decision">
  <bpmn:extensionElements>
    <zeebe:taskDefinition type="DMN" />
    <zeebe:taskHeaders>
      <zeebe:header key="decisionRef" value="dish-decision" />
    </zeebe:taskHeaders>
    <zeebe:ioMapping>
      <zeebe:output source="$.result" target="$.decisionResult" />
    </zeebe:ioMapping>
  </bpmn:extensionElements>
</bpmn:serviceTask>
```

## How to build

Build with Maven

`mvn clean install`

## How to run

Execute the JAR file via

`java -jar zeebe-dmn.jar`

## How to configure

You can provide a properties file `application.properties` to configure the Zeebe client and the DMN task worker.

```
# DMN task worker
dmn.models.dir=my-dmn-models                        # default: models
# Zeebe Client
```

## Code of Conduct

This project adheres to the Contributor Covenant [Code of
Conduct](/CODE_OF_CONDUCT.md). By participating, you are expected to uphold
this code. Please report unacceptable behavior to
code-of-conduct@zeebe.io.
