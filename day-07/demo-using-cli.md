# 🚀 Day-7: High Availability with MIGs and Load Balancing in GCP

## 🎯 Goal
Learn how to deploy a production-ready, highly available web application in GCP using **Managed Instance Groups (MIGs)**, **HTTP(S) Load Balancer**, and **health checks**, with observability through **Cloud Logging**.

---

## 📚 Key Concepts Covered

| Concept                        | Description |
|-------------------------------|-------------|
| **Managed Instance Group**     | A group of identical VMs managed automatically for autoscaling and self-healing |
| **Instance Template**          | Blueprint used to create VMs in the group |
| **HTTP(S) Load Balancer**      | Global, fully managed Layer 7 load balancer |
| **Health Check**               | Monitors the health of backends and removes unhealthy instances |
| **Multi-zone Deployment**      | Spreads instances across zones for HA |
| **Cloud Logging**              | Captures backend and load balancer logs for observability |

---

## 🧪 Hands-On Lab

### 🛠️ Step 1: Create a Startup Script for Web Server

    cat <<EOF > startup.sh
    #!/bin/bash
    apt update
    apt install -y nginx
    echo "Welcome to Day-7 MIG Demo - $(hostname)" > /var/www/html/index.html
    EOF

---

### 🛠️ Step 2: Create Instance Template

    gcloud compute instance-templates create web-template \
      --machine-type=e2-micro \
      --image-family=debian-11 \
      --image-project=debian-cloud \
      --metadata-from-file startup-script=startup.sh \
      --tags=http-server

---

### 🛠️ Step 3: Create Managed Instance Group Across 3 Zones

    gcloud compute instance-groups managed create web-mig \
      --base-instance-name=web \
      --size=3 \
      --template=web-template \
      --zones=us-central1-a,us-central1-b,us-central1-c

---

### 🛠️ Step 4: Expose Web Traffic via Firewall Rule

    gcloud compute firewall-rules create allow-http \
      --allow=tcp:80 \
      --target-tags=http-server \
      --description="Allow HTTP traffic to web servers"

---

### 🛠️ Step 5: Create Health Check

    gcloud compute health-checks create http web-health-check \
      --port=80

---

### 🛠️ Step 6: Create Backend Service and Add MIG

    gcloud compute backend-services create web-backend \
      --protocol=HTTP \
      --port-name=http \
      --health-checks=web-health-check \
      --global

    gcloud compute backend-services add-backend web-backend \
      --instance-group=web-mig \
      --instance-group-zone=us-central1-a \
      --global

---

### 🛠️ Step 7: Create URL Map and Target Proxy

    gcloud compute url-maps create web-map \
      --default-service=web-backend

    gcloud compute target-http-proxies create web-proxy \
      --url-map=web-map

---

### 🛠️ Step 8: Reserve Global IP and Create Forwarding Rule

    gcloud compute addresses create web-ip --global

    gcloud compute forwarding-rules create web-rule \
      --address=web-ip \
      --global \
      --target-http-proxy=web-proxy \
      --ports=80

---

### 🛠️ Step 9: Access the Load Balancer

    gcloud compute addresses describe web-ip --global

> Copy the IP and access it in the browser — it should hit one of your web servers!

---

## 📦 Real-World DevOps Use Case

> You're deploying a stateless web app that must remain highly available even if one zone goes down. You want:
> - **Autoscaling**
> - **Global load balancing**
> - **Health check-based instance removal**
> - **Monitoring of backend status via logs**

✅ MIG + Load Balancer + Multi-zone + Logging gives full production-grade setup.

---

## 📊 Enable Backend Logging

    gcloud compute backend-services update web-backend \
      --enable-logging \
      --logging-sample-rate=1.0 \
      --global

---

## ✅ Key Takeaways

- **MIGs** automate scaling, healing, and zone distribution.
- **HTTP(S) Load Balancer** routes traffic based on health and proximity.
- Health checks ensure only healthy instances serve traffic.
- Logs provide visibility into traffic patterns and backend health.
- This is the **foundation of production-grade, HA GCP deployments** for DevOps teams.

---
