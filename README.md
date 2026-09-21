# GitHub Challenge

<img src="https://octodex.github.com/images/Professortocat_v2.png" align="right" height="200px" />

Hey there!

Your challenge is ready.
Follow the instructions provided for this challenge and complete the required tasks in this repository.

Make sure your work is committed and pushed to your repository before submission.

Good luck!



&copy; 2025 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

# AIOps Monitoring and Event Processing

**Name:** Saharsh Singh
**Roll No:** 202401100100214
**Class:** CS 5C

## Task 1: Setup and Environment

This project monitors a `payment-service`. it detects 
unusual service behaviour and process it as an AIOps event in a simulated python environment.

Main components:

- `service_data.json`: operational data
- `anomaly_detector.py`: anomaly detection
- `event_producer.py`: event producer
- `event_topic.py`: in-memory event topic
- `event_consumer.py`: event consumer
- `aiops_pipeline.py`: complete pipeline
- `tests/`: validation tests

## Task 2: Operational Data Analysis

Metric fields are `response_time_ms`, `cpu_percent`, and `memory_percent`.
Log fields are `log_level` and `message`.


## Task 3: Anomaly Detection

The detector uses these thresholds:

- Response time: greater than `500 ms`
- CPU usage: greater than `80%`
- Memory usage: greater than `80%`
- Log level: `WARNING` or `ERROR`

Two anomalies were detected:

- `10:05`: high response time and an `ERROR` payment timeout log.
- `10:06`: high response time, high CPU, high memory, and an `ERROR` database timeout log.

No expected anomaly was missed and no normal record was incorrectly flagged.

## Task 4: Event-Processing Flow

The workflow is:

```text
Operational Data -> Anomaly Detector -> Producer -> Topic -> Consumer -> AIOps Output
```

The producer publishes anomaly events to the in-memory `anomaly-events` topic.
The consumer reads those events and returns them as the final AIOps output.

## Task 5: Problems Found and Corrected

1. The detector checked only `WARNING`, but the abnormal records used `ERROR`.
	The detector now handles both log levels.
2. The producer and consumer used different topic objects. They now share the
	same `EventTopic` instance.

## Task 6: Final Pipeline Execution

The final execution produced:

```text
Records processed: 10
Anomalies detected: 2
Events consumed: 2
```

The anomaly events were successfully generated, published, consumed, and
processed.

## Task 7: Documentation

This README contains all my supposed changes and findings about this project and the complete working of it to the best of my understanding.

## Task 8: Validation

Run all tests from the repository root:

```bash
PYTHONPATH=.:src python -m pytest -q

Output:
@Saharsh27n ➜ /workspaces/github-skills-challenge (main) $ PYTHONPATH=.:src python -m pytest -q
.........                                                                                                                 [100%]
9 passed in 0.14s
```


The test suite passes successfully.

To run the pipeline directly:

```bash
PYTHONPATH=src python src/aiops_pipeline.py
```

## Task 9: Commit and Submission

I've made the commits of several changes together and will be creating the pull request for final submission in the end after all changes.

## Limitation

The detector capabilities are fully static and does not evolve with the conditions and contraints and set in a fully manual mode.


Reproduce the demonstration:

From the repository root:

```bash
pip install -r requirements.txt
pip install pytest coverage pytest-cov
PYTHONPATH=src python src/aiops_pipeline.py
PYTHONPATH=.:src python -m pytest -q
PYTHONPATH=.:src python -m pytest --cov=src --cov-report=term-missing -q
```

The expected successful result is 10 records processed, 2 anomalies detected, and 2 events consumed.

