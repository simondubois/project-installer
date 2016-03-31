
# project-installer

<p align="center">
<img src="https://raw.githubusercontent.com/simondubois/project-installer/master/screenshot.png" alt="Git logo" title="Git logo" style="max-width:100%;"><br>
CLI to deploy project for development
</p>


## Roles

| Name | Condition | Tasks |
| --- | --- | --- |
| git | none | - clone repository |
| analyzer | none | - composer.json file<br>- laravel in composer.json<br>- lumen in composer.json<br>- index file / public folder<br>- sql files<br>- migration files<br>- seeds files<br>- package.json file<br>- set facts |
| php | ``composer.json`` exists | - install package<br>- mysql driver<br>- install curl<br>- install mcrypt<br>- enable mcrypt |
| composer |`` composer.json`` exists | - check version<br>- install package<br>- make executable<br>- install dependencies |
| laravel | ``composer.json`` contains ``"laravel/framework":`` | - create .env<br>- edit .env<br>- set key<br>- make writable |
| lumen | ``composer.json`` contains ``"laravel/lumen-framework":`` | - create .env<br>- edit .env<br>- generate key<br>- save key<br>- make writable |
| apache | ``index.php`` exists<br>or ``index.html`` exists<br>or ``public/index.php`` exists<br>or ``public/index.html`` exists | - install package<br>- clear default<br>- set servername<br>- enable rewrite<br>- add hostname<br>- create virtualhost<br>- enable virtualhost<br>- restart service |
| mysql | ``*.sql`` exist<br>or ``database/migrations`` contains more than 2 ``*.php``<br>or ``database/seeds`` contains more than 1 ``*.php`` | - install package<br>- start service |
| phpmyadmin | ``*.sql`` exist<br>or ``database/migrations`` contains more than 2 ``*.php``<br>or ``database/seeds`` contains more than 1 ``*.php`` | - apache role (with phpmyadmin parameters)<br>- install<br>- configure |
| nodejs | ``package.json`` exists | - add key<br>- add repository<br>- install package<br>- install dependencies |


## Usage

1. Install ansible :

```Shell

sudo apt-add-repository ppa:ansible/ansible -y
sudo apt-get update
sudo apt-get install software-properties-common ansible git python-apt -y

```

2. Allow sudo without password for ansible :

```Shell

echo "%sudo ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/ansible
sudo chown root:root /etc/sudoers.d/ansible
sudo chmod 0440 /etc/sudoers.d/ansible

```

3. Deploy project :

```Shell

# Template :
ansible-pull -U https://github.com/simondubois/project-installer.git -e "git_repository=GIT_URL git_destination=CLONE_PATH"

# Prevent project-installer to be cloned to ~/.ansible/pull/ (facultative) :
ansible-pull -U https://github.com/simondubois/project-installer.git -e "git_repository=GIT_URL git_destination=CLONE_PATH" -d "TEMPORARY_PATH"

# Example :
ansible-pull -U https://github.com/simondubois/project-installer.git -e "git_repository=https://github.com/simondubois/budget.git git_destination=$HOME/dev/budget" -d "/tmp/project-installer"

```
