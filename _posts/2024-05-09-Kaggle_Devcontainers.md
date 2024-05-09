# Getting Kaggle Working with Devcontainers

I previously had issues with working with Kaggle on my local device, especially while using devcontainers, but found a way to fix this. Hopefully this little tutorial could help you too. I am running devcontainers on vscode with [DockerDesktop](https://www.docker.com/products/docker-desktop/) on Windows Subsystem for Linux.

## 1. Generate Kaggle API Token
If you don't have a Kaggle account, just go to [kaggle](https://www.kaggle.com/) and create one with the register button and follow the necessary steps
![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/cd06747f-b045-43e3-bff1-386578de81f5)


Otherwise just sign in and navigate to your profile settings
![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/74c1d65f-c0e2-4d78-9942-24230b043762)

And click 'Create New Token' in the API settings
![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/24abd800-fd02-4670-be63-2817185560fb)

This will generate a key for you and download a _**kaggle.json**_ file. If you've already done this, it will deactivate any old keys and you'll have to change the key manually for whatever devices this affects.

## 2. Copy Contents of _**kaggle.json**_
This can easily be done opening it with VSCode. It should only have one line with your kaggle username and new key.
![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/d9f122f1-fe26-45cd-bcad-6b48eb9e411c)

Now, typically you just copy it into the directory said in the kaggle error message 'Can't find kaggle.json file' (for my windows device this is C:/Users/_my_username_/.kaggle/kaggle.json), but with devcontainers on WSL the location is a little harder to access.

## 3. Paste Contents to Correct Directory
Open a bash terminal in vscode and run the following commands. This will navigate to the .kaggle directory and run a text editor for a newly created kaggle.json file

```bash
cd ~/.kaggle/
vim kaggle.json
```

Now type `i` to add text to file.

Paste contents of your kaggle.json.

Press `Esc` to exit the insert mode.

Type `:wq` to exit vim
```bash
:wq
```
And that's it! Now Kaggle can run freely with your API on your local machine's devcontainers
