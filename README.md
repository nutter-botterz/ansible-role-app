# ansible-role-app

Ansible role for deploying Python Flask applications.

## Requirements

- Ansible 2.9+
- Python 3.11+ (for target host)
- Systemd (for service management)

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `app_name` | `ansible-role-app` | Application name |
| `app_version` | `1.0.0` | Application version |
| `app_port` | `5000` | Port to run on |
| `app_env` | `production` | Environment |
| `app_directory` | `/opt/{{ app_name }}` | Install directory |
| `app_user` | `app` | System user |

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: ansible-role-app
      vars:
        app_name: myapp
        app_port: 8080
```

## Installing the Role

You can install this role using `ansible-galaxy`. Here are the different ways to specify the version:

### Install Latest Version

```bash
ansible-galaxy install nutter-botterz.ansible-role-app
```

### Install Specific Release Version

```bash
# Install a specific version (e.g., v1.2.0)
ansible-galaxy install nutter-botterz.ansible-role-app,v1.2.0

# Install a specific release (without v prefix)
ansible-galaxy install nutter-botterz.ansible-role-app==1.2.0
```

### Install Latest from Specific Branch (Prerelease)

```bash
# Install latest from beta branch
ansible-galaxy install nutter-botterz.ansible-role-app,beta
```

### Install from Main Branch (Latest Stable)

```bash
# Install from main branch - gets latest stable release
ansible-galaxy install nutter-botterz.ansible-role-app,main
```

### Install from a Specific Commit

```bash
# Install from a specific commit SHA
ansible-galaxy install nutter-botterz.ansible-role-app,abcdef1
```

## Using in Requirements File

Add to your `requirements.yml`:

```yaml
# Install latest stable
- src: nutter-botterz.ansible-role-app

# Install specific version
- src: nutter-botterz.ansible-role-app
  version: 1.2.0

# Install from branch (prerelease)
- src: nutter-botterz.ansible-role-app
  version: beta

# Install from specific commit
- src: nutter-botterz.ansible-role-app
  version: abcdef1
```

Then install with:

```bash
ansible-galaxy install -r requirements.yml
```

## Testing

Run molecule tests:

```bash
molecule test
```

## License

MIT

## Author

Your Name
