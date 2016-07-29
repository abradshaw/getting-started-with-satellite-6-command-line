# Base Install

Start with a fresh installation of RHEL 7.2, which was installed via PXE and kickstart with an FTP source. I prefer this, over templates or machines deployed by Satellite/Foreman as it keeps it as clean as possible and there is no existing puppet configuration, might have lead to problems later on.

Plus, my test Sat 6 has a 300GiB vda, not keeping 2 Satelites on the hypervisor.

When installing, be sure to just use "Base" as the installation type.

Although I do add the following for comfort
* acpid
* chrony
* kexec-tools

Once installed, we will register the machine to Red Hat, and fully update it. Then we will change its Satellite version, add some subscriptions and download its manifest file and get the Satellite software installed.

