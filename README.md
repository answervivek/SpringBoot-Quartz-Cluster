# Quartz com Spring Boot Clustered

## Start application

Start by running the application build:

```shell script
mvn clean install
```

Start the application using docker-compose:
```shell script
docker-compose up --build
```

Wait a few seconds and you will see that the application has started, and one of the containers
took over the execution of the job:

```shell script
qtest2_1  | 2020-09-18 16:34:24.021  INFO 8 --- [eduler_Worker-3] com.example.quartz.service.TestService   : Running job on supervisor, job id ATestJob
qtest2_1  | 2020-09-18 16:34:24.021  INFO 8 --- [eduler_Worker-3] com.example.quartz.service.TestService   : Completed job on supervisor, job id ATestJob
qtest2_1  | 2020-09-18 16:34:26.026  INFO 8 --- [eduler_Worker-4] com.example.quartz.job.ATestJob          : ATestJob Running
qtest2_1  | 2020-09-18 16:34:26.026  INFO 8 --- [eduler_Worker-4] com.example.quartz.service.TestService   : Running job on supervisor, job id ATestJob
qtest2_1  | 2020-09-18 16:34:26.026  INFO 8 --- [eduler_Worker-4] com.example.quartz.service.TestService   : Completed job on supervisor, job id ATestJob
qtest2_1  | 2020-09-18 16:34:28.044  INFO 8 --- [eduler_Worker-5] com.example.quartz.job.ATestJob          : ATestJob Running
```

In the example case, we can see that **qtest2_1** took over the execution of the job.

So let's stop this process, use the following script:
```shell script
docker rm -f quartz_qtest2_1
```

Within a few seconds the **qtest1_1** application will take over the execution of the job:
```shell script
qtest1_1  | 2020-09-18 16:36:42.046  INFO 7 --- [duler_Worker-10] com.example.quartz.service.TestService   : Running job on supervisor, job id ATestJob
qtest1_1  | 2020-09-18 16:36:42.046  INFO 7 --- [duler_Worker-10] com.example.quartz.service.TestService   : Completed job on supervisor, job id ATestJob
qtest1_1  | 2020-09-18 16:36:44.032  INFO 7 --- [eduler_Worker-1] com.example.quartz.job.ATestJob          : ATestJob Running
qtest1_1  | 2020-09-18 16:36:44.033  INFO 7 --- [eduler_Worker-1] com.example.quartz.service.TestService   : Running job on supervisor, job id ATestJob
qtest1_1  | 2020-09-18 16:36:44.033  INFO 7 --- [eduler_Worker-1] com.example.quartz.service.TestService   : Completed job on supervisor, job id ATestJob
```

## End execution

To finish the application's execution use Ctrl+C, and to clean the containers, execute:
```shell script
docker-compose rm
```