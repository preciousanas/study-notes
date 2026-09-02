---
name: "🔴 Module 5: AI Engineering & Productionization (Flagship)"
about: "Track containerization, high-throughput vLLM serving, Kubernetes clusters, and monitoring."
title: "Module 5: AI Engineering & Productionization"
labels: "🔴 Must-Have, Module-5"
---

## 📖 Learning Resources Tracking
- [ ] FastAPI Documentation
- [ ] Docker — Get Started Guide
- [ ] Kubernetes — Official "Learn Kubernetes Basics" Tutorials
- [ ] MLOps Zoomcamp (DataTalksClub)
- [ ] MLflow / Weights & Biases Documentation
- [ ] GitHub Actions Documentation
- [ ] PyTorch FSDP / Hugging Face Accelerate / DeepSpeed Tutorials
- [ ] vLLM Documentation
- [ ] Hugging Face Quantization Docs
- [ ] Evidently AI Documentation

## 🛠️ Project Tasks: "Serve, Scale, and Monitor an LLM"
- [ ] Containerize your Module 4 fine-tuned model and serve it via vLLM behind a FastAPI gateway
- [ ] Deploy container to a local Kubernetes cluster (kind/minikube) with health checks & HPA autoscaling
- [ ] Quantize the model (4-bit) and write a benchmark report (`benchmarks/latency_report.md`) on metrics before vs. after
- [ ] Track all system experiments and hyperparameters inside MLflow
- [ ] Build a GitHub Actions CI pipeline (`.github/workflows/ci.yml`) to lint code, run tests, and build/push images
- [ ] Integrate Evidently AI to log input distribution drift and alert on production quality degradation

## 🏁 Operational Checkpoint
- [ ] **Verification:** If p99 latency doubled overnight in production, what are the first three things you'd check, in order? (Document this reflection inside your `notes.md`).
