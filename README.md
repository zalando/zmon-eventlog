###ZMON EventLog Service

[![codecov.io](https://codecov.io/github/zalando/zmon-eventlog-service/coverage.svg?branch=master)](https://codecov.io/github/zalando/zmon-eventlog-service?branch=master)


Setup:
psql -d eventlog -f database/eventlog/00_create_schema.sql

.. code-block:: bash

    $ ./mvnw clean install
    $ scm-source -f target/scm-source.json
    $ docker build -t zmon-eventlog-service .

Run with PostgreSQL:
POSTGRESQL_HOST=localhost POSTGRESQL_PORT=5432 POSTGRESQL_DATABASE=test POSTGRESQL_USER= POSTGRESQL_PASSWORD= java -jar target/zmon-eventlog-service-1.0-SNAPSHOT.jar

Create Event:
```
curl -X PUT localhost:8080/ -d "[{\"typeId\":212993, \"time\":\"2014-01-01T20:00:00.000\",\"attributes\":{\"alertId\":1,\"entity\":\"elsn01:5827\"}}]" -H "Content-Type: application/json"
```

Read Event:
```
curl localhost:8080/\?key=alertId\&value=1\&types=212993
```