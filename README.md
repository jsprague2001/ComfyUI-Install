# Install uv and ComfyUI

```
135  sudo apt update && sudo apt upgrade -y
  136  sudo apt install -y git build-essential
  137  curl -LsSf https://astral.sh/uv/install.sh | sh
  138  source $HOME/.local/bin/env
  139  curl -LsSf https://astral.sh/uv/install.sh | sh
  140  sudo apt install curl
  141  curl -LsSf https://astral.sh/uv/install.sh | sh
  142  source $HOME/.local/bin/env
  143  uv --version
  144  ls
  145  mkdir diffusion
  146  cd diffusion/
  147  ls
  148  cd ~
  149  ls
  150  cd diffusion/
  151  ls
  152  git clone https://github.com/comfyanonymous/ComfyUI.git
  153  cd ComfyUI
  154  ls
  155  uv venv --python 3.12
  156  source .venv/bin/activate
  157  uv pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
  158  uv pip install -r requirements.txt
  159  python3 -c "import torch; print(torch.cuda.is_available(), torch.cuda.get_device_name(0))"
  160  python3 main.py --listen 0.0.0.0 --port 8188
  161  sudo tee /etc/systemd/system/comfyui.service > /dev/null <<'EOF'
  162  [Unit]
  163  Description=ComfyUI
  164  After=network.target
  165  [Service]
  166  Type=simple
  167  User=jsprague
  168  WorkingDirectory=/home/jsprague/diffusion/ComfyUI
  169  ExecStart=/home/jsprague/diffusion/ComfyUI/.venv/bin/python3 main.py --listen 0.0.0.0 --port 8188
  170  Restart=on-failure
  171  [Install]
  172  WantedBy=multi-user.target
  173  EOF
  174  sudo systemctl daemon-reload
  175  sudo systemctl enable --now comfyui
  176  sudo systemctl status comfyui
  177  journalctl -u comfyui -f
  178  cat /etc/avahi/avahi-daemon.conf
```



