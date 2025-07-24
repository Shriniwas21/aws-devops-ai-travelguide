# Lab 5: Monitor Application with CloudWatch Anomaly Detection – TravelGuideAI

## ✅ Objective
- Enable anomaly detection for a custom metric in CloudWatch.
- Configure an alarm to trigger when values go outside expected ranges.
- Use AWS CLI and Python script to retrieve and post custom metrics.

---

## Task 1: Create Anomaly Detection Alarm

- Navigated to **CloudWatch > Metrics > TravelApplication > Metrics with no dimensions**
- Selected `UserLogins` metric
- Enabled anomaly detection
- Created alarm: `logins-alarm` (based on anomaly band, no static threshold)
- Observation: Initial state `Insufficient data`, changes to `In Alarm` after training

### 📸 Screenshots:
- `cloudwatch-enable-anomaly.png`, `cloudwatch-create-alarm.png`, `logins-metric-graph.png`

---

## Task 2: Retrieve Alarm & Metrics with AWS CLI

- Viewed anomaly detectors:
  ```bash
  aws cloudwatch describe-anomaly-detectors
  ```

- Described alarm metric settings:
  ```bash
  aws cloudwatch describe-alarms --alarm-names logins-alarm --query MetricAlarms[0].Metrics
  ```

- Retrieved anomaly detection band via metric math:
  ```bash
  aws cloudwatch get-metric-data --metric-data-queries '[...]'
  ```

### 📸 Screenshots:
- `cli-describe-detector.png`, `cli-describe-alarm.png`, `cli-metric-band-output.png`

---

## Task 3: Post Custom Metrics with Python Script

- Used `custom-memory-metrics.py` script
- Monitored memory usage of `nginx` and `amazon-ssm-agent`
- Script posts metrics every 60 seconds to namespace `HostResources`
- Observed data under dimensions `Hostname, ProcessName`

### 📸 Screenshots:
- `custom-metric-graph.png`, `script-terminal-output.png`

---

## Task 4: Observe Alarm State

- Revisited `logins-alarm` in CloudWatch > Alarms
- Alarm state: `In Alarm`
- Graph showed spike in `UserLogins` outside anomaly band

### 📸 Screenshots:
- `cloudwatch-in-alarm.png`, `cloudwatch-alarm-history.png`
