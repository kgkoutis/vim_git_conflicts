## Instructions for solving git conflicts in vim 

(Note: this is _not_ a complete overview of the issue, this is just an example)

Imagine that you want to merge the 'dev' branch to 'master'<br/>
Here 'dev' is the **feature branch** and 'master' is the **target branch**, where then HEAD is <br/>

1. Install, if not already installed, the **fugitive.vim** plugin (https://github.com/tpope/vim-fugitive) with any plugin manager <br/>
   -- like, e.g. vim-addon-manager (https://github.com/MarcWeber/vim-addon-manager)

2. Execute on master:
```bash
git merge dev
```

(As expected, conflicts arise)

3. Execute:
```bash
vim t
:Gvdiffsplit!
```

By the first command you should see the conflicts marked as 
```bash
<<<<<<< HEAD
(stuff)
===========
(other stuff)
>>>>>>> dev
```

The second command gives you a 3-window split. <br/>
In the **middle** window sits _always_ the conflicted file <br/>
In the **left** window sits _always_ the file in **target branch** <br/>
In the **right** window sits _always_ the file in **feature branch** <br/>

4. Execute:
```bash
:ls
```

This shows you 3 buffers open which:
+ the first one is always marked as the name of the file and it refers _always_ to the confilcted file in the middle
+ the second one has a '**//2**' inside its name and it refers _always_ to the file of the **target branch**
+ the third one has a '**//3**' inside its name and it refers _always_ to the file of the **feature branch**

5. Placing the cursor in the block of text you want to preserve you execute either:
```bash
:diffget //2 # target branch, here 'master'
```
or
```bash
:diffget //3 # feature branch, here 'dev'
```
to keep the block of text you would like to keep.<br/>
You can also introduce new changes in the middle file as you wish<br/>
If needed you can also select a range of lines from either the left or the right buffer, for example:

```bash
:1,5diffget //2
:1diffget //3
```
