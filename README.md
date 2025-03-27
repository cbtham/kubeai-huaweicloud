# KubeAI: AI Inferencing Operator on Huawei Cloud Managed Kubernetes Service (CCE)
Deploy and scale machine learning models on Kubernetes. Built for LLMs, embeddings, and speech-to-text.
For more information about the open-source project, refer https://github.com/substratusai/kubeai

![KubeAI Architecuture](./architecture/arch.excalidraw.png)

![KubeAI on CCE Architecuture](./architecture/kubeai-cce.png)

## Overview
KubeAI inferece operator allows you to run, manage and host LLMs easily on Kubernetes clusters on CPU or GPU(Nvidia, AMD) and even NPU and TPUs.
In this example, we will use KubeAI powered by Huawei Cloud CCE with a GPU node.

This is good for: 
🚀 LLM Inferencing - Operate vLLM and Ollama servers__
🎙️ Speech Processing - Transcribe audio with FasterWhisper__
🔢 Vector Embeddings - Generate embeddings with Infinity__
⚡️ Intelligent Scaling - Scale from zero to meet demand
📊 Optimized Routing - Dramatically improves performance at scale (see paper)
💾 Model Caching - Automates downloading & mounting (EFS, etc.)
🧩 Dynamic Adapters - Orchestrates LoRA adapters across replicas
📨 Event Streaming - Integrates with Kafka, PubSub, and more

🔗 OpenAI Compatible - Works with OpenAI client libraries
🛠️ Zero Dependencies - Does not require Istio, Knative, etc.
🖥 Hardware Flexible - Runs on CPU, GPU, or TPU

## Pre-requisite
Before running this, ensure you have the following,
1. Huawei Cloud account
2. Kubectl configured
3. Helm installed

### To deploy

1. Create a namespace, in this example "kubeai"
   ```kubectl create namepace -n kubeai```
2. Create pv and pvc for open-webui
   ```kubectl create -f pv-pvc.yaml -n kubeai```
3. Deploy kubeai with custom-values.yaml
   ```helm upgrade --install kubeai kubeai/kubeai -f custom-values.yaml  -n kubeai --wait --timeout 15m```
4. Deploy models with kubeai-models.yaml
   ```helm upgrade kubeai-models kubeai/models -f ./kubeai-models.yaml -n kubeai --wait --timeout 15m```
5. Create a Load Balancer service to access open-webui
   ```kubectl create -f elb-svc.yaml -n kubeai```
6. Visit the public ip shown at elb-svc-openwebui at CCE > Services & ingress.
