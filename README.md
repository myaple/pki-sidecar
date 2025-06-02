# pki-sidecar

A Docker Compose setup that provides an nginx proxy container with PKI client certificate support for secure API access.

## Overview

This repository contains a Docker Compose configuration with two services:

1. **nginx-proxy**: An nginx container that proxies HTTP requests to HTTPS://example.com/API/v1 with client certificate authentication
2. **goose**: A development container that can access the proxy service

## Prerequisites

- Docker and Docker Compose installed
- Client certificates and keys available in `/home/matt/.pki/` directory:
  - `client.crt` - Client certificate
  - `client.key` - Client private key

## Usage

1. Start the services:
   ```bash
   docker-compose up -d
   ```

2. The nginx proxy will be available internally on the `pki-network` at `http://nginx-proxy/v1` (not exposed to host)

3. From the goose container, you can access the proxy:
   ```bash
   curl http://nginx-proxy/v1/your-endpoint
   ```

4. Stop the services:
   ```bash
   docker-compose down
   ```

## Configuration

- **nginx.conf**: Contains the nginx configuration for proxying and client certificate handling
- **docker-compose.yml**: Defines the services and network configuration

## Network

The services communicate over a private Docker network (`pki-network`) and are not directly exposed to the host, providing isolation while allowing inter-container communication.