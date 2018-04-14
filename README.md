# ansible-role-filebeat

Tested on Ansible 2.4.2 and Ubuntu 16.04

This role has some configuration options and send logs to logstash.

So please refer filebeat.yml.j2 template file for the details.

Referenced by a
[Configuring Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html) document.

## Playbook sample
This sample playbook installs Filebeat.

* **logstash_host** : The ip of logstash host
* **logstash_port** : The port of logstash service
* **enable_kibana_dashboard (optional)** : Default value is false. It set to true, filebeat dashboard will be imported on Kibana automatically.
* **kibana_host (optional)** : If enable_kibana_dashboard is set, this value will be needed
* **kibana_port (optional)** : Same as kibana_host setting
* **version (optional)** : Default value is 6.x. If you'd like to install filebeat 5.x, you should set this value to 5.x.

```yaml
- hosts: filebeat_host
  become: yes
  roles:
    - role: filebeat
      logstash_host: '{{ ansible_default_ipv4.address }}'
      logstash_port: 5044
      enable_kibana_dashboard: true
      kibana_host: '{{ ansible_default_ipv4.address }}'
      kibana_port: 5601
      prospectors:
        - { type: syslog, files: ['/var/log/auth.log'] }
```
