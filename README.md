[![GitHub Continious Integration Workflow](https://github.com/grandegiraffo/pihole-doh/workflows/CI/badge.svg "GitHub Continious Integration Workflow")](https://github.com/grandegiraffo/pihole-doh/actions?query=workflow%3ACI)

# What is this?

A tiny [Docker Compose](https://docs.docker.com/compose/) project for setting up my [Pi-Hole](https://github.com/pi-hole/docker-pi-hole) in conjuction with [DNS-over-HTTPS Cloudflared](https://github.com/crazy-max/docker-cloudflared).

# How do I get started?

1. Set up Docker on a always-on fixed IP machine on your LAN.
2. Run a few terminal commands:

```console
git clone https://github.com/grandegiraffo/pihole-doh.git

cd pihole-doh

docker-compose up --detach
```

3. Tell your DHCP-server/router to use the fixed IP as prefered DNS and enjoy those secure lookups and ad-free surfing.
