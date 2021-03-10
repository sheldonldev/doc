# Install and Set Up Git

* Install [Git](https://github.com/sheldonldev/doc/tree/804ec9140919cf641e377a1b87f2428db52597e9/working-env/git-and-github/https/git-scm.com);
* Sign up for a [GitHub](https://github.com) account if you haven't got one;
* Associate your `Git` and `GitHub`:

```bash
# user settings
git config --global user.name <username>
git config --global user.email <email@domain.com>


# generate a new key
ssh-keygen -t rsa -C your_email@domain.com
# Press 'Enter' to save to default path
# Set Key: invisible when input.
# If don't input anything, the key is left empty
# Confirm Key.

cat ~/.ssh/id_rsa.pub
# show existing SSH key, copy to Github SSH Key


# DANGER: If you messed up, and want to remove the key
rm ~/.ssh/id_rsa.pub
```

