
## 🛒 K8-RoboShop: Deploying a Microservices E-commerce Website on Kubernetes with EKS

**Project Goal:**
To containerize and orchestrate a multi-component e-commerce application called **RoboShop** using **Kubernetes** on **AWS EKS (Elastic Kubernetes Service)**—leveraging cloud-native architecture, automation, and DevOps principles.

---

## 🚀 Why This Project Matters

In traditional setups, applications like RoboShop run on **virtual machines**, making them harder to scale, maintain, or upgrade. This project modernizes that process by:

* **Containerizing microservices** with Docker.
* **Orchestrating containers** using Kubernetes.
* **Automating infrastructure** with Terraform & eksctl.
* **Utilizing managed Kubernetes (EKS)** for reliability, scalability, and ease of use.

---

## 🔧 Tools & Technologies Used

| Tool           | Purpose                                      |
| -------------- | -------------------------------------------- |
| **VS Code**    | Writing and organizing manifest files        |
| **Git Bash**   | Version control & pushing code to GitHub     |
| **MobXterm**   | SSH/terminal access to EC2/Linux systems     |
| **Docker**     | Containerizing individual microservices      |
| **Kubernetes** | Running and managing containerized workloads |
| **Terraform**  | Provisioning infrastructure resources        |
| **EKS**        | Running Kubernetes clusters in AWS           |

---

## 📦 Services Deployed (Each with Its Own Manifest)

* MongoDB
* MySQL
* Redis
* RabbitMQ
* User Service
* Cart Service
* Catalog Service
* Shipping Service
* Payment Service
* Frontend

---

## 📁 Folder Structure & Execution

```bash
# Step 1: Create Namespace
kubectl apply -f 01-namespace.yaml

# Step 2: Apply All Microservices (excluding frontend)
for dir in */; do
  if [ "$dir" != "frontend/" ] && [ -f "${dir}manifest.yaml" ]; then
    kubectl apply -n roboshop -f "${dir}manifest.yaml"
  fi
done

# Step 3: Deploy Frontend
kubectl apply -n roboshop -f frontend/manifest.yaml

# Step 4: Get External Access URL
kubectl get svc -n roboshop
```

---

## 🛡️ IAM & EC2 Setup

* EC2 instance configured with **IAM Role** to allow `eksctl` and AWS CLI to create and manage EKS clusters.
* Script `docker.sh` is used to configure the instance with Docker and Kubernetes tools.

---

## 🧼 Cleanup Strategy to Save Cost

Once the cluster is no longer needed, destroy it to avoid unnecessary AWS charges:

```bash
cd docker/
eksctl delete cluster --config-file=eks.yaml
```

---

## 📚 Learning Outcomes

* ✅ Deploying microservices in Kubernetes using manifest files.
* ✅ Automating resource creation with `eksctl` and Terraform.
* ✅ Managing Kubernetes workloads using namespaces and labels.
* ✅ Gaining real-world exposure to AWS-managed Kubernetes via EKS.
* ✅ Optimizing cost by cleaning up unused cloud resources.
* ✅ Structuring multi-service projects for maintainability and scalability.

---

## 📸 References

Add visuals and screenshots for:

* Folder structure
* Frontend access URL
* Sample pod status (`kubectl get pods -n roboshop`)

> 📂 Place all reference images in the `images/` folder of your repo.

---

## ✅ Advantages of Using EKS for RoboShop

* **Managed Control Plane**: AWS handles scaling, patching, and availability of the Kubernetes control plane.
* **Integration with AWS Services**: IAM, ELB, CloudWatch, and EBS can be used seamlessly.
* **Scalability**: Easily scale nodes and workloads up/down.
* **Security**: Fine-grained access control using IAM & RBAC.
* **Cost Optimization**: Use spot instances or right-size your workloads.
* **High Availability**: Automatically runs workloads across multiple AZs.

