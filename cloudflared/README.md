# Add repository
```echo 'deb http://pkg.cloudflare.com/ <RELEASE> main' | sudo tee /etc/apt/sources.list.d/cloudflare-main.list```
- exsample  
```echo 'deb http://pkg.cloudflare.com/ focal main' | sudo tee /etc/apt/sources.list.d/cloudflare-main.list```

- import GPG key  
```curl -C - https://pkg.cloudflare.com/pubkey.gpg | sudo apt-key add -```

- update apt and install  
```sudo apt update && sudo apt install cloudflared -y```

# Login cloudflare
```loudflared tunnel login```

```cloudflared tunnel create <NAME>```
  
# Make config.yml file

```vim ~/.cloudflared/config.yml```
```
tunnel: <Tunnel-UUID>
credentials-file: /root/.cloudflared/<Tunnel-UUID>.json

ingress:
  - hostname: <HOST>
    service: http://localhost:8143
  - hostname: <HOST>
    service: http://localhost:3000
  - hostname: <HOST>
    service: http://localhost:19999
  # Catch-all rule, which just responds with 404 if traffic doesn't match any of
  # the earlier rules
  - service: http_status:404
```

```cloudflared tunnel validate```

```cloudflared tunnel route dns <UUID or NAME> <hostname>```

```cloudflared tunnel --config <path>/config.yml run```

# Install service

```sudo cloudflared --config <path>/config.yml service install```

```sudo systemctl start cloudflared```

```sudo systemctl enable cloudflared```

# Check tunnel

```cloudflared tunnel info```
