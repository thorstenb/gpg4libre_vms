## Vagrant VM builder scripts for gpg4libre test rigs

What this is for:

* we need reproducible, always-same test rigs for gpg4libre
* so test VMs check that box
* generating/maintaining those is a pain, so this needed scripting

What this does:

* pull 90-days Windows7 eval version from
  https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/
* pull standard Ubuntu 14.04 vagrant box
* stand up VirtualBoxes with gpg stuff and libreoffice readily
  installed

Fine print:

* so the win7 box do not have any remote deployment enabled out of the
  box, what you need to do locally is (since the win7-ie11 box cannot
  be redistributed):
  * `vagrant up` the box
  * do this manually, inside an admin-rights cmd.exe:
    `winrm quickconfig -q`
    `@powershell -NoProfile -ExecutionPolicy Bypass -Command "Set-Item WSMan:\localhost\Service\AllowUnencrypted -Value True; Set-Item WSMan:\localhost\Service\Auth\Basic -Value True"`
    `sc triggerinfo winrm start/networkon stop/networkoff`
  * export the box, and use it for the win7 setup:
    `vagrant package --output "yourboxname" --Vagrantfile Vagrantfile`
