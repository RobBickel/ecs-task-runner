ECS Task Runner
===============

Run a task on ECS and receive output by sending task logs to Cloudwatch Logs and streaming them back to you.

Installation
------------

`npm install ecs-task-runner`

Usage
-----

ECS Task Runner requires an already existing ECS cluster and Task Definition. The Task Definition must send it's logs to AWS Cloudwatch and the ECS hosts will need an IAM role that has permission to do that.

### CLI Tool

To use the cli tool you might want to install ECS Task Runner so the executable is in your path (`npm install -g ecs-task-runner`). Below is the command usage

```
Options:
  --cluster                                                           [required]
  --task-definition                                                   [required]
  --container-name                                                    [required]
  --cmd                                                               [required]
```

#### cluster
The arn of your ECS Cluster

#### task-definition
The arn of your ECS Task Definition

#### container-name
The name of your container in your Task Definition that you want to run this command in

#### cmd
The command you want to run

### Module

```
var ecsTaskRunner = require('ecs-task-runner');

var options = {
  clusterArn: 'xxx',
  taskDefinitionArn: 'xxx',
  containerName: 'xxx',
  cmd: 'echo hello'
};

ecsTaskRunner(options, function(err, stream) {
  if (err) throw err;

  stream.pipe(process.stdout);

  stream.on('error', (err) => {
    throw err;
  });
});
```
