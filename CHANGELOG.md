# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-11-02

### Added
- Support for PHP 8.1, 8.2, 8.3, and 8.4
- PHP-FPM support with configurable pools
- Modern Xdebug 3.x configuration
- Secure Composer installation with signature verification
- Comprehensive PHP extension management
- Support for Ubuntu 24.04 and Debian 11/12
- PHP-FPM pool template
- Security-focused default settings
- Extensive documentation and examples
- Multiple web server support (Apache2, PHP-FPM, CLI-only)
- Configurable PHP settings via variables
- Global Composer packages support
- Proper handlers for service restarts

### Changed
- **BREAKING**: Minimum Ansible version increased to 2.12
- **BREAKING**: Default PHP version changed from 7.2 to 8.3
- **BREAKING**: Xdebug configuration updated for Xdebug 3.x (incompatible with 2.x)
- **BREAKING**: Default Xdebug port changed from 9000 to 9003
- **BREAKING**: Variable names standardized (some renamed)
- Composer installation method completely rewritten for security
- Package management restructured for better organization
- Ubuntu version support updated (dropped 16.04, 18.04)

### Deprecated
- PHP 7.x support (still works but not recommended)

### Removed
- **BREAKING**: Support for Ubuntu 16.04 and 18.04
- **BREAKING**: Old Xdebug 2.x configuration options
- Hardcoded PHP ini paths
- Insecure Composer installation method

### Fixed
- Proper error handling in Composer installation
- Missing restart handlers
- Hardcoded values replaced with variables
- Security vulnerabilities in default configuration

### Security
- Composer signature verification
- Disabled dangerous PHP functions in FPM pools
- Restricted file permissions
- Security-focused default PHP settings

## [1.0.0] - 2019-XX-XX

### Added
- Initial release
- Basic PHP 7.2 installation
- Apache2 integration
- Basic Composer installation
- Basic Xdebug configuration
- Support for Ubuntu 16.04 and 18.04