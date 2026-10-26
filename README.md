# SkyPort

SkyPort is a self-hosted panel + daemon system for managing Docker-based applications, game servers, and other containerized workloads from a single web interface.

It is built as a two-part application:

- Skyport-Panel: the web management interface
- Skyport-Node: the remote daemon responsible for Docker operations and instance control

Together, these components provide a lightweight way to deploy, monitor, and manage containerized services from a single platform.

## Overview

SkyPort follows a panel + daemon architecture:

- The panel provides the user-facing web interface and management logic
- The daemon runs on the host machine and interacts directly with Docker
- Both components communicate through a shared key and configured endpoints
- The daemon exposes HTTP and WebSocket endpoints for operational requests and live telemetry

This design makes SkyPort flexible for self-hosted environments and lightweight server orchestration.

## Features

### Panel Features
- Express-based web application
- Session-based authentication
- EJS-based views
- Modular route structure
- Instance management interface
- Deployment workflow support
- Admin routes
- WebSocket-ready communication layer

### Daemon Features
- Docker integration via Dockerode
- Instance lifecycle management
- Start, stop, and restart actions
- Volume and filesystem operations
- Archive management
- FTP metadata handling
- Database creation support
- Real-time container status and monitoring

## Architecture

```text
┌──────────────────────┐
│   Skyport-Panel       │
│   Web Interface       │
│   Express + EJS       │
└──────────┬───────────┘
           │ HTTP / WebSocket
           ▼
┌──────────────────────┐
│   Skyport-Node        │
│   Docker Host Ops     │
│   Instance Manager    │
│   Volume/FTP/DB Ops   │
└──────────────────────┘
```

## Repository Structure

```text
SkyPort/
├── LICENSE
├── Skyport-Panel/
│   ├── config.json
│   ├── index.js
│   ├── package.json
│   ├── package-lock.json
│   ├── README.md
│   ├── pages.json
│   ├── public/
│   ├── routes/
│   ├── views/
│   ├── handlers/
│   ├── exec/
│   └── sptpnl.zip
│
└── Skyport-Node/
    ├── config.json
    ├── index.js
    ├── package.json
    ├── README.md
    ├── handlers/
    ├── routes/
    └── .gitignore
```

## Tech Stack

- JavaScript
- Node.js
- Express
- EJS
- Docker
- WebSockets
- SQLite via Keyv
- MySQL support
- Tailwind CSS support

## Requirements

Before running SkyPort, make sure you have:

- Node.js 18+
- npm
- Docker installed and running
- Access to a Linux/macOS host or Docker-compatible environment
- MySQL access if using database-related features
- Permission to interact with the Docker socket

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/2208Prathamesh/SkyPort.git
cd SkyPort
```

### 2. Install the panel dependencies

```bash
cd Skyport-Panel
npm install
```

### 3. Install the daemon dependencies

```bash
cd ../Skyport-Node
npm install
```

## Configuration

### Panel configuration

Edit `Skyport-Panel/config.json`:

```json
{
  "port": 3001,
  "version": "1.0.0",
  "key": "skyport_default_key"
}
```

### Daemon configuration

Edit `Skyport-Node/config.json`:

```json
{
  "remote": "http://localhost:3001",
  "key": "your_shared_key_here",
  "port": 3002,
  "version": "0.2.1",
  "mysql": {
    "host": "localhost",
    "user": "root",
    "password": ""
  },
  "ftp": {
    "ip": "127.0.0.1",
    "port": 3003
  }
}
```

Important:
- The `key` values in both config files should match.
- Change default values before exposing the project beyond a local environment.

## Running the Application

### Start the daemon

```bash
cd Skyport-Node
node .
```

### Start the panel

```bash
cd Skyport-Panel
node .
```

Then open:

```text
http://localhost:3001
```

## Typical Workflow

1. Start the daemon on the target host machine
2. Start the panel on the management machine
3. Configure matching keys between both components
4. Add or manage server instances through the UI
5. Use the daemon for deploys, volume functions, FTP metadata, power actions, and monitoring

## Development Status

SkyPort is an early-stage project focused on self-hosted Docker management. It includes a working architecture and real operational logic, but it should be considered experimental and not production-hardened without further security review and testing.

This project is best suited for:

- local development
- self-hosted labs
- experimental deployments
- learning and extending Docker-based panel systems

## Security Considerations

Before using SkyPort in a real environment:

- Change all default keys and secrets
- Restrict access to panel and daemon ports
- Use TLS / reverse proxy in front of the panel
- Limit Docker access to trusted users only
- Review filesystem permissions and host access
- Harden session and authentication handling

## Contributing

Contributions are welcome. If you would like to improve the project:

- open an issue
- suggest a feature
- improve code quality
- improve the security model
- add documentation and examples
- submit a pull request

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Acknowledgements

SkyPort is inspired by modern self-hosted server management systems and aims to provide a simple Docker-first control experience for managing applications and game servers.
