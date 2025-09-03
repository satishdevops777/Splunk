# Splunk
- Splunk is a data analytics and monitoring platform mainly used for machine data (logs, metrics, events).
- Splunk collects logs & metrics from servers, apps, networks, cloud, and security devices → stores them → makes them searchable → and lets you build dashboards, alerts, and reports.

🔑 Key Capabilities of Splunk

1. Data Ingestion
- Collects logs from servers, apps, containers, firewalls, cloud services, etc.
- Supports many sources (Syslog, HTTP, APIs, forwarders).

2. Indexing & Storage
- Stores data in indexed format for fast search.
- You can define data retention (hot, warm, cold, frozen).

3. Search & Query (SPL)
- Uses SPL (Search Processing Language) to query data.
- Example:
```spl
index=security sourcetype=firewall action=blocked | stats count by src_ip
```

4. Visualization & Dashboards
- Create real-time dashboards, charts, reports for monitoring & business insights.

5. Alerts & Automation
- Trigger alerts (email, webhook, Slack, PagerDuty) when thresholds are met.
- Example: Alert when login failures > 100 in 5 mins.

6. Apps & Integrations
- Splunkbase has 1000+ apps (AWS, GCP, Azure, Kubernetes, Docker, Palo Alto, etc.).

🔒 Splunk in Security (SIEM Use Case)
- Splunk Enterprise Security (Splunk ES) = SIEM solution.
- Detects threats, anomalies, intrusions using logs from IDS/IPS, firewalls, cloud.
- Supports SOAR (Splunk Phantom) → automates response (block IP, disable user).

⚙️ Splunk Components
- Forwarders → Collect logs & send to Splunk indexer.
  - Universal Forwarder (UF): Lightweight agent.
  - Heavy Forwarder: Parses data before sending.
- Indexer → Stores & indexes incoming data.
- Search Head → Provides web UI, dashboards, runs SPL queries.
- Deployment Server / Cluster Master → For managing multiple Splunk instances.

🔹 1. Splunk On-Premise Installation (Servers / VMs)
 - Steps to Install
    1. Download Splunk Enterprise 
    - From Splunk Downloads.
    - Example (RHEL/CentOS):
    ```bash
    wget -O splunk.rpm 'https://download.splunk.com/products/splunk/releases/9.2.0/linux/splunk-9.2.0.rpm'
    sudo rpm -ivh splunk.rpm
    ```
    2. Start Splunk
    ```bash
    sudo /opt/splunk/bin/splunk start --accept-license
    ```
    - Set up admin user.
    - Access Web UI → http://<server-ip>:8000.
    3. Enable Auto-Start
    ```bash
    sudo /opt/splunk/bin/splunk enable boot-start
    ```
    4. Install Splunk Universal Forwarder (on each server to collect logs/metrics):
    ```bash
    wget -O splunkforwarder.rpm 'https://download.splunk.com/products/universalforwarder/releases/9.2.0/linux/splunkforwarder-9.2.0.rpm'
    sudo rpm -ivh splunkforwarder.rpm
    ```
    - Configure forwarder to send logs to Splunk Indexer:
    ```bash
    /opt/splunkforwarder/bin/splunk add forward-server <splunk-indexer-ip>:9997 -auth admin:changeme
    /opt/splunkforwarder/bin/splunk add monitor /var/log
    ```

🔹 2. Splunk Cloud (Managed SaaS)
