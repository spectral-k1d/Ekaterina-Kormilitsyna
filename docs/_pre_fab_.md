# _pre-fab _

In the first weeks of 2023 I have tried to prepare myself for the up and coming Fab-Course by doing some pre-fab work with Georg. This had come with some challenges and required quite a bit of trouble shooting but there has been some progress made!


!!! tip "The key focus of these weeks were:"

    - Design and make an MKdocs website and get it running on GitHub
    - Outline multiple possible Final Projects
    - Start playing with Aduino.


!!! tip "The achieved outcomes were:"

    - Mkdocs website and Material are running on Github, but Material require a lot of troubleshooting, and the design elements are still not working as desired, website look is not how I would like it.
    - Only one final project are currently outlined not 4.
    - still not feeling 100 percent at ease with mkdocs- and not loving the design outputs.
	- having done some playing with Arudino 

but lets go step by step!

# _ 00 - 1 _ setting up mkdocs

**Step 1:** I followed the mkdocs tutorial on their website to download mkdocs using Terminal.

!!! failure "first issues"

    I ran into some first issues because neither pip nor python commands were working, and had to first understand that my computer had pip3 installed, and so I had to adjust any code I found online or in tutorials to this.
    I also installed brew ! [ this turned out to be the cause of different problems down the line]
    Also I am still having trouble embedding imagages- so for today please be kind towards the fact that sofar I have no embeddded screenshots.


![Screenshot 2022-12-27 at 13.30.13.png](_%20Pre-FaB%20Documentation%20_%2093dae4815a244f09b0f0794cd733e9cb/Screenshot_2022-12-27_at_13.30.13.png)

After realising this I simply followed the mkdocs tutorial

I also changed the default shell to zsh

![Screenshot 2022-12-27 at 13.19.24.png](_%20Pre-FaB%20Documentation%20_%2093dae4815a244f09b0f0794cd733e9cb/Screenshot_2022-12-27_at_13.19.24.png)

```python
$ pip3 install mkdocs 
```

Step 2 install material: 

```python
$ pip3 install mkdocs-material
```

---

# _ 00- 2 _ Deploying to GitHub

Once I thought Mkdocs was working i went to attempt the steps to deploy the mkdocs documentation page to github. 

### **Step 1: Creating a new SSH Key**

I went to follow the github tutorial. To be found [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). 

1. Open Terminal.
Go to the `.ssh` directory.
    
    ```
    $ cd ~/.ssh
    ```
    
2. Paste the text below, substituting in your GitHub email address.
    
    ```
    $ ssh-keygen -t ed25519 -C "your_email@example.com"
    ```
    
    I also added a password.
    
3. At the prompt, type a secure passphrase. For more information, see ["Working with SSH key passphrases](https://docs.github.com/en/articles/working-with-ssh-key-passphrases)."
    
    ```
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```
    

### **Step 2: Adding SSH Key to ssh-agent.**

```
$ eval "$(ssh-agent -s)"
```

### **Step 3: Adding Key Info to *config***

First, check to see if your `~/.ssh/config` file exists in the default location.

```
$ open ~/.ssh/config
> The file /Users/ekatrinakormilitsyna/.ssh/config does not exist.
```

Since the file doesn’t exist, I had to make a new one.

```
$ touch ~/.ssh/config
```

Open `.ssh/config` 

```python
$ open config
```

Add the following:

```
Host *.github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

### **Step 4: Adding the Key to *ssh-agent***

Adding private key to ssh-agent

```
$ ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

This add the new key to the Apple Keychain.

### **Step 5: Adding Public Key to github.com**

- Log into Github
- Profile > Settings > SSH and GPG Keys
- Click 'New SSH Key'

Copy the SSH public key to your clipboard.

If your SSH public key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

```python
$ pbcopy < ~/.ssh/id_ed25519.pub
  # Copies the contents of the id_ed25519.pub file to your clipboard
```

### **Step 6: Testing the connection**

```
$ ssh -T git@github.com
Hi spectral-k1d! You've successfully authenticated,
but GitHub does not provide shell access.
```
!!! failure "OH NO"
    
    Attempting to run gh-deploy came up triggred a log in request github. my identity could not be verified.
	Solution: I had to generate a token on the github website and had to enter this into the 'Password' request field after i entered my GitHub username.
	This was able to verify my identity. Since then there was no further log-in request.

YAY Things seem to be working lets try to start the deploy to github!

```python
$ mkdocs gh-deploy
```
… … …
### OH NO!
!!! failure "OH NO"
    
    Attempting to run gh-deploy came up with an error message that mkdocs-material template could not be recognised!.

### SOLUTION

After nearly a week of trying to figure out why repeatedly all attempts to deploy to github were failing I finally figured out what was wrong.

The problem all along had been that originally when I was installing mkdocs I did it once using brew and once using pip3. 

Now the way that mkdocs works, is that it looks for templates in the same directories as where mkdocs was originally installed, and it was using to utilitize the brew install for mkdocs, while material was installed using pip3 so I had to first undo the original installs.

 

```python
$ pip3 uninstall mkdocs

$ pip3 uninstall mkdocs-material

$ brew uninstall mkdcos-material

$ brew uninstall mkdocs
```

Once this was successfully achieved. I could go back and install MKdocs and material again using only pip3

```python
$ pip3 install mkdocs

$ pip3 install mkdocs-material
```

After this finally everything worked as it was supposed to!

### HONESTY CORNER

So after all of this, the documentation site could finally run, but I still struggle with it. Most of the aesthetic ideas I have I am struggling to implement. I know there is a lot that I still have to figure out in the next couple of days, especially if I want the site to represent some of my ideas and design ideas that relate to the project. Even for today, I struggled a lot with doing simple customisation, and it’s still not working, even when I try to change the font etc. 

I have also a harder time proofreading using mkdocs work-flows considering my dyslexia.

Aesthetically I very much prefer the look of notion pages, however I am absolutely aware of how limiting they are in terms of creating an actual website.
So for today I have also put all of this documentation into Notion in an attempt to help myself stay organised. 
You can find this site here: [NOTION PAGE](https://www.notion.so/FABACADEMY-741870308d1f488c91cade1936452b1d)
