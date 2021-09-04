# git-how-to

#### map git configs to multiple accounts on the same machine through containers (docker)

*OS used: MacOS, same steps can be used for linux.

#### Problem: 
What if there are multiple github accounts that need to be used for different projects.
Using the steps in this document might give you the feeling of using one computer for one git account.

#### Solution
A github account is assotiated with an email and with a SSH key.
Use a different directory in the host machine to store the SSH key and a different directory for git repo.
Use a ubuntu container to map the new SSH and git repo directories.

#### Prepare the Setup

#### Install docker (convenience scripts)
```bash
curl -fsSL https://test.docker.com -o test-docker.sh
```

```bash
#Install docker through convenience script
 curl -fsSL https://test.docker.com -o test-docker.sh
 sudo sh test-docker.sh curl -fsSL https://test.docker.com -o test-docker.sh
 sudo sh test-docker.sh
```

Typical SSH config is in the hidden .ssh under home directory (cd ~/.ssh):
Navigate in the the .ssh directory:
```bash
cd ~/.ssh
```

Typlical content of a .ssh directory
```bash
$ tree -a
.
├── config
├── id_rsa
├── id_rsa.pub
└── known_hosts
```

In the .ssh directory create another hidden directory. In this directory config for other accounts will be storred.
```bash
mkdir .ssh_other_accounts
```

Change directory to .ssh_other_accounts and create a directory for the new github/ssh account.
```bash
cd .ssh_other_account
```

Create the directory for the new account:
```bash
mkdir ermurachi_gmail_com
```

List the directory structure:
```bash
cd ermurachi_gmail_com
tree -a
```

```bash
$ tree -a
.
├── .ssh_other_accounts
│   └── ermurachi_gmail_com
├── config
├── id_rsa
├── id_rsa.pub
└── known_hosts
```

