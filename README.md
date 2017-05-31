# 🎩 trellis-database-and-uploads-migration
Ansible playbook for Trellis that manage database and uploads migration. Inspired by [hamedb89/trellis-db-push-and-pull](https://github.com/hamedb89/trellis-db-push-and-pull).

## ⚙️ Installation
1. [Download it](https://github.com/valentinocossar/trellis-database-and-uploads-migration/archive/master.zip)
2. Copy all `*.yml` files into Trellis root folder
3. Copy all `bin/*.sh` files into Trellis bin folder
4. Add `database_backup/*` to the end of the Bedrock `.gitignore` file
5. Set alias for host files as mentioned below in the hosts configuration section

### ‼️ Important
* The `database_backup` folder inside Bedrock will be automatically created if doesn't exist
* I recommend you to not perform `git` operations while running `./bin/database.sh` command, because this tool uses the Bedrock folder as temp folder to store database dump before importing/exporting it and then delete it

## 🏄 Usage
* Run `./bin/uploads.sh <environment> <site name> <mode>`
* Run `./bin/database.sh <environment> <site name> <mode>`

### 📌 Tips
* Available `<mode>` options for uploads task: `push`, `pull`
* Available `<mode>` options for database task: `push`, `pull`, `backup`

## 🛠 Hosts configuration
### Development

```
development ansible_host=192.168.50.5 ansible_connection=ssh ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/default/virtualbox/private_key

[development]
development

[web]
development
```

### Staging

```
staging ansible_host=your_server_hostname

[staging]
staging

[web]
staging
```

### Production

```
production ansible_host=your_server_hostname

[production]
production

[web]
production
```

## 🤝 Contributing

1. [Fork it](https://github.com/valentinocossar/trellis-database-and-uploads-migration/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
