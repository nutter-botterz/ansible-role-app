# ansible-role-template

 Ansible role for [purpose: e.g., managing Nginx, deploying Python apps, configuring Docker, etc.]

## Requirements

- Ansible 2.9+
- [Any additional requirements]

## Role Variables

Available variables with defaults:

```yaml
# Variable: example_variable
# Default: "default_value"
# Description: What this variable does
example_variable: "default_value"
```

## Dependencies

[Optional: list any roles or collections this depends on]

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: namespace.role_name
      vars:
        variable_name: value
```

## Installation

```bash
# Install from Galaxy
ansible-galaxy install namespace.role_name

# Or add to requirements.yml
- src: namespace.role_name
  version: version
```

## Testing

```bash
# Run molecule tests
molecule test

# Or converge only (faster for dev)
molecule converge
```

## License

MIT

## Author

[Your Name]