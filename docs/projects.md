---
layout: default
title: Projects
permalink: /Projects
---

This page goes into some of my key projects, showcasing my experience in systems engineering, data optimization, cloud infrastructure, and performance improvement. Each project highlights the challenges faced, the solutions I designed and implemented, and the resulting impact. Please feel free to reach out if you have any questions. Links can be found on my [About page](/about.markdown)

# Projects

*   [Async Push Pull Data Deployment](#async-push-pull)

## <a id="async-push-pull"> Async Push Pull Data Deployment

Led the design and execution of a highly scalable, automated data deployment pipeline that reduced deployment times by 90%.

**The Challenge:** Existing deployments were slow, linear, and required a secondary process to fix any errors, significantly slowing down data releases and prone to breakage. The team needed a reliable, automated solution to accelerate the release cycle and reduce operational overhead.

**The Solution:** I led the design and implementation of a new system using a multi-processing, asynchronous push-pull architecture. Key components included: 1) Master writer synced on writing using locks; 2) 30+ hosts polling for updates; 3) Compression, hashing, and backup functionality; 4) A robust 4-button point in time recovery system with blocking or non-blocking options. The system was designed to download, decompress, verify, and memory-map (mmap) over 400GB of data in under 12 minutes, with network bandwidth as the primary bottleneck.

    Languages: Bash, Python 3, Perl, C++
    Tech: AWS S3, Linux

**Results & Impact:** The new system reduced deployment times by 90%, significantly decreasing entropy by reducing the number of changes required per deployment. This enabled the team to meet new SLAs for client onboarding (adding ASV) and improved operational efficiency.

**What I Liked, Found Challenging and Learned:**

I enjoyed designing the system and the multiprocessing the most. There were also other challenges IE around how to ensure only one deployment is happening at once, how to throttle and also designing the recovery system that was interesting. These same these were what I found most challenging especially around the multiprocessing nature of the thing. I learned a-lot from this. Going in I knew little to nothing of python3 multiprocessing. On the other end of the tunnel I learned I rather enjoy parallel environments and found out when to use mp vs threading vs async in python3. On a side note, trust the docs when they explicitly tell you not to use `terminate()` to kill a proc. VSCode debugger is not that bad to use but multiprocessing race cases are not fun to debug.


## <a id="perl-migration">Perl Apache 2 Migration</a>

Migrated a monolithic Perl/Apache 2 fullstack site to a modern, multiprocess PLACK-based system.

**The Challenge:** The legacy Perl/Apache 2 site was difficult to maintain, scale, and secure. Modernizing the application was critical for performance, stability, and maintainability. The issue was this needed to be done minimally as this was a lift and shift.

**The Solution:** A multiprocess PLACK-based system, adding OAuth2 authentication, operation redo/recovery features, and handling for long-running requests. The migration involved minimal code refactoring and architectural changes.

    Languages: Perl, SQL, HTML, CSS
    Tech: SQL, AWS S3

**Results & Impact:** The new architecture improved scalability, security (through OAuth2), and resilience (with recovery features), significantly reducing operational risk and enhancing the development process.

**What I Liked, Found Challenging and Learned:**

This was my first true lift and shift project. It was nice navigating the MVP again as I had not done that since my time at FITKO. I also learned that while challenging, I do not enjoy perl so much. The most challenging part of the project was not the coding itself or learning the ins and out of the stack. No it was navigating perl 3rd party library docs and their ambiguity and Step 1????Finish aspects. Overall though this project was still fun to work on as I learned more about OAuth, how perl threading behaves (P.S. try not to do it), and why I like working on backend and systems.


## <a id="graphql-cpp-upgrade">GraphQL C++ Service Upgrade</a>

Led and executed an upgrade of a critical GraphQL C++ service's OS, tooling, and standards without service interruption.

**The Challenge:** The service was using outdated tools (clang-tidy, llvm-cov) and compiler standards, hindering development efficiency and potentially causing performance bottlenecks. Upgrading required meticulous planning to avoid downtime. The other challenge was how to tell if any changes affected processing wall time. 

**The Solution:** Over 3-4 months, I designed and led a phased release approach to upgrade the OS (Ubuntu 20 → 22), clang-tidy (10 → 14), llvm-cov (10 → 14), and C++ standard (C++17 → C++20). The upgrade also involved migrating from inheritance to type erasure and adopting vcpkg manifest mode.

    Languages: C++
    Tech: Docker, vcpkg, ECS, ECR, ASG, S3, CMake

**Results & Impact:** The upgrades reduced RTT by ~9% and CPU wall time by ~7%, significantly improving performance. The phased release approach ensured zero downtime.

**What I Liked, Found Challenging and Learned:**

I went into this project knowing little about C++ best practices and containerization. I had some really amazing team members here help me through some of the learning pain points, and my less than optimal naming choices (Sorry again if you ever read this). They were wonderful sound boards for the proposed release plan and when I ran into compilation or build issues. The most challenging part of this project was figuring out where exactly to start from. I knew little of the code base before working on it and muddling through helped me get to the end. I learned so much about containerization best practices, C++, vcpkg and AWS. This project is where I also learned I like infrastructure and full system design which has shaped my current though process when doing any changes.

## <a id="core-dumps">Core Dump S3 Uploads</a>

Implemented automated Core Dump uploading to S3 on multiple ECS services.

**The Challenge:** Debugging production issues was slow due to having to wade through log outputs. Engineers needed faster access to crash information.

**The Solution:** I automated the process of uploading core dumps to S3 upon service crashes. This included creating a step-by-step debugging machine and detailed documentation.

    Languages: Bash
    Tech: CGDB, S3, ECS, ASG

**Results & Impact:** Reduced debug time by 40%, significantly accelerating incident resolution.

**What I Liked, Found Challenging and Learned:**

This project ended up working with containers extensively during testing which I found was the most enjoyable part. It was also nice learning more about what core dumps are, when they are made and where they typically go. The most challenging part of this project was figuring out how a container calls override scripts during stack traces. There were many, this works on my machine, moments before finding the right docs to read through. Overall this project taught me a-lot about lower level aspects of linux, working with cgdb and gdb, and nuances of containerization.

## <a id="statistical-load-testing">Statistical Load Testing Suite</a>

Proposed, led, designed, and executed a repeatable GraphQL statistical load testing suite.

**The Challenge:** Existing load testing lacked rigor and reproducibility, leading to uncertainty during major changes and costly analysis times.

**The Solution:** I built a one-line command to run tests and generate cleaned CSV results. The suite included exploratory and hypothesis testing scripts and leveraged data-driven metrics to reduce decision-making costs and risks.

    Languages: Python 3, Bash
    Modules: Matplotlib, SciPy, NumPy, Pandas, Seaborn, Statsmodels

**Results & Impact:** Reduced major change entropy and cost analysis times by providing data-driven decision metrics.

**What I Liked, Found Challenging and Learned:**

This project was an addon to the [GraphQL C++ Service Upgrade](#graphql-cpp-upgrade) as one of the challenges was being able to say X was faster than Y for foo, bar but not baz. I had fun working on this project as applied statistics can be quite interesting when it is end to end. I ran into some issues regarding load, page limitations and RTT. All of the combined could cause things to slow down to a halt, but had the added benefit of being a load tester for the system as well. This project taught me some of the dos and don'ts of building a semi used tool. It is very easy to build what works for you, but harder to build something that is purposeful, reliant and easy to pick up again. I also realized how nice it is to have data backing a decision. This still shapes my design choices to this day with thinking about what should be stored, monitored and tested.

## <a id="rockdb-endpoint">RockDB Exploration Endpoint</a>

Led and executed the creation of a RockDB exploration GraphQL endpoint.

**The Challenge:** Accessing and debugging data within a RockDB-backed service required significant expertise and was a barrier for less specialized engineers.

**The Solution:** I built a GraphQL endpoint to expose RockDB data, allowing PDs and on-call engineers to debug critical client-facing issues without code owner intervention.

    Languages: C++
    Tech: CMake

**Results & Impact:** Reduced debug time by 70% for critical client issues, empowering more engineers to resolve problems independently.

## <a id="https-api-migration">HTTPS API Migration</a>

Led and executed the migration of a critical HTTPs API endpoint to serverless implementation.

**The Challenge:** The existing endpoint's location was being deprecated due to service and infrastructure changes.

**The Solution:** I migrated the endpoint closer to the service location, enabled automatic cleanup and client notifications.

    Languages: Python 3
    Tech: ASG, Lambda, Parquet, S3, DynamoDB

**Results & Impact:** Reduced processing time by 9%, improving overall RTT for the endpoint.

## <a id="ec2-on-demand">EC2 to On-Demand Migration</a>

Proposed, led, and executed a migration from always-up EC2 instances to on-demand scaling.

**The Challenge:** Always-up EC2 instances were expensive and inefficient.

**The Solution:** I migrated to an on-demand flow using containerization, enabling 1:1 base environments across all stages including local development.

    Tech: Docker, EFS, ECS, EC2, ASG

**Results & Impact:** Reduced cloud costs by 37% and recovery/debug time by 60%.

## <a id="rds-rightsizing">RDS Rightsizing Plan</a>

Proposed, led, and executed an RDS rightsizing plan.

**The Challenge:** RDS instances were overprovisioned and costly.

**The Solution:** I implemented a rightsizing plan without any service interruption or hardware overutilization issues.

    Tech: RDS, Postgres, PgAdmin

**Results & Impact:** Reduced cloud costs by 82% without impacting service availability.

## <a id="monitoring-suite">Comprehensive Monitoring Suite</a>

Designed and implemented a comprehensive monitoring suite.

**The Challenge:** Existing monitoring lacked coverage and insight, leading to delayed detection and slower debugging.

**The Solution:** I identified time series vs. log groups, implemented dashboards in Grafana and Kibana, and increased alerting coverage on 40 metrics.

    Languages: Python 3, Bash, PostgreSQL
    Modules: Matplotlib, NumPy, Pandas
    Tech: Docker, S3, EC2, Kibana, Grafana, Postgres

**Results & Impact:** Increased early alerting coverage by ~30%, decreased debug time by ~50%, and improved data-driven decision-making.

## <a id="qa-testing-suite">Multithreaded QA Suite</a>

Led, Designed and implemented a multithreaded QA testing suite for data changes.

**The Challenge:** ETL pipeline had limited coverage for data sets and required developer intervention to debug and suppress.

**The Solution:** I built a multithreaded suite that allowed for per section QA testing that can be disabled via on-call or PDs. Results are tracked long-term to enable monitoring of trend changes.

    Languages: Python 3, PostgreSQL
    Modules: pyodbc
    Tech: Postgres

**Results & Impact:** Increased QA test coverage for 4 full data sets. 

## <a id="elasticsearch-optimization">Elasticsearch Optimization</a>

Proposed and implemented Elasticsearch index creation optimizations.

**The Challenge:** Elasticsearch indexes consumed excessive RAM and processing time.

**The Solution:** I switched to using streaming generator patterns on data load and index creation time.

    Languages: Python 3
    Tech: Elasticsearch, Postgres

**Results & Impact:** Reduced RAM usage by 60%, processing time by 20%.

## <a id="postgres-optimization">PostgreSQL Optimization</a>

Led optimization of over 20 PostgreSQL functions.

**The Challenge:** A real-time ETL pipeline was bottlenecked by slow PostgreSQL functions.

**The Solution:** Optimize functions using chained CTEs, indexes and lighter patterns. Each query would be audited via EXPLAIN ANALYZE.

    Languages: PostgreSQL, Python 3
    Tech: PgAdmin, RDS

**Results & Impact:** Increased data throughput by up to 15x allowing for enablement of seven new data sets.
