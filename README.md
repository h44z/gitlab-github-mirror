Gitlab to Github mirroring
===

This repo is used for testing mirroring of a gitlab repo to github using gitlab-ci.
For gitlab ee, there already exists a mirroring service, so this is only useful for gitlab ce.

# Prerequisites
Setup gitlab-ci and create a shell runner. (https://docs.gitlab.com/runner/install/)

![Runner Configuration](https://raw.githubusercontent.com/h44z/atestproject/master/runner.png)

Next create or edit the file `/etc/ssh/ssh_known_hosts`:

```bash
# touch /etc/ssh/ssh_known_hosts
```

Allow the runner to modify the file (not needed if you do not update the ssh keys automatically):
```bash
# chown :gitlab-runner /etc/ssh/ssh_known_hosts
# chmod g+w /etc/ssh/ssh_known_hosts
```

You can prefill the known hosts file (you can also run this step in the gitlab runner):
```bash
# ssh-keyscan -t rsa,dsa,ecdsa github.com > /etc/ssh/ssh_known_hosts
```

Then create a new ssh key-pair for the gitlab runner (do not use a key password!):
```bash
# su gitlab-runner
$ cd
$ ssh-keygen -t rsa -b 4096
$ cat .ssh/id_rsa.pub
```

Add the key to your github account.

Now just edit the `.gitlab-ci.yml` file in your repo to fit your needs. Enjoy the gitlab to github mirroring :)

Warning/Hint: changes on github will be overwritten!!
