# 🎩 trellis-database-and-uploads-migration
Ansible playbook for Trellis that manage database and uploads migration. Inspired by [hamedb89/trellis-db-push-and-pull](https://github.com/hamedb89/trellis-db-push-and-pull).

## ⚙️ Installation
1. Copy all `*.yml` files into Trellis root folder
2. Copy all bin/*.sh` files into Trellis bin folder
3. Set alias for host files as mentioned below in the hosts configuration section

## 🏄 Usage
* Run `./bin/uploads.sh <environment> <site name> <mode>`
* Run `./bin/database.sh <environment> <site name> <mode>`

### 📌 Tips
* Available `<mode>` options for uploads task: `push`, `pull`
* Available `<mode>` options for database task: `push`, `pull`, `backup`

## 🛠 Hosts configuration
### Development

```
development 192.168.50.5 ansible_connection=ssh ansible_user=vagrant ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/default/virtualbox/private_key
[development]
development

[web]
development
```

### Staging

```
staging your_server_hostname

[staging]
staging

[web]
staging
```


### Production
```
production your_server_hostname
[production]
production

[web]
production
```
