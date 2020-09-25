This project is a repertoir of playbooks, task and other definitions used with the [Ansible](https://www.ansible.com/resources/get-started) automation framework. Tasks defined here can be imported as a Git Submodule and reused across projects with similar requirements in their build and deployment methodologies. The central usage scenario assumed by the authors is developing a web application locally and publishing to a virtual private server or cloud server instance. The configuration was put together for use with DigitalOcean, though it should function with other Linux-based servers, as well.

## Variables

Some tasks may use certain variables to control what kind of operations they perform through other utilities or what data is used for specific operations. Included task definitions with specific variable requirements are listed in this section.

### VPS Set-Up

The set-up process prepares a cloud server instance for use and creates a suitable user account for use with SSH and Ansible automation tasks. The following variables are needed by the set-up task.

#### `server_user`

The name of the dedicated administration, automation and maintenance account, copying authentication from the root user set up during provisioning (e.g. SSH known public keys). As `ansible_user` is usually `root` for initial set-up, this variable should not be set to `root` too following best practices.

### Certificate Provisioning

Creating certificates uses the publicly available service [Let's Encrypt](https://letsencrypt.org). When including the task, the following variables should be defined.

#### `server_certificate_directory`
The root directory all output and dependency files for `certbot` are placed for permanent residence on the server, commonly set to `/etc/letsencrypt`.

#### `server_certificate_log_directory`
The directory to store all logs created by `certbot` during operation, commonly set to `var/log/letsencrypt`.

#### `server_certificate_provisioning_user`
The directory to store all logs created by `certbot` during operation, commonly set to `var/log/letsencrypt`.

### GitLab Listener

[Listener](https://gitlab.com/apricum/gitlab-listener) is a utility for setting up autonomous releases and custom lifecycles for server environments. When including the task, the following variables should be defined.

#### `dep_listener_release_root`
The path to precompiled and packaged releases on the host machine to be copied to a remote (without a trailing slash).

#### `dep_listener_release_name`
The name of the package file for the current release to be loaded and installed. Expected to be located in the release root at `dep_listener_release_root`. Example: `"GitLabListener-0.4.0.tar.gz"`.

#### `dep_listener_service`
The path to a prepared `systemd` service definition file to be copied and installed for use as a start-on-launch service on a remote.