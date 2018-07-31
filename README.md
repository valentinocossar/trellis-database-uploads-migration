# 🎩 trellis-database-uploads-migration
Ansible playbook for Trellis that manage database and uploads migration. Inspired by [hamedb89/trellis-db-push-and-pull](https://github.com/hamedb89/trellis-db-push-and-pull).

## ⚙️ Installation
1. [Download latest release](https://github.com/valentinocossar/trellis-database-uploads-migration/releases/latest)
2. Copy `CHANGELOG-TRELLIS-DATABASE-UPLOADS-MIGRATION.md` file into Trellis root folder (so you can always know the version of the tool you are using)
3. Copy all `*.yml` files into Trellis root folder
4. Copy all `bin/*.sh` files into Trellis bin folder
5. Add `database_backup/*` to the end of the Bedrock `.gitignore` file
6. Set alias for host files as mentioned below in the hosts configuration section

### ‼️ Important
* Tested up to Ansible 2.6.1
* This tool doesn't work with Ansible 2.4.1.0 due to a bug (see [#9](https://github.com/valentinocossar/trellis-database-uploads-migration/issues/9))
* The development vagrant VM must be powered on every time you run a command, this because the tool checks if the site folder exists and its name is the same of the `local_path` parameter in `wordpress_sites.yml`
* The `database_backup` folder inside Bedrock will be automatically created if doesn't exist
* I recommend you to not perform `git` operations while running `./bin/database.sh` command, this because the tool uses the Bedrock folder as temp folder to store database dump before importing/exporting it and then delete it
* To support url search and replace for Trellis 0.9.8 and lower, remove `.canonical` from variables `url_from` and `url_to` in the files `database-pull.yml` and `database-push.yml`
* This tool hasn't been tested with a multisite configuration, any help with this implementation would be appreciated
* This tool has only been tested with macOS and Ubuntu 18.04 LTS, any help with other operating systems would be appreciated

## 🏄 Usage
* Run `./bin/uploads.sh <environment> <site name> <mode>`
* Run `./bin/database.sh <environment> <site name> <mode>`

### 📌 Tips
* Available `<mode>` options for uploads task: `push`, `pull`
* Available `<mode>` options for database task: `push`, `pull`, `backup`
* The `push` is for sending to the selected environment and the `pull` for receiving from it
* The `backup` is for backup the database of the selected environment

## 🛠 Hosts configuration
### Development
```
[development]
development_host ansible_host=192.168.50.5 ansible_connection=ssh ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/default/virtualbox/private_key ansible_ssh_extra_args="-o StrictHostKeyChecking=no -o GlobalKnownHostsFile=/dev/null -o UserKnownHostsFile=/dev/null -o IdentitiesOnly=yes -o ForwardAgent=yes"
development_host

[web]
development_host
```

### Staging
```
[staging]
staging_host ansible_host=your_server_hostname
staging_host

[web]
staging_host
```

### Production
```
[production]
production_host ansible_host=your_server_hostname
production_host

[web]
production_host
```
## 🤝 Contributing

1. [Fork it](https://github.com/valentinocossar/trellis-database-uploads-migration/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
