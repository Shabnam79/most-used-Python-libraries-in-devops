# DevOps-Centric Python Libraries Documentation

This documentation outlines best practices and usage examples for the most widely adopted Python libraries in the DevOps domain.

---

## 1. **Ansible (Python-based IaC)**

**Use Case:** Automate configuration management and software provisioning across servers.

```bash
# Install Ansible
pip install ansible
```

**Why it's used:** Enables agentless orchestration using YAML-based playbooks for scalable infrastructure automation.

**Example:**
```yaml
- name: Install NGINX on Ubuntu
  hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

```bash
ansible-playbook nginx.yml
```

---

## 2. **Boto3 (AWS SDK for Python)**

**Use Case:** Programmatically manage AWS resources.

```bash
pip install boto3
```

**Why it's used:** Provides Pythonic access to AWS APIs for infrastructure automation in CI/CD pipelines.

**Example:**
```python
import boto3

ec2 = boto3.resource('ec2')
instance = ec2.create_instances(
    ImageId='ami-0abcdef1234567890',
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro',
    KeyName='your-key-pair-name'
)
print("Launched instance ID:", instance[0].id)
```

---

## 3. **Docker SDK for Python (`docker-py`)**

**Use Case:** Manage Docker containers using Python scripts.

```bash
pip install docker
```

**Why it's used:** Automates container lifecycle operations directly through code, ideal for CI jobs and container orchestration.

**Example:**
```python
import docker
client = docker.from_env()

container = client.containers.run("nginx", detach=True)
print("Container ID:", container.id)
```

---

## 4. **Fabric**

**Use Case:** Automate remote server administration using SSH.

```bash
pip install fabric
```

**Why it's used:** Simplifies execution of remote commands and deployment scripts using Python over SSH.

**Example:**
```python
from fabric import Connection

c = Connection(host="192.168.0.1", user="ubuntu", connect_kwargs={"key_filename": "~/.ssh/id_rsa"})
c.run("uname -a")
```

---

## 5. **Requests**

**Use Case:** Interact with HTTP APIs to perform health checks or consume services.

```bash
pip install requests
```

**Why it's used:** Simplifies REST API integration and service monitoring scripts.

**Example:**
```python
import requests

response = requests.get("http://example.com/health")
if response.status_code == 200:
    print("Service is healthy")
else:
    print("Service health check failed")
```

---

## 6. **Pytest**

**Use Case:** Unit testing and automation testing in CI/CD workflows.

```bash
pip install pytest
```

**Why it's used:** Offers robust, readable syntax for scalable automated testing.

**Example:**
```python
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
```

```bash
pytest test_file.py
```

---

## 7. **Scapy**

**Use Case:** Craft network packets for testing and security validation.

```bash
pip install scapy
```

**Why it's used:** Enables packet manipulation and network inspection for DevSecOps scenarios.

**Example:**
```python
from scapy.all import sr1, IP, ICMP

packet = IP(dst="8.8.8.8")/ICMP()
response = sr1(packet, timeout=2)
if response:
    print("Ping successful")
else:
    print("Ping failed")
```

---

## 8. **Airflow**

**Use Case:** Schedule and orchestrate complex workflows.

```bash
pip install apache-airflow
```

**Why it's used:** DAG-based orchestration for ETL, automation tasks, and cross-platform data workflows.

**Example:**
```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime

with DAG(dag_id="hello_world",
         schedule_interval="*/5 * * * *",
         start_date=datetime(2023, 1, 1),
         catchup=False) as dag:

    task = BashOperator(
        task_id="say_hello",
        bash_command="echo 'Hello from Airflow!'"
    )
```

---

## 🔒 Security Best Practices
- Always sanitize input for `Requests`, `Fabric`, and `Docker` usage.
- Store AWS credentials securely using `~/.aws/credentials` or AWS Secrets Manager.
- Leverage Airflow’s secrets backend for managing sensitive configurations.

---

