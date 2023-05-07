# SOCKS5 Proxy Actions
SOCKS5 Proxy hosted on GitHub Actions.

Proof of concept Chisel's SOCKS5 Proxy running on GitHub Actions.

As GitHub Actions runner does not have a public IP address, we use Cloudflare Tunnel to have a tunnel to GitHub Actions runner.

This GitHub action participated on [GitHub Actions Hackathon 2021](https://dev.to/animmouse/hosting-a-socks5-proxy-on-github-actions-27mj), but sadly, it lost.

Your Computer > Cloudflare > GitHub Actions runner > GitHub Actions' Internet

## Deprecation
This workflow is deprecated as this may potentially violate the [GitHub Actions Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-for-additional-products-and-features#actions), please use [AnimMouse/SOCKS5-Proxy-Codespaces](https://github.com/AnimMouse/SOCKS5-Proxy-Codespaces) instead.

> Actions should not be used for:
> - cryptomining;
> - disrupting, gaining, or attempting to gain unauthorized access to, any service, device, data, account, or network (other than those authorized by the GitHub Bug Bounty program);
> - the provision of a stand-alone or integrated application or service offering the Actions product or service, or any elements of the Actions product or service, for commercial purposes;
> - any activity that places a burden on our servers, where that burden is disproportionate to the benefits provided to users (for example, don't use Actions as a content delivery network or as part of a serverless application, but a low benefit Action could be ok if it’s also low burden); or
> - if using GitHub-hosted runners, any other activity unrelated to the production, testing, deployment, or publication of the software project associated with the repository where GitHub Actions are used.

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