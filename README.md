# Containerized n8n Application

This repository contains a Docker Compose configuration for quickly deploying an n8n automation platform with MySQL as the database backend.

## Overview

[n8n](https://n8n.io/) is a fair-code licensed workflow automation tool that helps you automate tasks across different services. This setup provides:

- n8n application (version 1.94.0)
- MySQL 8.0 database for persistent storage
- Automatic container restart
- Basic authentication support
- Custom network configuration
- Persistent data storage

## Prerequisites

- Docker
- Docker Compose
- Basic understanding of environment variables

## Quick Start

1. Clone this repository:
```bash
git clone https://github.com/yourusername/containerized-n8n-app.git
cd containerized-n8n-app
```

2. Create a `.env` file in the root directory with the following variables:
```env
# MySQL Configuration
MYSQL_DATABASE=your_n8n_database
MYSQL_USER=your_n8n_db_user
MYSQL_PASSWORD=your_secure_password
MYSQL_ROOT_PASSWORD=your_secure_root_password

# n8n Configuration
N8N_PORT=5678
N8N_HOST=localhost

# Basic Authentication (Optional, set false if not use)
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=your_username
N8N_BASIC_AUTH_PASSWORD=your_password
```

3. Start the application:
```bash
docker-compose up -d
```

4. Access n8n at `http://localhost:5678` (or your configured host/port)

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MYSQL_DATABASE` | MySQL database name | n8n |
| `MYSQL_USER` | MySQL user | n8n_user |
| `MYSQL_PASSWORD` | MySQL password | - |
| `MYSQL_ROOT_PASSWORD` | MySQL root password | - |
| `N8N_PORT` | Port for n8n web interface | 5678 |
| `N8N_HOST` | Host for n8n | localhost |
| `N8N_BASIC_AUTH_ACTIVE` | Enable/disable basic auth | false |
| `N8N_BASIC_AUTH_USER` | Basic auth username | - |
| `N8N_BASIC_AUTH_PASSWORD` | Basic auth password | - |

### Persistence

The setup includes two Docker volumes:
- `n8n_mysql_data`: Stores MySQL database files
- `n8n_data`: Stores n8n application data

### Networking

The application runs on a dedicated Docker network named `n8n-network` using the bridge driver.

## Maintenance

### Backup

To backup your data, you should:
1. Backup the MySQL database
2. Backup the n8n data volume

### Updating

To update to a newer version of n8n:
1. Update the image version in `docker-compose.yml`
2. Run `docker-compose down`
3. Run `docker-compose up -d`

## Troubleshooting

If you encounter issues:
1. Check the logs: `docker-compose logs -f`
2. Ensure all environment variables are properly set
3. Verify the MySQL container is running: `docker-compose ps`

## Security Notes

- Change default passwords in the `.env` file
- Enable basic authentication in production
- Use strong passwords
- Consider implementing SSL/TLS for production deployments

## License

This project is distributed under the terms of the LICENSE file included in this repository.
