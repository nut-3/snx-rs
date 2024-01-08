# Rust client for Checkpoint VPN tunnels

This project contains a Rust source code of the unofficial client for Checkpoint VPN.
Based on the reverse engineered protocol used by the vendor application.

## Advantages over the 'official' snx client for Linux:

* IPSec support (faster tunnel)
* Better privacy for DNS requests: only requests for VPN-specific suffixes are routed through the tunnel
* Better integration with NetworkManager and systemd-resolved

## Implemented features

* SSL tunnel
* IPSec tunnel
* Username/password authentication with Microsoft MFA Authenticator
* Multi-factor codes input via TTY (SMS/SecurID/TOTP)

## Roadmap
 
* SAML SSO support

## Usage

There are two ways to use the application:

* Standalone service mode, selected by `-m standalone` parameter. This is the default mode. Run `snx-rs --help` to get a help with all command line parameters. In this mode the application takes connection parameters either from the command line or from the specified configuration file.
* Command mode, selected by `-m command` parameter. In this mode the application runs as a service without
 establishing a connection and awaits for the commands from the external client. Use `snxctl` utility
 to send commands to the service. The following commands are accepted:
  - `connect` - establish a connection. Parameters are taken from the `~/.config/snx-rs/snx-rs.conf` file.
  - `disconnect` - disconnect a tunnel
  - `reconnect` - drop a connection and then connect again
  - `status` - show connection status
  - `info` - dump server information in JSON format
* MFA codes will be prompted if the application has attached terminal, otherwise authentication error is triggered

## License

Licensed under [GNU Affero General Public License version 3](https://opensource.org/license/agpl-v3/)
