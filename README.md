
## Setup dev

Install grav-admin from zip
Install php
May need to manually install php-gd and turn this extension on in `/etc/php/php.ini`.

```bash
cd grav-admin/

# remove default 'user' folder
rm -r user

# symlink 'luvan-skeleton' as 'user' folder
ln -s ~/my/location/luvan-skeleton ~/my/location/grav-admin/user

# install dependencies (plugins)
bin/grav install

# symlink 'luvan-pages' as 'user/pages' folder
ln -s ~/my/location/luvan-pages ~/my/location/grav-admin/user/pages

# symlink 'luvan-theme' as 'user/theme/luvan' folder
ln -s ~/my/location/luvan-theme ~/my/location/grav-admin/user/themes/luvan
```

## Run dev

Run the simple dev server from `grav-admin/` :
```bash
php -S localhost:8000 system/router.php
```

watch scss modifications :
```bash
cd user/themes/luvan
scss --watch scss:css
```

## Deploy with YUNOHOST

install grav as a yunohost app

```bash
# from grav folder in /var/www/

# remove base user folder
rm -r user

# clone the new user folder
git clone https://github.com/Axolotle/luvan-website.git user

# install plugins
bin/gpm install problems
bin/gpm install error
bin/gpm install admin
bin/gpm install pagination

# add the content repo ('pages' folder)
cd user/
git clone https://github.com/Axolotle/luvan-pages pages

# add the theme
cd theme/
git clone https://github.com/Axolotle/luvan-theme luvan

# reset files and folders ownership
chown -R grav:grav /var/www/grav/user

# change the admin route
vim user/config/plugins/admin.yaml
# then change the 'route' value
```
