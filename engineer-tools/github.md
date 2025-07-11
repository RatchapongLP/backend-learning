# GitHub setup (for macOS)

## git CLI
I only installed brew and updated it on macOS Sequoia 15.5. Not sure how git CLI was made available.
```
% brew update // This is done definitely.
% brew install git // I don't remember doing this.
% git -v
git version 2.39.5 (Apple Git-154)
```

## GitHub config
It might be not required as I did this before step 1 but did not work until steps 1-5 were done.
I also did not check if both the config parameters were already set but went ahead and set them.
You can try unsetting them and see how it goes.
```
$ git config --global user.name "RatchapongLP"
$ git config --global user.email "rat...@gmail.com"
$ git config -l
```

## Personal access token
1. Login to your github account on web browser.
2. Goto settings --> developers setting --> personal access tokens --> 
Generate new token (classic) for general use --> save the token somewhere safe.
3. Open the Keychain Access application on Mac.
4. Create an Internet password item by clicking `Create a new Keychain item`. 
Type in the URL `https://github.com/RatchapongLP`, paste the PAT from step 2 and save.
5. In a github repo local directory, try `git push origin`, a prompt should be launched.
Just enter the macOS account password. Click always allow. That's all done.

