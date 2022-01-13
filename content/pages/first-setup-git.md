+++
title = "First time Git setup"
slug = "first-setup-git"
type = "ros-tutorial"
+++

## Git SCM installation
### Brief Introduction

Git is a powerful distributed version control (DVC) software used for tracking development workflow of a project. It provides a full-fledged tracking history and Git is generally easy to use. As [the ReactOS project infrastructure](https://github.com/reactos/reactos) relies on Git for software development and patch contributions, this tutorial aims primarly on how to install Git SCM and do a basic user configuration.

**NOTE**: Git SCM is a Git utility that uses CLI (command line interface) as the primary UI for Git interactions. This tutorial doesn't take into account GUI equivalents for Git such as TortoiseGit!

### Obtaining the Git SCM installer

Opening the [Git SCM home page](https://git-scm.com) you'll be greeted with this (the image is clickable). Proceed with downloading the Git SCM installer.

[![Git website](../images/first-setup-git/git-site.png)](../images/first-setup-git/git-site.png)

### Installing Git SCM

Once the downloading has finished, you'll be greeted with this installer window. Proceed with specifying a directory where Git SCM should be installed (or C:\\Program Files as default).

[![Git Welcome](../images/first-setup-git/git-welcome.png)](../images/first-setup-git/git-welcome.png)

Once you're done you have to specify which options to be chosen for the Git installation process. You can either choose the ones you wish or choose the following options that I personally use.

[![Git Options](../images/first-setup-git/git-component.png)](../images/first-setup-git/git-component.png)

Git will ask you for a text editor to be used by default when Git attempts to launch the chosen editor to, for example, submitting a commit message description or doing an interactive rebase. I personally use Notepad++ as the default text editor for Git but you can choose whatever you want.

[![Git Editors](../images/first-setup-git/git-editor.png)](../images/first-setup-git/git-editor.png)

Git gives you the ability to use it across different tools such as the Windows command prompt, from dedicated Git Bash (which is provided by the installer) or by using a 3rd party software. Such options might modify your PATH environment variable. I personally choose using Git from Bash only.

[![Git PATH](../images/first-setup-git/git-use.png)](../images/first-setup-git/git-use.png)

Afterwards Git installer asks you which secure extension to be used for Git. By default you can choose OpenSSH.

[![Git SSH](../images/first-setup-git/git-ssh.png)](../images/first-setup-git/git-ssh.png)

Furthermore Git will ask for certificates to be used during HTTPS connections. You can choose the native Windows certificates store but I personally use OpenSLL for that.

[![Git OpenSSL](../images/first-setup-git/git-openssl.png)](../images/first-setup-git/git-openssl.png)

Now here comes the line endings. Windows uses CRLF (carriage return -- line feed) whereas \*nix-like systems such as Linux use LF (line feed) only. Understanding the difference is important as confusing the two character encodings may end up breaking the endings when checking out files or committing changes. It's recommended that you use the first option when concerning with ReactOS development.

[![Git Endings](../images/first-setup-git/git-endings.png)](../images/first-setup-git/git-endings.png)

Finally, Git prompts you for extra features. It's up to you if you want them or not. After that Git SCM will be installed although enabling file system caching is a neat feature.

[![Git Extra](../images/first-setup-git/git-extra.png)](../images/first-setup-git/git-extra.png)

Once everything is set, the Git installer should finish. You now have Git SCM installed!

[![Git Finish](../images/first-setup-git/git-install-finish.png)](../images/first-setup-git/git-install-finish.png)

## Git configuration file

Git SCM depends upon a configuration file, **.gitconfig**, to read the user configuration settings as well changing them for instance the real name of the committer, E-mail address, the personal GPG key for committing or editing the default text editor. Git comes with `git config` command line that allows you to edit the said configuration file. Click the right mouse button and you'll see two menu Git context items, **Git GUI** and **Git Bash**. Click on Git Bash. The Bash terminal appears like this.

[![Git Bash](../images/first-setup-git/git-bash.png)](/images/first-setup-git/git-bash.png)

### Setting your user name & E-mail address

Applying your name and mail is very easy to do. `git config` accepts a parameter, setting-attribute, which alters the behaviour or the looks of Git depending on the purpose of the setting you change. In our case...

`git config --global user.name "YOUR_NAME_HERE"`  
`git config --global user.email YOUR_MAIL_HERE`

Besides the setting-attribute `git config` accepts a flag, `--global`, which tells the command line to to assign the preferred setting data globally, that is, available across different project repositories you contribute.

### Setting your text editor

By default a text editor is already chosen (depending on what you have selected) during the setup installation process but you can manually change it whenever you want.

`git config --global core.editor "PATH_TO_EDITOR"`

### List the configuration file

`git config --list` displays a list of saved attribute settings of your configuration file. The list is shown like follows.

[![Git Config](../images/first-setup-git/git-config.png)](/images/first-setup-git/git-config.png)