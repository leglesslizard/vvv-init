You may want to [read our overview](https://github.com/cftp/vvv-init/wiki).

# How to use this example bootstrap

## Basic setup

1. Run a search and replace for `site-name` to whatever the subdomain for your development site will be
2. Run a search and replace for `site_name` to whatever the database name for your development site will be
3. Run a search and replace for `Site Name` to whatever the human readable name for your development site will be
4. Remove these initial instructions, leaving the "Development environment bootstrap" heading and everything below it
5. Create a deploy user on your GitHub repo, create a set of private and public keys for this user and upload the public key to GitHub. Copy the public *and private* keys for this user into the `ssh` folder of this bootstrap. Give this user pull permissions. **NOTE: You have a potential security issue if you give this user push (or GitHub admin) permissions, as you are distributing the private key for the user!**
6. Amend the "Development environment bootstrap" heading and paragraph below so it reflects your purpose for the particular development environment
7. Test everything works as expected in a [VVV](https://github.com/10up/varying-vagrant-vagrants/) context
8. Copy or `git push` to a new repo or new branch in an existing repo
9. Point people towards the `readme.md` in the repo you pushed to, so they can get going

## Using Composer

See [Composer](https://github.com/cftp/vvv-init/wiki/Introduction#composer) and [Private Repos](https://github.com/cftp/vvv-init/wiki/Introduction#private-repos)

The private and public keys are not included in this publically distributed repo, you will need to copy these into the `.ssh` folder.

You will need to include the Composer autoload, so add this near the top of `wp-config.php` (which is a file you may wish to have under version control, separating out the environment specific portion into a non-version controlled `wp-config-local.php`):

```php
// composer
if ( file_exists( __DIR__ . '/wp-content/vendor/autoload.php' ) ) {
	require __DIR__ . '/wp-content/vendor/autoload.php';
}
```

You've then got the `wrapper-composer.sh` and `build-wpengine.sh` scripts available to you.

# Development environment bootstrap

This site bootstrap is designed to be used with [Varying Vagrants Vagrant](https://github.com/10up/varying-vagrant-vagrants/) and a WordPress single site, the code for which is stored as a monolithic (or submoduled, probably) Git(Hub) repo.

To get started:

1. If you don't already have it, clone the [Vagrant repo](https://github.com/10up/varying-vagrant-vagrants/) (perhaps into your `~/Vagrants/` directory, you may need to create it if it doesn't already exist)
2. Install the Vagrant hosts updater: `vagrant plugin install vagrant-hostsupdater`
3. Clone this branch of this repo into the `www` directory of your Vagrant as `www/site-name`
4. If your Vagrant is running, from the Vagrant directory run `vagrant halt`
5. Followed by `vagrant up --provision`.  Perhaps a cup of tea now? The initial provisioning may take a while.
6. If you want the user uploaded files, you'll need to download these separately

Then you can visit:
* [http://site-name.dev/](http://site-name.dev/)

This script is free software, and is released under the terms of the <abbr title="GNU General Public License">GPL</abbr> version 2 or (at your option) any later version. See license.txt.
