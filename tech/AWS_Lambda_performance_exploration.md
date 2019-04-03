# AWS Lambda performance exploration
20190403

|The work presented here is done by Intuit Futures team|

As one benefit of a serverless architecture, Lambda has simplified performance tuning for development teams. 
Developers can focus on coding and have less concerns over the conventional performance issues. 
The allocation of the share of CPU time are related to Lambda Memory configuration.

The down side of the autoscaling is what’s called a “cold start”. This occurs when there are no requests incoming for a given Lambda instance, deeming it idle. 
Once an instance idled for awhile, it may be removed to release resources. 
When another request to come in, and all lambda instances are busy, a new Lambda instance will be initialized to serve the request. 
For more information, refer to Concept of cold start section.

In your Lambda code, you can create concurrent or parallel threads. But once the main thread stops, all child threads will be stopped. This is useful since you are charged by how long your function runs for, so you can perform multiple tasks at once.

The performance tests were done on a Lambda that we developed.

- It is triggered by an upstream SQS queue
- It performs a small JSON message transformation
    - JSON transformation takes about 1 ms to complete on an i7 CPU
- Then the new JSON is sent to three downstream SQS queues
    - SQS enqueue operation requires TLS handshake. It requires more CPU time in our test cases. It takes 30 ms on a T2.large EC2 instance
- The downstream SQS publishing is done in three separate promises

The workload that we simulated in this exploration:
- 10 concurrent clients
- Each client sends 1 request per second
- Each message in size is 1.5k bytes
- Test duration: 1 minute

