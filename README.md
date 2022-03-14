# SOCKS5 Proxy Actions
SOCKS5 Proxy hosted on GitHub Actions.

Proof of concept Chisel's SOCKS5 Proxy running on GitHub Actions.

As GitHub Actions runner does not have a public IP address, we use Cloudflare Tunnel to have a tunnel to GitHub Actions runner.

Your Computer > Cloudflare > GitHub Actions runner > GitHub Actions' Internet

## Usage
1. Setup Cloudflare Tunnel Client by following instructions on [setup-cloudflared README.md](https://github.com/AnimMouse/setup-cloudflared/blob/main/README.md).
2. At the config.yaml, set `url:` to `http://localhost:8080`.
3. Run the workflow specifying the time to run.
4. Connect to your chisel websocket by running `chisel client https://example.com socks`.
5. Connect your browser to chisel's SOCKS5 proxy by setting proxy settings to `localhost:1080`.

### Example config.yaml file
Using url:
```yaml
url: http://localhost:8080
tunnel: deadbeef-1234-4321-abcd-123456789abc
credentials-file: /home/runner/.cloudflared/deadbeef-1234-4321-abcd-123456789abc.json
```
Using ingress:
```yaml
tunnel: deadbeef-1234-4321-abcd-123456789abc
credentials-file: /home/runner/.cloudflared/deadbeef-1234-4321-abcd-123456789abc.json
ingress:
  - service: http://localhost:8080
```