# 🧠 Neural Nexus – Transformer-Based End-to-End Web Application Firewall (WAF) Pipeline  
**Smart India Hackathon 2025 | Problem Statement ID: SIH25172 | Theme: Blockchain & Cybersecurity**  

---

## 🚀 Overview  

**Neural Nexus** introduces **NeuralGuard**, a **Transformer-based Web Application Firewall (WAF)** built to deliver **real-time, adaptive, and zero-day threat protection** for modern web infrastructures.  

Unlike traditional signature-based WAFs that rely on static rules, NeuralGuard leverages **deep contextual learning** through **Transformer Autoencoders** trained exclusively on benign traffic patterns. This enables **context-aware anomaly detection**, identifying and blocking novel or obfuscated attacks before they reach the application layer.

---

## 🧩 Problem Statement  

Traditional WAFs struggle to detect **zero-day exploits**, **evasive attacks**, and **contextual anomalies** in HTTP traffic.  
The challenge is to design an **end-to-end intelligent WAF pipeline** that:  
- Operates **in real-time** without adding significant latency.  
- **Learns autonomously** from benign traffic.  
- **Scales dynamically** to handle production-grade workloads.  
- Seamlessly integrates with existing web infrastructure.  

---

## 💡 Proposed Solution – NeuralGuard Architecture  

NeuralGuard employs a **sidecar architecture** integrated with **Nginx** for non-blocking traffic inspection and decision-making:  

1. **Entry Gateway (Nginx):**  
   - Pauses each request and forwards metadata via an `intercept_request` to the WAF sidecar.  

2. **WAF Sidecar (FastAPI + Transformer Engine):**  
   - Performs **deep anomaly detection** using a quantized Transformer model.  
   - Returns verdicts:  
     - `200 OK` → Safe traffic  
     - `403 Forbidden` → Malicious traffic (blocked instantly)  

3. **Control Plane (Continuous Learning):**  
   - Message Queue → Data Lake → Training Pipeline → Model Registry → CI/CD.  
   - Enables **autonomous model retraining**, versioning, and zero-downtime redeployment.  

4. **Logging & Monitoring:**  
   - Asynchronous logging ensures every verdict is captured without affecting throughput.  
   - Integrated monitoring and dashboards for auditability and compliance.

---

## 🧭 Design Approach & Tooling Rationale  

The **NeuralGuard** project was built with a clear goal — to achieve **real-time, self-learning web application security** without the trade-offs of traditional WAF systems.  
Every technology and architectural decision was made with **performance, scalability, and autonomy** in mind.  

### 🔧 Why These Tools?

| Component | Technology | Reason for Selection |
|------------|-------------|----------------------|
| **Reverse Proxy & Gateway** | **Nginx** | Industry-standard, lightweight, and high-performance web proxy capable of handling massive concurrent traffic. It enables request interception through the `auth_request` module, crucial for WAF integration. |
| **WAF Engine (Inference API)** | **FastAPI + Uvicorn** | FastAPI offers asynchronous I/O and native ASGI support, which ensures ultra-low latency for model inference. Uvicorn’s event loop design is perfect for serving ML-based verdicts in real-time. |
| **Deep Learning Framework** | **PyTorch + Hugging Face Transformers** | Provides flexible and production-grade Transformer architectures for sequence modeling. Hugging Face simplifies model experimentation and fine-tuning with pre-trained language models. |
| **Model Optimization** | **ONNX + INT8 Quantization** | Converts and compresses large Transformer models for faster inference without sacrificing accuracy — vital for production environments where every millisecond matters. |
| **Data Pipeline** | **Kafka / RabbitMQ + Logstash + Elasticsearch / S3** | Enables asynchronous log streaming, indexing, and long-term data retention. Kafka ensures reliable, fault-tolerant message delivery; Elasticsearch supports deep security analytics. |
| **Model Training & Versioning** | **PyTorch Lightning + MLflow / DVC** | MLflow and DVC provide experiment tracking, version control, and reproducibility — critical for continuous model improvement and rollback safety. |
| **Containerization & Scaling** | **Docker + Kubernetes** | Ensures isolated, portable environments. Kubernetes handles automatic scaling using HPA (Horizontal Pod Autoscaling) to maintain throughput under load. |
| **Monitoring & Observability** | **Prometheus + Grafana** | Provides real-time visibility into latency, CPU utilization, and inference accuracy metrics. Enables proactive issue detection and SLA assurance. |
| **Automation & Deployment** | **GitHub Actions / Jenkins CI/CD** | Fully automates training-to-deployment cycles, enabling “Security-as-Code” where every WAF update is versioned, reviewed, and deployed without downtime. |

---

### 🧠 Project Approach  

The approach to NeuralGuard is **pipeline-driven and incremental**, built around continuous feedback and adaptation rather than static rule enforcement.

1. **Data-Centric Learning**  
   - Train Transformer Autoencoders exclusively on **benign web traffic**, learning the natural syntax and structure of legitimate requests.  
   - Any deviation from this learned grammar is treated as a potential anomaly.  

2. **Sidecar Architecture for Non-Blocking Security**  
   - Instead of embedding the WAF directly into the application, a **sidecar container** handles inference.  
   - This keeps latency minimal and ensures the core application remains unaffected by the WAF’s computational load.  

3. **Continuous Model Improvement**  
   - The **Control Plane** (Message Queue → Data Lake → Training Pipeline → CI/CD) automatically retrains models on fresh data.  
   - Updated models are pushed to the **Model Registry** and redeployed seamlessly, ensuring continuous learning without downtime.  

4. **Explainability & Trust**  
   - Logging every inference decision (verdict + confidence score + request signature) allows explainable security decisions.  
   - Future modules (Explainable AI) will provide **transparent reasoning** behind block/allow verdicts for analysts.  

5. **Scalability and Reliability**  
   - By combining **microservices, Kubernetes scaling, and async event loops**, NeuralGuard achieves real-time protection at scale — even under unpredictable traffic spikes.  

---

In short, **NeuralGuard** combines **deep learning, modern DevOps, and scalable web infrastructure** into a single adaptive security pipeline — a next-gen WAF that **learns, adapts, and defends autonomously**.


---
## 🧠 Innovation Highlights  

| Feature | Description |
|----------|-------------|
| **Context-Aware Defense** | Understands the semantic “grammar” of normal web traffic for zero-day attack detection. |
| **Non-Blocking Architecture** | Sidecar-based processing keeps response latency minimal. |
| **Self-Learning WAF** | Continuously updates model parameters from benign data streams. |
| **Security-as-Code** | Integrated into CI/CD pipelines for version-controlled, automated WAF deployments. |

---

## ⚙️ Technical Approach  

### **Core Technologies**
- **Traffic Layer:** Nginx (reverse proxy, SSL/TLS termination, load balancing).  
- **Inference Engine:** FastAPI/Uvicorn serving Transformer models (PyTorch/TensorFlow) optimized via **ONNX & INT8 quantization**.  
- **Data Pipeline:** Kafka/RabbitMQ → Logstash → Elasticsearch/S3 for event storage and feature extraction.  
- **Model Training:** PyTorch Lightning + Hugging Face, with versioning via **MLflow/DVC**.  
- **Deployment & Scaling:** Docker + Kubernetes with **Horizontal Pod Autoscaling (HPA)**.  
- **Monitoring:** Prometheus + Grafana.  

### **Operational Flow**
1. Nginx forwards traffic to NeuralGuard sidecar.  
2. Transformer model performs real-time anomaly inference.  
3. Decisions are logged asynchronously.  
4. Feedback loop retrains models periodically through CI/CD automation.  

---

## 🧩 System Architecture  

![alt text](image.png)

---

## 📊 Feasibility & Viability  

- **Mature Stack:** Built on stable open-source technologies (Nginx, PyTorch, Kubernetes).  
- **Scalable Design:** Modular microservices enable independent scaling and upgrades.  
- **Value Proposition:** Targets WAF limitations—detecting zero-day threats without latency trade-offs.  
- **Continuous Improvement:** Feedback-driven model updates ensure evolving protection.  

---

## ⚠️ Challenges & Risk Mitigation  

| Challenge | Risk | Mitigation |
|------------|------|------------|
| **Model Latency & Load** | Increased response time under peak load | Request queuing with ASGI event loops + Kubernetes HPA |
| **False Positives/Negatives** | Operational disruptions | Human-in-the-loop validation + adaptive threshold tuning |
| **Data Quality & Model Drift** | Reduced accuracy over time | Incremental learning & versioned retraining via CI/CD |

---

## 💥 Impacts & Benefits  

### **Technological**
- Detects **zero-day and obfuscated threats** in real time.  
- Provides **quantifiable, data-driven security insights**.  
- Integrates smoothly with enterprise-grade infrastructures.  

### **Operational**
- Reduces manual rule updates through automation.  
- Enhances SOC team efficiency via detailed audit logs.  
- Scales seamlessly under dynamic traffic conditions.  

### **Economic**
- Cuts security operation costs with automation.  
- Prevents losses from data breaches and downtime.  
- Optimizes resource utilization, reducing cloud spend.  

### **Social & Ethical**
- Ensures data privacy and compliance (GDPR, ISO 27001).  
- Guarantees fair and uninterrupted access under attack.  

---

## 🔬 Research & References  

| Paper/Source | Key Focus |
|---------------|------------|
| [AI-Driven Transformer for Real-Time Anomaly Detection (Thesai.org)](https://thesai.org/Downloads/Volume16No2/Paper_111-AI_Driven_Transformer_Frameworks.pdf) | Transformer-based contextual detection |
| [WAF Based on Anomaly Detection using Deep Learning (DergiPark)](https://dergipark.org.tr/tr/download/article-file/2142038) | Deep learning models for WAFs |
| [Log Anomaly Detection using Transformer + TCN (ResearchGate)](https://www.researchgate.net/publication/390867799_Log_Anomaly_Detection_Method_Based_on_Transformer_and_Temporal_Convolutional_Networks) | Hybrid temporal analysis for anomaly detection |

### **Existing Systems for Comparison**
- [OWASP ModSecurity](https://github.com/owasp-modsecurity/ModSecurity/wiki)  
- [NAXSI (Nginx Anti-XSS & SQL Injection)](https://github.com/nbs-system/naxsi)  
- [Imperva WAF](https://www.imperva.com/products/web-application-firewall-waf/)  

### **Dataset**
A curated dataset of **1,133,280 normalized benign HTTP requests** from three distinct applications has been generated, validated, and is ready for model training.

---

## 🧰 Repository Structure  
```
NeuralGuard/
├── src/
│ ├── waf_sidecar/ # FastAPI app & Transformer inference
│ ├── nginx_config/ # Nginx reverse proxy & auth_request setup
│ ├── model_training/ # Data preprocessing & model training scripts
│ ├── ci_cd/ # Jenkins/GitHub Actions pipelines
│ └── utils/ # Logging, metrics, and monitoring helpers
├── datasets/
│ └── benign_corpus/ # Preprocessed benign request dataset
├── docs/
│ └── architecture_diagram.png
├── Dockerfile
├── kubernetes/
│ ├── deployment.yaml
│ ├── service.yaml
│ └── hpa.yaml
├── requirements.txt
└── README.md

```

---

## ⚡ Getting Started  

### **Prerequisites**
- Docker & Kubernetes cluster  
- Python 3.10+  
- Kafka, Elasticsearch stack  

### **Setup Instructions**
```bash
# Clone the repo
git clone https://github.com/adityashriwas/NeuralGuard.git
cd NeuralGuard

# Install dependencies
pip install -r requirements.txt

# Start WAF Sidecar locally
uvicorn src.waf_sidecar.main:app --host 0.0.0.0 --port 8080
```

## Deploy via Kubernetes

- kubectl apply -f kubernetes/deployment.yaml
- kubectl apply -f kubernetes/service.yaml
- kubectl apply -f kubernetes/hpa.yaml

---

## 🌍 Conclusion  

The **NeuralGuard** project represents a forward leap in the evolution of Web Application Firewalls — shifting from static, rule-based defense to **adaptive, learning-based security intelligence**.  
By merging the strengths of **Transformer architectures**, **sidecar-based design**, and **continuous learning pipelines**, Neural Nexus delivers a WAF solution that is:  

- **Context-aware:** Understands the semantics of real-world web traffic.  
- **Self-improving:** Learns continuously without human retraining.  
- **Scalable:** Operates under real-time constraints with high concurrency.  
- **Explainable:** Provides clear reasoning behind every security verdict.  

Our goal isn’t just to stop attacks — it’s to build **AI-driven security systems that evolve faster than threats themselves**.

---

## 🤝 Contribution  

We welcome contributions from developers, researchers, and cybersecurity experts who share our vision of intelligent web defense.  

You can contribute by:  
- Improving model performance or explainability.  
- Enhancing CI/CD or deployment automation.  
- Adding new datasets or data augmentation strategies.  
- Building visual dashboards or analytics extensions.  

To contribute:  
1. Fork the repository.  
2. Create a new branch: `git checkout -b feature-name`.  
3. Commit changes and open a Pull Request with a detailed description.  

---
