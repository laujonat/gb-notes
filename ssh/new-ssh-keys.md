---
description: Generate New SSH Keys
---

# Adding SSH Keys

### SSH Keys

Follow these instructions to create or add SSH keys on Linux, MacOS & Windows. Windows users without OpenSSH [can install and use PuTTY](https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/create-with-putty/) instead.

#### Create a new key pair, if needed

Open a terminal and run the following command:

```text
ssh-keygen
```

CopyCopy

You will be prompted to save and name the key.  Generating public/private rsa key pair. Enter file in which to save the key \(/Users/USER/.ssh/id\_rsa\):

Next you will be asked to create and confirm a passphrase for the key \(highly recommended\):Enter passphrase \(empty for no passphrase\):  
Enter same passphrase again:

This will generate two files, by default called `id_rsa` and `id_rsa.pub`. Next, add this public key.

#### Add the public key

Copy and paste the contents of the **.pub** file, typically id\_rsa.pub, into the **SSH key content** field on the left.

```text
cat ~/.ssh/id_rsa.pub
```

For more detailed guidance, see [How to Add SSH Keys to Droplets](https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/)

