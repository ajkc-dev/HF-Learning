---
description: >-
  Since Colab is a free service it's best to run your notebook from a local
  machine with better GPU.
---

# Connecting to Colab

### Phase 1: Prepare the GCP VM

Assuming you have a fresh VM (e.g., Debian or Ubuntu), run these commands in your VM terminal.

#### 1. Update System & Install Python/Pip

First, ensure your package lists are fresh and you have the necessary build tools.

{% code overflow="wrap" %}
```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
```
{% endcode %}

#### 2. Create a Virtual Environment

Since modern Linux prevents system-wide pip installs, we create an isolated environment to house the Colab bridge.

{% code overflow="wrap" %}
```bash
# Create the environment folder
python3 -m venv colab-env
```
{% endcode %}

\# Activate it

{% code overflow="wrap" %}
```bash
source colab-env/bin/activate
```
{% endcode %}

Tip: You will know it's working when you see (colab-env) appear before your command prompt.

#### 3. Install the Colab Connectivity Tools

Inside your activated environment, install Jupyter and the specific extension Colab needs to communicate.

{% code overflow="wrap" %}
```bash
pip install jupyter jupyter_http_over_ws \
jupyter serverextension enable --py jupyter_http_over_ws
```
{% endcode %}

***

### Phase 2: Launch and Tunnel

#### 1. Start the Jupyter Server

Run this command on the VM. It tells the server to trust requests coming from the Google Colab domain.

{% code overflow="wrap" %}
```bash
jupyter notebook \
  --NotebookApp.allow_origin='https://colab.research.google.com' \
  --port=8888 \
  --NotebookApp.port_retries=0 \
  --NotebookApp.allow_credentials=True \
  --no-browser
```
{% endcode %}

Important: Look for a line in the output that says:

{% code overflow="wrap" %}
```bash
http://localhost:8888/?token=YOUR_UNIQUE_TOKEN_HERE
```
{% endcode %}

Copy this entire URL.

#### 2. Open the SSH Tunnel (On Your Local Computer)

Open a terminal on your actual laptop/desktop (not the VM) and run:

{% code overflow="wrap" %}
```bash
gcloud compute ssh YOUR_VM_NAME \
    --zone YOUR_ZONE \
    -- -L 8888:localhost:8888
```
{% endcode %}

This acts like a "pipe," taking everything happening on your VM's port 8888 and making it appear on your local computer's port 8888.

***

### Phase 3: Connect Google Colab

1. Go to[ colab.research.google.com](https://colab.research.google.com/).
2. Click the down arrow next to the Connect button (top right).
3. Select Connect to local runtime.
4. Paste the URL you copied earlier (the one with the token).
5. Click Connect.

***

#### Summary Checklist

* System Python: Untouched (stays safe).
* Virtual Env: Activated and containing jupyter\_http\_over\_ws.
* Firewall: No GCP firewall rules needed because we are using an SSH Tunnel (port 22).
* Storage: Any files you save in Colab will now appear on your GCP VM disk.

Does the connection show as "Connected (Local)" in the top right of your Colab screen now?

<br>
