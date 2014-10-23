Kamel.supervisor
=================

Most of the code is from [Stouts.supervisor](https://github.com/Stouts/Stouts.supervisor), just made it work under CentOS 6.5.

Ansible role which manage [supervisor](http://supervisord.org)
Ansible role apt which help you with:

* Install and manage [supervisor](http://supervisord.org)
* Install [superlance](http://superlance.readthedocs.org)
* Manage supervisor tasks
* Provide handlers for reload and restart supervisor

#### Variables

The role variables and default values.

```yaml

supervisor_enabled: yes                   # The role is enabled
supervisor_version: "3.1.2"
supervisor_bindir: "/usr/bin"
supervisor_bin: "{{ supervisor_bindir }}/supervisord"
supervisor_pid: /var/run/supervisord.pid
supervisor_nofile: 65356                  # Set max opened files (set blank to default limits)
supervisor_cfgdir: /etc
supervisor_conf_file: "{{ supervisor_cfgdir }}/supervisord.conf"
supervisor_logdir: /var/log/supervisor    # path to logs directory
supervisor_incdir: "{{supervisor_cfgdir}}/supervisord.d" # path to include directory
supervisor_tasks: []                      # List of supervisor programs
                                          # Ex. supervisor_tasks:
                                          #       - name: <name>
                                          #         option: value
                                          #         option: value
                                          #         option: value
supervisor_events: []                     # similar to tasks/programs but for eventlisteners like crashmail
supervisor_superlance: no                 # Install superlance (http://superlance.readthedocs.org/
```

#### Usage

Add `Kamel.supervisor` to your roles and set vars in your playbook file.

Example:

```yaml

- hosts: all

  roles:
    - Kamel.supervisor

  vars:
    supervisor_tasks:
        - name: ping
          command: ping google.com
          autostart: true
          autorestart: true
    supervisor_events:
        - name: crashmail
          command: crashmail -p program -m alerts@example.com
          events: PROCESS_STATE_EXITED
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/kamelzcs/Kamel.supervisor/issues)!
