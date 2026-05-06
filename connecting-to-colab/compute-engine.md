---
description: NVIDIA Tesla L4 Instance 32 vCPU
---

# Compute Engine

The NVIDIA L4 Tensor Core GPU is a compact, energy-efficient data center accelerator based on the Ada Lovelace architecture. Launched in 2023 as the successor to the popular Tesla T4, it is designed for universal workloads including AI inference, video processing, and virtual workstations. \[1, 2, 3, 4]

### Key Specifications

* Architecture: NVIDIA Ada Lovelace (5nm process).
* Memory: 24 GB GDDR6 with ECC.
* Power Consumption: Very low 72W TDP (slot-powered, no extra connectors needed).
* Form Factor: Low-profile, single-slot PCIe Gen4 x16.
* Cooling: Passive (requires server chassis airflow).
* Performance:
  * FP32: 30.3 TFLOPS.
  * FP8 Tensor Core: 485 TFLOPS (with sparsity).
  * INT8 Tensor Core: 485 TOPS (with sparsity). \[1, 2, 3, 5, 6, 7, 8]

***

### Core Capabilities

* AI Inference: Optimized for Large Language Models (LLMs) like [Gemma](https://www.reddit.com/r/homelab/comments/1l8v7nt/nvidia_l4/) and Llama, offering up to 2.5x higher generative AI performance than the T4.
* Video Processing: Includes AV1 hardware encoding/decoding support; can host over 1,000 concurrent AV1 video streams at 720p30.
* Graphics & Virtualization: Features third-generation RT Cores and DLSS 3 support, delivering over 4x higher graphics performance for virtual workstations (vWS) and cloud gaming compared to the previous generation. \[1, 2, 3, 4, 9, 10]

***

### Comparison: L4 vs. T4 vs. A100

NVIDIA L4NVIDIA T4 (Previous)NVIDIA A100 (High-End)Ada LovelaceTuringAmpere \[11] 24 GB GDDR6 \[12, 13] 16 GB GDDR6 \[4, 14, 15] 40/80 GB HBM2e \[4, 16, 17, 18] 72W70W \[4, 18, 19] 250-400W \[18, 20, 21] Yes \[22] NoNoYesNoNoEfficient Inference \[23] Basic InferenceTraining / Massive Scale

_Source: Comparisons from_ [_Jarvislabs_](https://jarvislabs.ai/blog/l4-vs-a100) _and_ [_Clarifai_](https://www.clarifai.com/blog/t4-vs-l4)_._ \[24, 25]



💡 Key Takeaway: The L4 is a "production sweet spot" for serving models under 24GB, providing 3-5x better cost-efficiency for inference than the A100 while consuming significantly less power. \[24, 25]Would you like to know about cloud providers that offer L4 instances, or are you looking for specific benchmarks for a particular AI model?

\
\[1] [https://www.nvidia.com](https://www.nvidia.com/en-us/data-center/l4/)\[2] [https://lenovopress.lenovo.com](https://lenovopress.lenovo.com/lp1717-thinksystem-nvidia-l4-24gb-pcie-gen4-passive-gpu)\[3] [https://www.pny.com](https://www.pny.com/File%20Library/Company/Support/Product%20Brochures/NVIDIA%20Data%20Center%20GPUs/pny-nvidia-l4-datasheet.pdf)\[4] [https://developer.nvidia.com](https://developer.nvidia.com/blog/supercharging-ai-video-and-ai-inference-performance-with-nvidia-l4-gpus/)\[5] [https://www.techpowerup.com](https://www.techpowerup.com/gpu-specs/l4.c4091)\[6] [https://www.servethehome.com](https://www.servethehome.com/nvidia-l4-review-the-versatile-ai-inference-card-pny/)\[7] [https://www.pny.com](https://www.pny.com/nvidia-l4)\[8] [https://www.cisco.com](https://www.cisco.com/c/dam/en/us/products/collateral/servers-unified-computing/ucs-c-series-rack-servers/nvidia-l4-gpu.pdf)\[9] [https://www.reddit.com](https://www.reddit.com/r/homelab/comments/1l8v7nt/nvidia_l4/)\[10] [https://www.pny.com](https://www.pny.com/en-eu/nvidia-l4)\[11] [https://www.aime.info](https://www.aime.info/blog/en/deep-learning-gpu-benchmarks-2020/)\[12] [https://www.youtube.com](https://www.youtube.com/watch?v=kBoxEjM19J8\&t=2)\[13] [https://www.baseten.co](https://www.baseten.co/blog/understanding-nvidias-datacenter-gpu-line/)\[14] [https://yandex.cloud](https://yandex.cloud/en/docs/compute/concepts/gpus)\[15] [https://www.bestgpusforai.com](https://www.bestgpusforai.com/gpu-comparison/l4-vs-a100)\[16] [https://ai.plainenglish.io](https://ai.plainenglish.io/the-10-best-gpus-for-llm-and-ai-development-in-2025-from-builders-to-breakthroughs-805c62c3baf7)\[17] [https://acecloud.ai](https://acecloud.ai/blog/nvidia-a100-vs-l4-gpu/)\[18] [https://www.dell.com](https://www.dell.com/en-hk/shop/nvidia-l4-pcie-72-watt-24gb-passive-single-wide-low-profile-gpu-customer-install/apd/490-bjrr/graphic-video-cards)\[19] [https://lenovopress.lenovo.com](https://lenovopress.lenovo.com/lp1926-thinksystem-nvidia-t4-16gb-pcie-passive-gpu)\[20] [https://acecloud.ai](https://acecloud.ai/blog/nvidia-a100-vs-l4-gpu/)\[21] [https://www.databasemart.com](https://www.databasemart.com/blog/best-nvidia-gpus-for-llm-inference-2025)\[22] [https://www.boston-it.com](https://www.boston-it.com/wp-content/uploads/l4-datasheet-2595652.pdf)\[23] [https://acecloud.ai](https://acecloud.ai/blog/nvidia-a100-vs-l4-gpu/)\[24] [https://jarvislabs.ai](https://jarvislabs.ai/blog/l4-vs-a100)\[25] [https://www.clarifai.com](https://www.clarifai.com/blog/t4-vs-l4)

Use Gemini to determine the efficiency of the below maching type instance.

{% code overflow="wrap" %}
```bash
gcloud compute instances create instance-20260502-160249 --project=superpositional --zone=northamerica-northeast1-c --machine-type=g2-custom-32-122880 --network-interface=network-tier=PREMIUM,stack-type=IPV4_ONLY,subnet=default --metadata=enable-osconfig=TRUE --maintenance-policy=TERMINATE --provisioning-model=STANDARD --service-account=39929026647-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/trace.append --accelerator=count=1,type=nvidia-l4 --create-disk=auto-delete=yes,boot=yes,device-name=instance-20260502-160249,image=projects/debian-cloud/global/images/debian-12-bookworm-v20260428,mode=rw,size=10,type=pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=goog-ops-agent-policy=v2-template-1-7-0,goog-ec-src=vm_add-gcloud --reservation-affinity=any && printf 'agentsRule:\n  packageState: installed\n  version: latest\ninstanceFilter:\n  inclusionLabels:\n  - labels:\n      goog-ops-agent-policy: v2-template-1-7-0\n' > config.yaml && gcloud compute instances ops-agents policies create goog-ops-agent-v2-template-1-7-0-northamerica-northeast1-c --project=superpositional --zone=northamerica-northeast1-c --file=config.yaml && gcloud compute resource-policies create snapshot-schedule default-schedule-1 --project=superpositional --region=northamerica-northeast1 --max-retention-days=14 --on-source-disk-delete=keep-auto-snapshots --daily-schedule --start-time=20:00 && gcloud compute disks add-resource-policies instance-20260502-160249 --project=superpositional --zone=northamerica-northeast1-c --resource-policies=projects/superpositional/regions/northamerica-northeast1/resourcePolicies/default-schedule-1
```
{% endcode %}

