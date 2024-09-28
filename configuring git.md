initially adding whatever this is called 
~~~
git config --global user.name "username"
git config --global user.email "primary email"  
~~~

## Adding primary account via ssh 
generating a ssh keypair
~~~
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
~~~

starting the ssh agent
~~~
eval "$(ssh-agent -s)"
~~~

adding private key to ssh agent
~~~
ssh-add ~/.ssh/id_rsa
~~~

to add this to github account just copy the contents of .pub file and add it as a ssh key in github 

testdrive
~~~
ssh -T git@github.com
~~~

## Adding second account via ssh
generate another ssh keypair(change name to `id_rsa_second` when prompted)
~~~
ssh-keygen -t rsa -b 4096 -C "your_email_for_second_account@example.com"
~~~

adding private key to ssh agent
~~~
ssh-add ~/.ssh/id_rsa_second
~~~

to add this to github account just copy the contents of .pub file and add it as a ssh key in github 

## Configuring ssh for multiple users
edit or create a folder `.ssh/config`

add the following in it
~~~
# Primary account
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa

# Second account
Host github-second
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_second
~~~


## **Important note** for working with repos through second github account

when you clone a repo normally it goes like this 
`git clone git@github.com:AbbasYT/test-auth.git`

but for using second account you have to chanfge it to `github-second` like this
~~~
git clone github-second:AbbasYT/test-auth.git
~~~


you have to manually add this when you clone any repo so that it does not not use the primary email and name(which we added globally), just do this directly after cloning a repo with second account
~~~
git config user.name "username"
git config user.email "second email"
~~~



