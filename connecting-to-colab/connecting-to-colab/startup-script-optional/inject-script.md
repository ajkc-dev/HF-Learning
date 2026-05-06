# Inject Script

You inject this setup directly into your `gcloud compute instances create` command using the `--metadata startup-script` flag. This ensures the VM is "Colab-ready" the moment it finishes booting.

#### The Unified `gcloud` Command

This command combines your optimized hardware specs (L4 GPU, 100GB disk) with the automation script derived from your documentation.

```bash
gcloud compute instances create hf-learning-vm \
    --project=superpositional \
    --zone=northamerica-northeast1-c \
    --machine-type=g2-standard-4 \
    --accelerator=count=1,type=nvidia-l4 \
    --image-family=common-cu121-debian-11-py310 \
    --image-project=deeplearning-platform-release \
    --boot-disk-size=100 \
    --boot-disk-type=pd-balanced \
    --maintenance-policy=TERMINATE \
    --metadata=startup-script='#!/bin/bash
    # 1. Install dependencies [cite: 5, 9]
    apt update && apt install -y python3-venv

    # 2. Setup Virtual Env [cite: 10, 14]
    python3 -m venv /opt/colab-env
    source /opt/colab-env/bin/activate

    # 3. Install Colab tools [cite: 18, 21, 22]
    pip install jupyter jupyter_http_over_ws
    jupyter serverextension enable --py jupyter_http_over_ws

    # 4. Launch Jupyter [cite: 24, 27-32]
    jupyter notebook \
      --NotebookApp.allow_origin="https://colab.research.google.com" \
      --port=8888 \
      --NotebookApp.port_retries=0 \
      --NotebookApp.allow_credentials=True \
      --no-browser \
      --allow-root &'
```

***

#### How to Retrieve the Token

Because the script runs automatically in the background at boot, you won't see the token on your screen. To find it so you can connect:

1.  SSH into your VM once it is running.

    <a class="button secondary"></a>
2.  Run this command to view the startup logs:

    Bash

    ```
    sudo journalctl -u google-startup-scripts.service
    ```
3.  Look for the URL that starts with `http://localhost:8888/?token=...`.

    <a class="button secondary"></a>

#### Why this is more efficient:

*   Automation: You don't have to manually run Phase 1 every time you create a new VM.

    <a class="button secondary"></a>
*   Clean Environment: By using `/opt/colab-env`, your project stays organized and avoids "Externally Managed Environment" errors.

    <a class="button secondary"></a>
* No Port Conflicts: It explicitly binds to port 8888, which matches your recommended SSH tunnel command.

Once you have that token from the logs, you can proceed directly to Phase 2 (Tunneling) and Phase 3 (Connecting) in your guide.
