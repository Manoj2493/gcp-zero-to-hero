# Day-02: GCP Project Setup and Billing

---

## What You Will Learn Today

- GCP Hierarchy
- What is a GCP project and why it's needed
- How billing accounts work in GCP
- Setting budget alerts to avoid unexpected charges
- Enabling APIs required for your workloads

---

## GCP Hierarchy

<img width="1024" height="1024" alt="GCP Resource Hierarchy Flowchart" src="https://github.com/user-attachments/assets/c1d9b947-bf12-4b30-9df6-df3491dc01a8" />

## Understanding GCP Projects

In GCP, everything you create (VMs, buckets, databases, etc.) lives inside a **project**.

- Think of a **project** as a folder where all your cloud resources are grouped.
- Every project has its own billing, IAM roles, and API settings.
- You can have multiple projects under the same billing account.

Use-case:
- One project for payments team.
- Another for shipment team.

---

## Billing Accounts in GCP

When you signed up for the free tier, a billing account was automatically created and linked to your default project.

Important points:
- A single billing account can be linked to multiple projects.
- If your free credits expire, charges will start applying only if you manually upgrade.

---

## Task 1: Create a New Project

1. Go to the GCP Console: https://console.cloud.google.com
2. From the top bar, click on the project dropdown
3. Click **New Project**
4. Give it a name like `gcp-zero-to-hero`
5. Select your billing account and create

This is the project we will use for all future labs.

---

## Task 2: Set Budget Alerts

Budget alerts help you track usage and avoid surprises.

Steps:

1. Go to Billing → Budgets & alerts
2. Click **Create Budget**
3. Set a budget limit (example: ₹1000)
4. Configure email alerts at 50%, 90%, and 100%

Note: These are just alerts. GCP won't stop services automatically.

---

## Task 3: Enable APIs for Core Services

APIs must be enabled before you can use many GCP services.

Recommended APIs to enable now:

- Compute Engine API
- Cloud Storage API
- Cloud Logging API
- Cloud Monitoring API
- Cloud Resource Manager API
- IAM Service Account Credentials API

Steps:

1. Go to **APIs & Services → Library**
2. Search each API by name and click **Enable**

Alternatively, use Cloud Shell:

```bash
gcloud services enable compute.googleapis.com \
    storage.googleapis.com \
    monitoring.googleapis.com \
    logging.googleapis.com \
    cloudresourcemanager.googleapis.com \
    iamcredentials.googleapis.com
```
