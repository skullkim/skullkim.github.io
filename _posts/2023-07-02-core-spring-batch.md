---
layout:       post
title:        "spring batch Job과 Step 설정하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
- Spring
---

스프링 배치에서 Job과 Step을 설정할 떄 설정할 수 있는 다양한 옵션들을 살펴보겠습니다.
# Job 설정하기
## 재시작여부
Job은 기본적으로 재시작 가능하지만, 재시작이 불필요하다면 재시작을 비활성화 할 수 있습니다. Job은 기본적으로 처음 시작하면 Job instance가 생성되고, 해당 job instance를 여러번 시작하면 시작 횟수만큼 job execution이 생성됩니다. 만약 재시작을 바활성화 한다면 하나의 Job instance에 대해 한 번만 job을 시작할 수 있습니다. 
```java
@Bean
public Job job() {
    return jobBuilderFactory.get("job prevent restart")
            .preventRestart() // 재시작 방지
            .start(decompress())
            .next(readWrite())
            .next(cleanTasklet())
            .build();
}
```
따라서 해당 재시작 방지를 한 뒤 해당 job 플로우를 여러번 실행해야 한다면 서로 다른 job instance를 만들어 주어야 합니다. 이를 위해선 get() 메서드의 파라미터인 job의 이름을 바꾸어주면 됩니다. 그 이유는 스프링 배치에서 JobLauncher의 구현체로 제공하는 SimpleJobLauncher가 job 이름과 job 파라미터로 job instance 존재 여부를 판단하기 때문입니다.
```java
package org.springframework.batch.core.launch.support;
public class SimpleJobLauncher implements JobLauncher, InitializingBean {

    ...

    @Override
	public JobExecution run(final Job job, final JobParameters jobParameters)
			throws JobExecutionAlreadyRunningException, JobRestartException, JobInstanceAlreadyCompleteException,
			JobParametersInvalidException {
                Assert.notNull(job, "The Job must not be null.");
		Assert.notNull(jobParameters, "The JobParameters must not be null.");

		final JobExecution jobExecution;
		JobExecution lastExecution = jobRepository.getLastJobExecution(job.getName(), jobParameters);
		if (lastExecution != null) {
			if (!job.isRestartable()) {
				throw new JobRestartException("JobInstance already exists and is not restartable");
			}

            ...
        }
        ...
    }
}
```
## JobExecution 인터셉팅
만약 어떤 job 실행 전후에 code를 실행하고 싶다면 JobListener를 사용하면 됩니다. JobListene는 JobExecutionListener를 implements하여 구현하거나 @BeforeJob, @AfterJob 어노테이션을 사용해 구현할 수 있습니다.
JobExecutionListener를 사용한 방식은 다음과 같습니다.
```java
// SampleListener.java
@Slf4j
public class SampleListener implements JobExecutionListener {

    @Override
    public void beforeJob(final JobExecution jobExecution) {
        log.info("before job");
    }

    @Override
    public void afterJob(final JobExecution jobExecution) {
        log.info("after job");
    }
}

// LinearFlowJob.java
@Slf4j
@EnableBatchProcessing
@Configuration
public class LinearFlowJob {

    ...

    @Bean
    public Job job() {
        return jobBuilderFactory.get("simple job")
                .listener(sampleListener())
                .start(decompress())
                .next(readWrite())
                .next(cleanTasklet())
                .build();
    }

    @Bean
    public JobExecutionListener sampleListener() {
        return new SampleListener();
    }

    ...
}
```
어노테이션을 사용한 방식은 다음과 같습니다.
```java
// SampleListener.java
@Slf4j
public class SampleListener {

    @BeforeJob
    public void beforeJob(final JobExecution jobExecution) {
        log.info("before job");
    }

    @AfterJob
    public void afterJob(final JobExecution jobExecution) {
        log.info("after job");
    }
}

// LinearFlowJob.java
@Slf4j
@EnableBatchProcessing
@Configuration
public class LinearFlowJob {

    ...

     @Bean
    public Job job() {
        return jobBuilderFactory.get("simple job")
                .listener(sampleListener())
                .start(decompress())
                .next(readWrite())
                .next(cleanTasklet())
                .build();
    }

    @Bean
    public JobExecutionListener sampleListener() {
        return JobListenerFactoryBean.getListener(new SampleListener());
    }

    ...
}
```
JobListener사용 시 주의할 점이 하나 있습니다. afterJob() 메서드는 job의 성공, 실패와 상관 없이 실행됩니다. 따라서 Job 실행 결과에 따라 로직을 나누고 싶다면 다음과 같이 afterJob을 구현해야 합니다.
```java
public void afterJob(JobExecution jobExecution){
    if (jobExecution.getStatus() == BatchStatus.COMPLETED ) {
        //job success
    }
    else if (jobExecution.getStatus() == BatchStatus.FAILED) {
        //job failure
    }
}
```
## JobParametersValidator
만약 JobParameter에 대한 검증을 해야 한다면 JobParametersValidator를 implement해서 원하는 검증을 진행할 수 있습니다.
```java
// LocalDateParameterValidator.java
public class LocalDateParameterValidator implements JobParametersValidator {

    private final String parameterName;

    public LocalDateParameterValidator(final String parameterName) {
        this.parameterName = parameterName;
    }

    @Override
    public void validate(final JobParameters parameters) throws JobParametersInvalidException {
        try {
            assert parameters != null;
            LocalDate.parse(Objects.requireNonNull(parameters.getString(parameterName)));
        } catch (DateTimeParseException | NullPointerException e) {
            throw new JobParametersInvalidException(parameterName + " parameter 가 날짜 형식이 아닙니다.");
        }
    }
}

// LinearFlowJob.java
@Slf4j
@EnableBatchProcessing
@Configuration
public class LinearFlowJob {

    ...

    @Bean
    public Job job() {
        return jobBuilderFactory.get("simple job")
                .validator(new LocalDateParameterValidator("date"))
                .start(decompress())
                .next(readWrite())
                .next(cleanTasklet())
                .build();
    }

    ...
}
```
## Java Configuration
Spring 3 이전까지는 스프링 배치 설정을 XML로 했습니다. Spring 3이후 자바를 사용한 설정 방식이 도입되면서 @EnableBatchProcessing 어노테이션을 사용할 수 있게 되었습니다. @EnableBatchProcessing은 다음과 같은 기본 설정들을 제공합니다.
- StepScope과 JobScope 인스턴스를 하나씩 생성합니다.
- 다음과 같은 빈들을 autowired 합니다.
  - JobRepository
  - JobLauncher
  - JobRegistry
  - JobExplorer
  - JobOperator
- DataSource와 PlatformTransactionManager가 컨텍스트 내에서 사용되는데 각각 dataSource, transactionManger라는 이름으로 제공됩니다. 만약 이 빈들에 대한 설정을 바꾸고 싶다면 @EnableBatchProcessing 어노테이션의 attribute를 사용하면 됩니다. 다만, 이 기능은 spring batch v5부터 제공되며 spring batch v5는 spring6를 필요로 합니다.

커스텀 DataSource와 TransactionManager를 사용 방법은 다음과 같습니다.
```java
@Configuration
@EnableBatchProcessing(dataSourceRef = "batchDataSource", transactionManagerRef = "batchTransactionManager")
public class MyJobConfiguration {

	@Bean
	public DataSource batchDataSource() {
		return new EmbeddedDatabaseBuilder().setType(EmbeddedDatabaseType.HSQL)
				.addScript("/org/springframework/batch/core/schema-hsqldb.sql")
				.generateUniqueName(true).build();
	}

	@Bean
	public JdbcTransactionManager batchTransactionManager(DataSource dataSource) {
		return new JdbcTransactionManager(dataSource);
	}

	public Job job(JobRepository jobRepository) {
		return new JobBuilder("myJob", jobRepository)
				//define job flow as needed
				.build();
	}

}
```
spring batch v5부터는 @EnableBatchProcessing 대신 DefaultBatchConfiguration class를 extends해서 사용할 수도 있습니다. 이 클래스는 @EnableBatchProcessing하고 같은 빈들을 제공합니다. 사용 방법은 다음과 같습니다.
```java
@Configuration
class MyJobConfiguration extends DefaultBatchConfiguration {

	@Bean
	public Job job(JobRepository jobRepository) {
		return new JobBuilder("job", jobRepository)
				// define job flow as needed
				.build();
	}

}
```
## JobRepository에 관한 설정들
JobRepository는 스프링 배치와 관련된 영속화된 도메인 객체들에 대해 CRUD 연산을 수행할 때 사용됩니다. 이런 도메인 객체로는 JobExecution, StepExecution 등이 있습니다. 만약 @EnableBatchProcessing 어노테이션을 사용한다면 JobRepositor는 기본으로 제공됩니다.
### JobRepository 트랜잭션 설정
만약 스프링 배치가 제공하는 FactoryBean을 사용한다면 트랜잭션 advice는 자동으로 생성됩니다. 이를 통해 배치 데이터가 올바르게 유지되게 해서 실패 후 재시작 등을 가능하게 합니다. 
JobRepository 내의 create* 메서드에 대한 격리 레벨은 두 프로세스가 동시게 같은 job을 실행하려 할 때 하나만 성공하도록 보장합니다. 기본 격리 레벨은 SERIALIZABLE이지만 create* 메서드에 대한 호출이 짧기 때문에 SERIALIZABLE로 인한 큰 문제를 발생하지 않습니다. 만약 이 격리 레벨을 바꾸고 싶다면 다음과 같이 @EnableBatchProcessing의 attribute를 사용하면 됩니다(spring batch v5 부터).
```java
@Configuration
@EnableBatchProcessing(isolationLevelForCreate = "ISOLATION_REPEATABLE_READ")
public class MyJobConfiguration {

   // job definition

}
```
### Table prefix 변경
스프링 배치에 사용되는 테이블들의 prefix는 모두 'BATCH_'입니다. 이 prefix를 바꾸고 싶을 경우 다음과 같은 방법을 사용하면 됩니다.
```java
@Configuration
@EnableBatchProcessing(tablePrefix = "SYSTEM.TEST_")
public class MyJobConfiguration {

   // job definition

}
```
## JobLauncher 설정
만약 