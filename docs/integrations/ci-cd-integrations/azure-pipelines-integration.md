# Azure Pipelines integration

## Overview of Azure Pipelines integration

Snyk enables security across the Microsoft Azure ecosystem including for Azure Pipelines by automatically finding and fixing application and container vulnerabilities.

Ready-to-use tasks for Azure Pipelines can be inserted quickly and directly from the Azure interface, enabling you to customize and automate your pipelines with no extra coding. Among the tasks included is the Snyk task.

You can include the Snyk task in your pipeline to test for security vulnerabilities and licensing issues as part of your routine work. In this way you can test and monitor your application dependencies and container images for security vulnerabilities. When the testing is done you can review and work with results directly from the Azure Pipelines output, as well as from the Snyk interface.

The Snyk Security Scan task is available for all languages supported by Snyk and Azure DevOps.

### Custom API Endpoints

By default, the task uses the [https://snyk.io/api](https://snyk.io/api) endpoint. It is possible to configure Snyk to use a different endpoint by set a `SNYK_API` environment variable in the pipeline:

![](<../../.gitbook/assets/Screenshot 2022-07-22 at 17.36.54.png>)

Please refer to the [Snyk documentation](https://docs.snyk.io/snyk-cli/configure-the-snyk-cli#configuration-to-connect-to-the-snyk-api) for more information about environment configuration.

### **Example of a Snyk task to test a node.js (npm) based application**

This section shows examples of Snyk Security Scan task configurations and parameters for testing a Node.js (npm) application.

The configuration panel appears as follows:

![Snyk Security Scan configuration panel](../../.gitbook/assets/mceclip0-24-.png)

Click **add** and the task is added to your pipeline as follows:

![Snyk Security Scan task added to a pipeline](../../.gitbook/assets/mceclip1-15-.png)

### **Simple example of testing an application**

```
- task: SnykSecurityScan@0
  inputs:
    serviceConnectionEndpoint: 'snykToken'
    testType: 'app'
    monitorWhen: 'always'
    failOnIssues: true
```

### **Example of a Snyk task for a container image pipeline**

The following is an example of the Snyk Security Scan task within the script for a container image pipeline.

When populated with the most common settings, the configuration panel in Azure looks much like the following:

![](../../.gitbook/assets/mceclip2-5-.png)

The following is an example of the same configuration once you've added it to your pipeline.

![](../../.gitbook/assets/mceclip3-1-.png)

### **Simple example of testing a container image**

```
- task: SnykSecurityScan@1
  inputs:
    serviceConnectionEndpoint: 'snykToken'
    testType: 'container'
    dockerImageName: 'goof'
    dockerfilePath: 'Dockerfile'
    monitorWhen: 'always'
    failOnIssues: true
```