# Google Cloud Storage (GCS)

Google Cloud Storage (GCS) is Google’s **object storage service**, designed to store files of any size (from a few KB to petabytes) in a secure, durable, and highly available way.  
It’s the **GCP equivalent of AWS S3 or Azure Blob Storage** and is widely used in DevOps for storing artifacts, logs, backups, and static assets.

---

## 🔹 Key Features of GCS

### 1. **Object Storage**
- Stores data as **objects** (file + metadata) inside **buckets**.  
- Ideal for unstructured data like logs, media, backups, and CI/CD artifacts.  

---

### 2. **Durability**
- GCS provides **11 nines (99.999999999%) durability**.  
- Data is automatically replicated across multiple physical devices.  
- This means your data is extremely safe from hardware failures.  

---

### 3. **Availability & Storage Classes**
- GCS offers different storage classes depending on how often you access data:  
  - **Standard** → For frequently accessed data.  
  - **Nearline** → For data accessed once a month.  
  - **Coldline** → For data accessed once a quarter.  
  - **Archive** → For rarely accessed, long-term storage.  
- Classes differ in **cost per GB** and **retrieval charges**.  

---

### 4. **Regions and Multi-Regions**
- You choose where your data is stored:  
  - **Region** → Data stays in one location (e.g., `asia-south1`).  
  - **Dual-Region** → Data is stored in two regions automatically.  
  - **Multi-Region** → Data is spread across a continent (e.g., US, Europe, Asia).  
- **Multi-region storage** improves availability and global access speeds.  

---

### 5. **Security**
- All data is **encrypted at rest and in transit** by default.  
- Fine-grained **IAM roles** (e.g., Storage Object Viewer, Storage Object Admin).  
- Supports **service accounts** for keyless authentication from apps/VMs.  

---

### 6. **Cost Highlights**
- **Pay only for what you use** (no upfront capacity planning).  
- Costs include:  
  - Storage per GB/month (cheaper for Coldline/Archive).  
  - Network egress (downloading data out of GCP).  
  - API requests (PUT/GET/LIST).  
- ✅ Tip: Use **lifecycle policies** to automatically move older data to cheaper classes.  

---

### 7. **Performance**
- High throughput, low latency access to objects.  
- Strong **read-after-write consistency** globally (you always get the latest object after upload).  

---

### 8. **Integration with DevOps Tools**
- **CI/CD** → Store build artifacts, Helm charts, Terraform state files.  
- **Observability** → Centralized log storage.  
- **Static hosting** → Host websites or documentation directly from GCS.  
- **Analytics** → Integrates with BigQuery, Dataflow, and AI/ML pipelines.  

---

## ✅ Quick Recap
- **Buckets** are the main container in GCS.  
- Data is **durable, secure, and highly available**.  
- Multiple **storage classes** help balance cost and performance.  
- **Multi-region support** makes global apps faster.  
- Perfect for **DevOps workflows** like CI/CD artifacts, backups, and log storage.  

