# Modern PHP Ansible Role

A comprehensive Ansible role for installing and configuring PHP with support for multiple PHP versions, web servers (Apache2, PHP-FPM), and development tools.

## Features

- ✅ Support for PHP 8.1, 8.2, 8.3, and 8.4
- ✅ Multiple web server configurations (Apache2, PHP-FPM, CLI-only)
- ✅ Secure Composer installation with signature verification
- ✅ Modern Xdebug 3.x configuration
- ✅ Comprehensive PHP extension management
- ✅ PHP-FPM pool configuration
- ✅ Security-focused default settings
- ✅ Support for Ubuntu 20.04, 22.04, 24.04 and Debian 11, 12

## Requirements

- Ansible >= 2.12
- Target systems: Ubuntu 20.04+, Debian 11+
- Privileged access (sudo) on target hosts

## Role Variables

### Core Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `php_version` | `"8.3"` | PHP version to install (8.1, 8.2, 8.3, 8.4) |
| `php_webserver` | `apache2` | Web server type (`apache2`, `fpm`, `cli-only`) |
| `use_ppa` | `true` | Use Ondrej PPA for latest PHP versions |

### PHP Extensions

| Variable | Default | Description |
|----------|---------|-------------|
| `php_packages` | See defaults | Core PHP packages |
| `php_extensions` | See defaults | Additional PHP extensions |
| `php_system_packages` | See defaults | System packages (APCu, etc.) |

### Composer Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `install_composer` | `true` | Install Composer |
| `composer_version` | `"2"` | Composer major version |
| `composer_keep_updated` | `true` | Keep Composer updated |
| `composer_global_packages` | `[]` | Global packages to install |

### Xdebug Configuration (Xdebug 3.x)

| Variable | Default | Description |
|----------|---------|-------------|
| `install_xdebug` | `false` | Install and configure Xdebug |
| `xdebug_mode` | `"debug,coverage"` | Xdebug modes |
| `xdebug_start_with_request` | `"trigger"` | When to start Xdebug |
| `xdebug_client_port` | `9003` | Debug client port |
| `xdebug_client_host` | `"host.docker.internal"` | Debug client host |
| `xdebug_idekey` | `"VSCODE"` | IDE key for debugging |

### PHP-FPM Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `php_fpm_user` | `www-data` | FPM process user |
| `php_fpm_group` | `www-data` | FPM process group |
| `php_fpm_listen` | `/run/php/php{{ php_version }}-fpm.sock` | FPM listen socket |
| `php_fpm_pm` | `dynamic` | Process manager type |
| `php_fpm_max_children` | `50` | Maximum child processes |

### PHP Settings

| Variable | Default | Description |
|----------|---------|-------------|
| `php_memory_limit` | `"256M"` | PHP memory limit |
| `php_max_execution_time` | `60` | Maximum execution time |
| `php_upload_max_filesize` | `"64M"` | Maximum upload file size |
| `php_post_max_size` | `"64M"` | Maximum POST data size |
| `php_display_errors` | `false` | Display errors |
| `php_log_errors` | `true` | Log errors |

## Example Playbooks

### Basic Apache Setup

```yaml
- hosts: webservers
  become: true
  roles:
    - role: php
      vars:
        php_version: "8.3"
        php_webserver: apache2
        install_composer: true
        install_xdebug: false
```

### PHP-FPM with Nginx

```yaml
- hosts: webservers
  become: true
  roles:
    - role: php
      vars:
        php_version: "8.3"
        php_webserver: fpm
        install_composer: true
        php_fpm_listen: "127.0.0.1:9000"
```

### Development Environment with Xdebug

```yaml
- hosts: development
  become: true
  roles:
    - role: php
      vars:
        php_version: "8.3"
        php_webserver: apache2
        install_composer: true
        install_xdebug: true
        composer_global_packages:
          - "phpunit/phpunit"
          - "friendsofphp/php-cs-fixer"
        php_display_errors: true
        xdebug_mode: "debug,coverage,profile"
```

### Custom PHP Extensions

```yaml
- hosts: webservers
  become: true
  roles:
    - role: php
      vars:
        php_version: "8.3"
        php_extensions:
          - "php{{ php_version }}-curl"
          - "php{{ php_version }}-gd"
          - "php{{ php_version }}-mysql"
          - "php{{ php_version }}-redis"
          - "php{{ php_version }}-imagick"
```

## Directory Structure

```
php/
├── defaults/main.yml          # Default variables
├── handlers/main.yml          # Event handlers
├── meta/main.yml             # Role metadata
├── tasks/
│   ├── main.yml             # Main tasks
│   ├── composer.yml         # Composer installation
│   └── xdebug.yml          # Xdebug configuration
├── templates/
│   └── www.conf.j2         # PHP-FPM pool template
├── tests/
│   ├── inventory           # Test inventory
│   └── test.yml           # Test playbook
└── README.md              # This file
```

## Dependencies

None

## Testing

Run the test playbook:

```bash
ansible-playbook -i tests/inventory tests/test.yml
```

## Compatibility

| OS | Version | Status |
|----|---------|--------|
| Ubuntu | 20.04 (Focal) | ✅ Supported |
| Ubuntu | 22.04 (Jammy) | ✅ Supported |
| Ubuntu | 24.04 (Noble) | ✅ Supported |
| Debian | 11 (Bullseye) | ✅ Supported |
| Debian | 12 (Bookworm) | ✅ Supported |

## Security Considerations

- Composer is installed with signature verification
- PHP-FPM runs with restricted permissions
- Dangerous PHP functions are disabled in FPM pools
- Error display is disabled by default in production
- File upload restrictions are enforced

## Changelog

### v2.0.0 (2025)
- Complete modernization
- Added PHP 8.1-8.4 support
- Added PHP-FPM support
- Modern Xdebug 3.x configuration
- Secure Composer installation
- Comprehensive documentation

### v1.0.0 (2019)
- Initial release
- PHP 7.2 support
- Basic Apache configuration

## License

MIT

## Author Information

Created by Mike Horrocks in 2019. Modernized in 2025.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

For bugs and feature requests, please create an issue on GitHub.
