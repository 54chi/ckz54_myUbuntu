# Setting up Ubuntu for 54chi for Node, Python, Salesforce, Go and Blog

These are the essentials I need for a comfortable experience with Ubuntu with Salesforce B2B Commerce:

1. VERSION CONTROL: Git. But use gitlab if you want private repos that can be accessed outside the VPN!
2. CLI: SFDX
3. IDE: Visual Studio w/Forcecode and SF Extensions
4. BROWSER: Firefox (primary) and Chrome (as a backup or for performance analysis)
5. SUPPORTING LANGUAGES: Node (with NVM), Python3 (with Jupyter notebook), Go (for Hugo), vue (js framework) and vuepress (for documentation)

## Git
1. Open a terminal window
2. Install regular *git*:
    ```shell
    $ sudo apt install git
    ```

## Python
1. Open a terminal window
2. Install *python3*:
    ```shell
    $ sudo apt-get update
    $ sudo apt-get install python3.6
    ```
3. Install *pip3*:
    ```shell
    $ sudo apt-get install python3-pip
    ```

## Java

1. Open a terminal window
2. Install *Java 8*
   ```shell
   sudo apt install openjdk-8-jre-headless
   ```

## Node and SFDX cli

1. Open a terminal window
2. Install *NPM*
   ```shell
   $ sudo apt-get install npm
   ```
3. Since sfdx-cli doesn’t seem to work with node v8, let’s also install *curl* and *NVM* while at it (https://gist.github.com/d2s/372b5943bce17b964a79):
    ```shell
    $ sudo apt-get install curl
    $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
    $ source ~/.bashrc
    $ nvm install v10
    ```
4. Then install *sfdx-cli*
    ```shell
    $ npm install --global sfdx-cli
    ```
5. We will also install *yarn*, as it is becoming the next npm:
    ```shell
    $ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    $ echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
    $ sudo apt-get update && sudo apt-get install --no-install-recommends yarn
    ```


## Firefox

1. Firefox comes with Ubuntu. I like to install a couple extensions to make it safer to browse around.
2. Open Firefox, install *NoScript *and *uBlock Origin *extensions to keep it lean and fast
   1. NoScript is the best way to prevent your page loading extra javascript stuff you don’t want to. 
   2. uBlock will block popups without selling your soul

## Chrome

1. Download and install Chrome (https://www.google.com/chrome/). You want the *.deb* file since we are in Ubuntu
2. Since Chrome won’t be my default browser (long live Firefox!) we don’t need any plugins (yet)

## VS Code

1. Download and Install VS Code (https://code.visualstudio.com (https://code.visualstudio.com/)). You want the *.deb *file since we are in Ubuntu
2. Over VS Code and install the *ForceCode* extension by John Aaron Nelson and the *Salesforce Extension Pack* by Salesforce (this will take a while). This will install:
    1.  ForceCode and 
    2. Salesforce Extension Pack, which installs
        1. Apex, 
        2. Apex Interactive Debugger, 
        3. Apex Replay Debugger, 
        4. Salesforce CLI Integration, 
        5. Aura Components, 
        6. Visualforce, 
        7. Lightning Web Components and 
        8. Python (???!!)
3. In VS Code, disable the telemetry stuff unless you are ok of getting spied. 
    ```
    File > Preferences > Settings
    Type "telemetry"
    Disable both the Crash Reporter and Telemetry options
    ```
4. Restart VS Code

## Jupyter

1. Open a terminal window
2. Install Jupyter notebook
    ```shell
    $ sudo -H pip3 install --upgrade pip
    $ sudo -H pip3 install virtualenv
    ```
3. References: https://www.digitalocean.com/community/tutorials/how-to-set-up-jupyter-notebook-with-python-3-on-ubuntu-18-04

## Docker

1. Open a terminal window
2. Install docker
    ```shell
    $ sudo apt-get update
    $ sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    $ sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
    $ sudo apt update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```
3. References:
    1. https://docs.docker.com/install/linux/docker-ce/ubuntu/
    2. https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04

## Hugo

1. Open a terminal window
2. Install Hugo
    ```shell
    $ sudo apt-get install hugo
    ```
## Vuepress

1. Open your project
2. Install Vuepress
   ```shell
   $ yarn add -D vuepress@next
   ```
## Vue cli

1. Open a terminal window
2. Install vue clie
   ```shell
   $ yarn global add @vue/cli
   ```

------------------

## Shortcuts and tips

### Virtual Machine:

Everytime the computer goes to sleep, the network in the VM goes down.

Re-enabling the network after coming back from sleep:
- In the bottom status bar, click on the adapter icon (The 2 screens)
- Click on "Connect Network adapter" (to disable it)
- Click on "Connect Network adapter" again (to re-enable it)
  
### Linux:

- CTRL+Alt+T: Terminal window
- Windows key: Search 
- $ which xyz: tells you where a program lives
- If program xyz is not found in your PATH, follow these steps to add it and allow it to be run from anywhere. _Note: your profile may be in your .profile, .bash_profile, .bashrc, .zshrc, etc._
    - Add this to your profile: export PATH="$PATH:/path/xyz-[version]/bin" (the path may vary of course)
    - If in the terminal, log in and log out for the changes to take effect

### VSCode/ForceCode:

- CTRL+B:     Toggle the file explorer
- CTRL+`:     Terminal window (bash or wsl)
- Create *vs snippets* to make your life easier. Mine are here: https://github.com/54chi/ckz54_VSCodeSnippets

If you want to make VS a little lighter upon load, you can then disable the following plugins, as we won't typically use them (since we don't do active development). P.S. Don't delete them...you may need them sometimes!:

* Apex Interactive Debugger
* Apex Replay Debugger: super cool to debug and see the values at any give time!
* Aura Components
* Lightning Web Components: the future is lightning, but we are not living in the future!

### Jupyter:

https://www.dataquest.io/blog/jupyter-notebook-tutorial/

### Vuepress:

1. Create a sample doc
    ```
    # create a docs directory
    mkdir docs
    # create a markdown file
    echo '# Hello VuePress' > docs/README.md
    ```
2. Then add to package.json
    ```json
    {
        "scripts": {
            "docs:dev": "vuepress dev docs",
            "docs:build": "vuepress build docs"
        }
    }
    ```
3. To create docs in real time (by default, you will see the results in http://localhost:8080/):
   ```shell
   $ yarn docs:dev # OR npm run docs:dev
   ```
4. To generate docs (by default they will be created in docs/.vuepress/dist):
   ```shell
   $ yarn docs:build # Or npm run docs:build
    ```
