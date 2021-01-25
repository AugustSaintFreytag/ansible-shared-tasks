This project is a repertoir of playbooks, task and other definitions used with the [Ansible](https://www.ansible.com/resources/get-started) automation framework. Tasks defined here can be imported as a Git Submodule and reused across projects with similar requirements in their build and deployment methodologies. The central usage scenario assumed by the authors is developing a web application locally and publishing to a virtual private server or cloud server instance. The configuration was put together for use with DigitalOcean, though it should function with other Linux-based servers, as well.

## Variables

Some tasks may use certain variables to control what kind of operations they perform through other utilities or what data is used for specific operations. Included task definitions with specific variable requirements are listed in this section.

### VPS

The set-up process prepares a cloud server instance for use and creates a suitable user account for use with SSH and Ansible automation tasks. The following variables are needed by the set-up task.

#### `server_user`

The name of the dedicated administration, automation and maintenance account, copying authentication from the root user set up during provisioning (e.g. SSH known public keys). As `ansible_user` is usually `root` for initial set-up, this variable should not be set to `root` too following best practices.

### Certificates

Creating certificates uses the publicly available service [Let's Encrypt](https://letsencrypt.org). When including the task, the following variables should be defined.

#### `server_certificate_directory`
The root directory all output and dependency files for `certbot` are placed for permanent residence on the server, commonly set to `/etc/letsencrypt`.

#### `server_certificate_log_directory`
The directory to store all logs created by `certbot` during operation, commonly set to `var/log/letsencrypt`.

#### `server_nginx_certificate_provisioning_user`
The directory to store all logs created by `certbot` during operation, commonly set to `var/log/letsencrypt`.

### Swift

The [Swift language](https://swift.org) is a general-purpose, open source programming language launched by Apple. It is the dominant development language for macOS and iOS with compilation also available for Linux and Windows. The language's core libraries are required to run command line utilities included herein. When including the task, the following variables should be defined.

#### `dep_swift_release`
The public URL of the binary release of Swift as an archive, ready for installation on the target system.

### GitLab Listener

[GitLab Listener](https://gitlab.com/apricum/gitlab-listener) is a utility for setting up autonomous releases and custom lifecycles for server environments. When including the task, the following variables should be defined.

#### `dep_listener_release`
The public URL of the precompiled and packaged binary release of GitLab Listener as an archive, ready for installation on the target system.

#### `dep_listener_service`
The public URL to a prepared `systemd` service definition file to be copied and installed for use as a start-on-launch service on a remote.

#### `listener_server_port`
The exposed port GitLab Listener listens on for events send through webhooks or custom user events.

### Cockpit Sync

The internal data and managed assets can be saved to a local archive on disk or restored from previously extracted data with [Cockpit Sync](https://gitlab.com/apricum/cockpit-sync), a command line utility to manage a Cockpit set-up running through Docker and an associated data volume. When including the task, the following variables should be defined.

#### `dep_cockpit_sync_release`
The public URL of the precompiled and packaged binary release of Cockpit Sync as an archive, ready for installation on the target system.