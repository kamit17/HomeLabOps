# HomeLabOps LDAP Docker Setup

## Project Overview

This project contains a Dockerized setup for an OpenLDAP server with phpLDAPadmin for easy LDAP directory management. It also includes Jenkins and a custom webapp service. The OpenLDAP service uses the osixia/openldap image and supports bootstrapping LDAP data either with built-in defaults or via custom LDIF files.

## Features

- OpenLDAP container with secure admin via environment variables
- phpLDAPadmin for web-based LDAP directory browsing and editing
- Jenkins CI server to automate workflows
- Custom webapp container example included
- Data persisted in Docker volumes for stateful LDAP and Jenkins data
- Support for custom bootstrap LDIF import or default baked-in LDAP tree


## Getting Started

### Prerequisites

- Docker Engine
- Docker Compose
- Basic knowledge of LDAP and Docker


### Setup and Running

1. Clone this repository:

```bash
git clone <repo-url>
cd HomeLabOps/docker
```

2. Set your LDAP admin password environment variable:

```bash
export LDAP_ADMIN_PASSWORD=YourStrongPasswordHere
```

3. Ensure your `bootstrap.ldif` exists at `../ldap/ldif/bootstrap.ldif` (optional if using custom bootstrap).
4. Start the containers with fresh volumes:

```bash
docker-compose down -v
docker-compose up -d
```

5. Access phpLDAPadmin at [https://localhost:6443](https://localhost:6443)
Bind DN: `cn=admin,dc=homelab,dc=local`
Password: LDAP_ADMIN_PASSWORD you set
6. Use Apache Directory Studio or other LDAP tools at `ldap://localhost:389` with the same bind DN and password.

## Usage Notes

- With no custom LDIF mounted, OpenLDAP initializes with a minimal default directory (base domain and organization).
- To bootstrap custom LDAP entries, add your LDIF to `../ldap/ldif/bootstrap.ldif` and rebuild or reinitialize the container.
- LDAP data is persisted in Docker volumes even after container restarts.
- Modify LDAP structure and users using phpLDAPadmin or CLI tools after startup when using default setup.


## Contributing

Contributions, issues, and feature requests are welcome! Please fork the repo and submit pull requests or open issues.

## License

This project is licensed under the MIT License.

***

