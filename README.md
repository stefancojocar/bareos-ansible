# Bareos

Role to setup Bareos server, bareos clients, bareos jobs and telegram messages.

# Variables
## Server

- `bareos_setup_db` - Check if postgresql DB `bareos` exists. If not, create and fill with data (`false`)
- `webui_admin_password` - Creates `password` for webui
- `webui_tls_enable` - Disable tls for webui
- `register_clients_enabled` - Register clients with bconsole
- `telegram_enabled` - Telegram used for messages
- `bot_token` - Telegram bot token
- `chat_id` - Telegram chat id
- `jobs_enabled` - Copy bareos jobs from folder files to bareos server (created manual)

```
bareos_clients:
  - name: "client1-fd"
    address: "192.168.0.2"
    password: "password_for_client1"  # Specify password for client1
  - name: "client2-fd"
    address: "192.168.0.3"
    password: "password_for_client2"  # Specify password for client2
```

Example hosts file
----------------

```
[bareos-server]
bareos-server ansible_host=192.168.0.4

[bareos-client]
bareos-client1 ansible_host=192.168.0.2
bareos-client2 ansible_host=192.168.0.3

```

Example Playbook
----------------

```
---
- name: Install and Configure Bareos Client
  hosts: bareos-client
  become: true
  roles:
    - { name: bareos-client, tags: bareos }

- name: Install and Configure Bareos Server
  hosts: bareos-server
  become: true
  roles:
    - { name: bareos-server, tags: bareos }
    - { name: bareos-jobs, tags: bareos }

```