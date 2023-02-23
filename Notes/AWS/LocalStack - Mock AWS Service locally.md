## Localstack 

To start the localstack container, save the below code as `docker-compose.yml` and run `docker-compose up` command in the directory where the file is saved. Once the container is up and running, you can access the AWS services using `localhost:4566` endpoint.

```yaml
version: '3.2'
services:
  localstack:
    image: localstack/localstack:0.10.6
    container_name: localstack_demo
    ports:
      - '4563-4599:4563-4599'
      - '8082:8080'
    environment:
      - SERVICES=s3:4566,lambda,dynamodb,apigateway,ses,sns,sqs
      - DEBUG=1
      - HOSTNAME_EXTERNAL=localhost
      - LAMBDA_EXECUTOR=docker 
      - DOCKER_HOST=unix:///var/run/docker.sock
      - DATA_DIR=/tmp/localstack/data
      - AWS_DEFAULT_REGION=us-east-1
      - AWS_SECRET_ACCESS_KEY=dummy
      - AWS_ACCESS_KEY_ID=dummy
    volumes:
      - './.localstack:/tmp/localstack'
      - '/var/run/docker.sock:/var/run/docker.sock'
```

**Environment Variables**
- `SERVICES` : Specifies which AWS services Localstack should simulate
- `DEBUG=1` : Enables debug mode
- `DATA_DIR` : Specifies where localstack will create temp files
- `LAMBDA_EXECUTOR` : Specifies the Lambda executor to use when running Lambda functions in Localstack (python, docker, local). `docker` runs lambda function as separate docker container (For this we have to specify DOCKER_HOST)
- `DOCKER_HOST` : Specifies the location of the Docker host that the Localstack container should communicate with. We can share the docker host of the host machine by setting this path and mapping the volume of host docker engine to this path
- `/var/run/docker.sock` : Socket where docker daemon is listening. Docker daemon is like a backend server which is listening to front end client and performs tasks related to docker

**AWS CLI**
- Use `awslocal` or with aws cli use `aws --endpoint-url http://localhost:4566`

**Spring Boot**

- AWS sdk dependency
```xml
<dependency>
<groupId>com.amazonaws</groupId>
<artifactId>aws-java-sdk-s3</artifactId>
<version>1.11.761</version>
</dependency>
```

- Basic S3 configuration
```java
@Configuration
public class S3Config {

    @Value("${amazon.aws.accesskey}")
    private String amazonAWSAccessKey;

    @Value("${amazon.aws.secretkey}")
    private String amazonAWSSecretKey;

    @Value("${amazon.aws.region}")
    private String amazonAWSRegion;

    @Value("${amazon.aws.endpoint}")
    private String endpointUrl; // http://localhost:4566

    @Bean
    public AmazonS3 s3Client(){
        AwsClientBuilder.EndpointConfiguration endpointConfiguration 
        = new AwsClientBuilder.EndpointConfiguration(endpointUrl,
                amazonAWSRegion);

        return AmazonS3ClientBuilder
                .standard()
                .withEndpointConfiguration(endpointConfiguration)
                .withCredentials(new AWSStaticCredentialsProvider(amazonAWSCredentials()))
                .withPathStyleAccessEnabled(true)
                //.withRegion(amazonAWSRegion)
                .build();
    }

    @Bean
    public AWSCredentials amazonAWSCredentials() {
        return new BasicAWSCredentials(
                amazonAWSAccessKey, amazonAWSSecretKey);
    }
}
```