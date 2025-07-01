# Swan Provider Setup Guide

Become a Swan Provider and contribute to the decentralized AI and storage network. This guide covers prerequisites, installation, configuration, and network onboarding.

## Prerequisites

- Linux or macOS server (recommended)
- Docker and Docker Compose installed
- Stable internet connection
- Sufficient CPU, RAM, and storage resources
- (Optional) Public IP address for maximum connectivity

## Installation

1. **Clone the Swan Provider repository:**
   ```sh
git clone https://github.com/filswan/swan-provider.git
cd swan-provider
```
2. **Copy and edit the configuration file:**
   ```sh
cp .env.example .env
# Edit .env to set your provider details, resource limits, and API keys
```
3. **Start the provider service:**
   ```sh
docker-compose up -d
```

## Configuration

- Edit `.env` to set:
  - Provider name and contact info
  - Resource limits (CPU, RAM, storage)
  - API keys for Swan Cloud integration
  - Network settings (ports, public IP)

## Joining the Network

- Register your provider on the [Swan Cloud Provider Portal](https://provider.swancloud.ai/)
- Monitor your node status and earnings via the portal dashboard
- Keep your software up to date for security and performance

## Troubleshooting

- Check logs with `docker-compose logs`
- Consult the [Provider FAQ](faq.md) for common issues
- Reach out to the [community support](../../community/support.md) if you need help 