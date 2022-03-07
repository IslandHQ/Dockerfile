# quickly use
```cloudflared tunnel --url http://localhost:8080```

- if after login
```cloudflared tunnel --hostname test.example.com --url http://localhost:8080```

# download
```sh
sudo wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 && sudo mv ./cloudflared-linux-amd64 /usr/local/bin/cloudflared && sudo chmod a+x /usr/local/bin/cloudflared && sudo cloudflared update
```

# login
```cloudflared login``` or ```cloudflared tunnel login```

# make tunnel
```cloudflared tunnel create <TUNNEL-NAME>```

# make config file
```touch $HOME/.cloudflared/config.yml```

```vim $HOME/.cloudflared/config.yml```

```config.yml
tunnel: <Tunnel-UUID>
credentials-files: <Tunnel-UUID>.json

ingress:
  - hostname: test-1.example.com
    service: https://localhost:443
    # Disables TLS verification
    originRequest:
      noTLSVerify: true
  - hostname: test-2.example.com
    service: http://localhost:3000
  # Rules can match the request's hostname to a wildcard character:
  - hostname: '*.example.com'
    service: https://localhost:8002
  # Example of a request over TCP:
  - hostname: example.com
    service: tcp://localhost:8000
  # Example of a request over a Unix socket:
  - hostname: staging.example.com
    service: unix:/home/production/echo.sock
  # Example of a request mapping to the Hello World test server:
  - hostname: test.example.com
    service: hello_world
  # catch-all
  - service: http_status:404
```

```cloudflared tunnel ingress validate```

```cloudflared tunnel route dns <TUNNEL-NAME> test-1.example.com``` overwrite dns `-f`

```cloudflared tunnel run```
