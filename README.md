# Ansible role `vsftpd`

[![Build Status](https://travis-ci.org/bertvv/ansible-role-vsftpd.svg?branch=master)](https://travis-ci.org/bertvv/ansible-role-vsftpd)

An Ansible role for setting up Vsftpd under CentOS/RHEL 7, Fedora 25, Ubuntu LTS 12.04 (precise), or 14.04 (trusty). Specifically, the responsibilities of this role are to:

- install necessary packages
- manage configuration
- manage SELinux settings, when it is enabled

Configuring the firewall is outside the scope of this role. Use another role suitable for your distribution, e.g. [bertvv.rh-base](https://galaxy.ansible.com/bertvv/rh-base).

If you like/use this role, please consider giving it a star or reviewing it on Ansible Galaxy. Thanks!

## Requirements

No specific requirements

## Role Variables

Please refer to the [vsftpd.conf(5)](http://vsftpd.beasts.org/vsftpd_conf.html) man page for detailed info on the variables listed below. The variable names here are consistent with the Vsftpd configuration parameters.

| Variable                      | Default | Comments (type)                                                                             |
| :---                          | :---    | :---                                                                                        |
| `vsftpd_anon_root`            | -       | Directory for guest users. Defaults to home directory of the `ftp` user.                    |
| `vsftpd_anonymous_enable`     | true    | Specifies whether anonymous logins are permitted or not.                                    |
| `vsftpd_config`               | -       | List of dicts for other options not available as role variables. See below.                 |
| `vsftpd_connect_from_port_20` | true    | Controls whether PORT style data connections use port 20 on the server. machine.            |
| `vsftpd_listen`               | true    | When enabled, run `vsftpd` in standalone mode. Mutually exclusive with `vsftpd_listen_ipv6` |
| `vsftpd_listen_ipv6`          | false   | When enabled, run `vsftpd` in standalone mode, over IPv6.                                   |
| `vsftpd_local_enable`         | false   | Specifies whether logins from registered users are permitted or not.                        |
| `vsftpd_local_root`           | -       | Directory for registered users. Defaults to their home directory.                           |
| `vsftpd_local_umask`          | 022     | The value that the umask for file creation is set to for local users.                       |
| `vsftpd_syslog_enable`        | true    | If enabled, log output goes to the system log (`journalctl -u vsftpd.service`)              |
| `vsftpd_write_enable`         | true    | Controls whether any FTP commands which change the filesystem are allowed or not.           |

Vsftpd options not provided in the list above can be added with `vsftpd_options` as a list of dicts with two fields, `key` and `value`. **Remark** that boolean options should be specified with `'YES'` or `'NO` *within quotes*. Otherwise the Jinja template engine will interpret these values as booleans instead of strings an translate them into, "True" and "False", respectively.

```Yaml
vsftpd_options:
  - key: xferlog_enable
    value: 'YES'
  - key: xferlog_file
    value: /var/log/vsftp_xfer.log
```

## Dependencies

No dependencies.

## Example Playbook

See the test playbooks in either the [Vagrant](https://github.com/bertvv/ansible-role-vsftpd/blob/vagrant-tests/test.yml) or [Docker](https://github.com/bertvv/ansible-role-vsftpd/blob/docker-tests/test.yml) test environment. See the section Testing for details.

## Testing

There are two types of test environments available. One powered by Vagrant, another by Docker. The latter is suitable for running automated tests on Travis-CI. Test code is kept in separate orphan branches. For details of how to set up these test environments on your own machine, see the README files in the respective branches:

- Vagrant: [tests](https://github.com/bertvv/ansible-role-vsftpd/tree/tests)
- Docker: [docker-tests](https://github.com/bertvv/ansible-role-vsftpd/tree/docker-tests)

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome. The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork. Github can then easily create a PR based on that branch.

## License

2-clause BSD license, see [LICENSE.md](LICENSE.md)

## Contributors

- [Bert Van Vreckem](https://github.com/bertvv/) (maintainer)

