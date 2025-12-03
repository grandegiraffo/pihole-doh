[![GitHub Continuous Integration Workflow](https://github.com/grandegiraffo/pihole-doh/workflows/CI/badge.svg "GitHub Continuous Integration Workflow")](https://github.com/grandegiraffo/pihole-doh/actions?query=workflow%3ACI)

# What is this?

A tiny [Docker Compose](https://docs.docker.com/compose/) project for setting up my [Pi-Hole](https://github.com/pi-hole/docker-pi-hole) in conjunction with [DNS-over-HTTPS Cloudflared](https://github.com/crazy-max/docker-cloudflared).

# How do I get started?

1. Set up Docker on an always-on fixed IP machine on your LAN.
2. Run a few terminal commands:

```console
git clone https://github.com/grandegiraffo/pihole-doh.git

cd pihole-doh

# Set your Pi-hole admin password
export PIHOLE_WEBPASSWORD="your-secure-password-here"

docker compose up --detach
```

3. Tell your DHCP-server/router to use the fixed IP as preferred DNS and enjoy those secure lookups and ad-free surfing.

## Security Notes

- The default admin password is set via the `PIHOLE_WEBPASSWORD` environment variable
- For production use, set a strong password before starting the containers
- Consider using Docker secrets for better password management in production environments

## Resource Management

The compose file includes memory limits for all services:
- Pi-hole: 512MB limit, 256MB reserved
- Cloudflared: 128MB limit, 64MB reserved
- Watchtower: 128MB limit, 64MB reserved

All services include health checks for better reliability and faster startup detection.
