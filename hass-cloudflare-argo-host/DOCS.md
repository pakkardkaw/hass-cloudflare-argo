# Cloudflare Argo Home Assistant Add-on

## Configuration

1. Setup Cloudflare Tunnel as indicated [here](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/tunnel-guide/#local-setup-cli-setup) in step 1-3.
2. Add Cloudflare DNS CNAME record pointing `{hostname}` to `{UUID}.cfargotunnel.com`.
4. Upload file in `~/.cloudflared/{UUID}.json` to `/config/cloudflare_argo/{UUID}.json`.
5. Upload file `config.yml` to `/config/cloudflare_argo/config.yml`.
6. Start Addon.

Example config.yml
```
tunnel: {UUID}
credentials-file: /config/cloudflare_argo/{UUID}.json
ingress:
  - hostname: {hostname}
    service: http://127.0.0.1:{hass_port}
  - service: http_status:404
```

You must add this configuration into "main configuration" for see real-user IP.
```
homeassistant:
  external_url: "https://{hostname}"
http:
  use_x_forwarded_for: true
  trusted_proxies: 
    - 127.0.0.1
```