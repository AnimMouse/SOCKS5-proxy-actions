# SOCKS5 Proxy Actions
SOCKS5 Proxy hosted on GitHub Actions.

Proof of concept Chisel's SOCKS5 Proxy running on GitHub Actions.

As GitHub Actions runner does not have an accessible IP address, we use Cloudflare Tunnel to have a tunnel to GitHub Actions runner.

Your Computer > Cloudflare > GitHub Actions runner > GitHub Actions' Internet

## Usage

1. Setup Cloudflare Tunnel Client by following instructions on [setup-cloudflared README.md](https://github.com/AnimMouse/setup-cloudflared/blob/main/README.md).
2. At the config.yml, set `service:` to `http://localhost:8080` at `ingress:`.
```
ingress:
  - service: http://localhost:8080
```
3. Run the workflow.
4. Connect to your chisel websocket by running `chisel client https://example.com/ socks`.
5. Connect your browser to chisel's SOCKS5 proxy by setting proxy settings to `localhost:1080`.