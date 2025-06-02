# SSH
This protocol allows you to connect/communicate safely to a remote machine. It is used to with your github repo and in order 
to be able to communicate with github to be able to interact with the repositories you are a collabotor of you need to set up
the configurations of this protocol and those are

1. Create SSH key, this generates a private and a public key, public key will be stored in your repo and private key will be
stored in your computer, this step could actually be separated into two steps.


2. There is something called the SSH agent, this agent has to know who you are interacting with, and for that, in the previous
step you should've already created an ".ssh" directory in your user's root directory and inside this you can either add the
github ssh key fingerprints from [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints)
or the first time you try to clone a repository you will be asked if you want to add the remote host fingerprints to your ssh configurations, if
you agree, an `known_hosts` file will be created. You can avoid adding the key to the ssh agent everytime you want to stablish connection
to the remote host by creating and configuring a `config` file as shown [here](https://dev.to/jajera/how-to-configure-github-authentication-using-ssh-certificates-3haj)
and [here](https://linuxize.com/post/using-the-ssh-config-file/)
