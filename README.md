# git-how-to

### GIT map to container
*OS used: MacOS, same steps can be used for linux.*

### Problem: 
What if there are multiple github accounts that need to be used for different projects?

### Solution
A github account is assotiated with an email and with an SSH key to a container.
Use a different directory in the host machine to store the SSH key and a different directory for git repo.
Use a ubuntu container to map the new SSH and git repo directories.


---

### Prepare the Setup
Install docker [Link](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script):
```bash
curl -fsSL https://test.docker.com -o test-docker.sh
```

```bash
#Install docker through convenience script
 curl -fsSL https://test.docker.com -o test-docker.sh
 sudo sh test-docker.sh curl -fsSL https://test.docker.com -o test-docker.sh
 sudo sh test-docker.sh
```

Verify that docker was successfully installed:
```bash
docker -v
```

Typical SSH config is in the hidden .ssh under home directory (cd ~/.ssh).\
Navigate in the the .ssh directory:
```bash
cd ~/.ssh
```

Typical content of an .ssh directory
```bash
$ tree -a
.
├── config
├── id_rsa
├── id_rsa.pub
└── known_hosts
```

In the .ssh directory create another hidden directory.
```bash
mkdir .ssh_other_accounts
```

Change directory to .ssh_other_accounts and create a directory.
```bash
cd .ssh_other_account
```

Create a directory that will be used to store ssh-key assotiated with the new git account.
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

Generate a new SSH key.\
The string after -C is the email using for github account in this case (any string can be used instead of the email)
[how-to-Github-link](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key):
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
This will generate a private key and a public key:

* public key \.pub  \(id_ed25519.pub\) can be shared with public, anyone.
* private key (id_ed25519) is to be kept private, don't share
```bash
$ pwd & tree
/Users/ion/.ssh/.ssh_other_accounts/ermurachi_gmail_com
.
├── id_ed25519
└── id_ed25519.pub
```
