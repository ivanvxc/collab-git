# Workshop - Lab 01

In this lab exercise you are going to be working with a local git repository, creating it from scratch and performing some of the most common actions.

> Note: in this case "local" repository means that it is not synchronized yet with any other remote location. Your lab work takes place on a machine in the cloud, but the repository is "local" to it.

## Task 1

This task creates a repository from scratch and adds some files to it.

### Step 1

Open an SSH session to the lab machine. Its login details are provided by the instructor on the day of the workshop.

### Step 2

In the `/home/ntc` folder, create a new `labs` folder and change into it.

```
ntc training ~ $ mkdir -p /home/ntc/labs
ntc training ~ $ cd /home/ntc/labs/
ntc training ~/labs $
```

### Step 3

You are now going to create a new git repository (called `vlan-config`) to track an ansible playbook and some other files.

```
ntc training ~/labs $ git init vlan-config
Initialized empty Git repository in /home/ntc/labs/vlan-config/.git/
ntc training ~/labs $ cd vlan-config/
ntc training ~/labs/vlan-config (master #) $
```

### Step 4

Take a look at the content of the `vlan-config` folder. It's empty with the exception of the `.git` folder that holds all the information git is working with.

```
ntc training ~/labs/vlan-config (master #) $ ls -al
total 12
drwxrwxr-x 3 ntc ntc 4096 Nov 30 10:33 .
drwxrwxr-x 3 ntc ntc 4096 Nov 30 10:33 ..
drwxrwxr-x 7 ntc ntc 4096 Nov 30 10:34 .git

ntc training ~/labs/vlan-config (master #) $ tree -a
.
└── .git
    ├── HEAD
    ├── branches
    ├── config
    ├── description
    ├── hooks
    │   ├── applypatch-msg.sample
    │   ├── commit-msg.sample
    │   ├── fsmonitor-watchman.sample
    │   ├── post-update.sample
    │   ├── pre-applypatch.sample
    │   ├── pre-commit.sample
    │   ├── pre-merge-commit.sample
    │   ├── pre-push.sample
    │   ├── pre-rebase.sample
    │   ├── pre-receive.sample
    │   ├── prepare-commit-msg.sample
    │   └── update.sample
    ├── info
    │   └── exclude
    ├── objects
    │   ├── info
    │   └── pack
    └── refs
        ├── heads
        └── tags

10 directories, 16 files
ntc training ~/labs/vlan-config (master #) $
```

> Note: `ls` and `tree` do not show by default hidden folders (the ones with names starting with a dot) which is why you need to provide the `-a` parameter to them.

### Step 5

Create a new file named `inventory` with the following contents in the repository (`/home/ntc/labs/vlan-config`) using your editor of choice.

```
nyc-router-[01:05]
```

```
ntc training ~/labs/vlan-config (master #%) $ cat inventory
nyc-router-[01:05]
ntc training ~/labs/vlan-config (master #%) $
```

### Step 6

Check the git status of the working directory. Observe how git has noticed the existence of a new file which is not yet part of the repository - i.e. it is **untracked**.

```
ntc training ~/labs/vlan-config (master #%) $ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        inventory

nothing added to commit but untracked files present (use "git add" to track)
```

> Note: The custom git prompt includes a `%` sign now, showing we have untracked files in the working directory.

### Step 7

Add this file to the repository by staging it. This marks it for inclusion in the next git commit.

```
ntc training ~/labs/vlan-config (master #%) $ git add inventory
ntc training ~/labs/vlan-config (master +) $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   inventory
```

> Note: The custom git prompt now has a `+` sign, showing we have staged files in the working directory.

### Step 8

Create a new commit to store the `inventory` file permanently in the repository. You should get an error as shown below.

```
ntc training ~/labs/vlan-config (master +) $ git commit -m "add inventory file"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'ntc@training.(none)')
```

This situation is very likely to happen the first time you set up git on a machine, be it your own laptop or a VM in the cloud. There is no pre-existing git configuration and git does not know who you are.

### Step 9

While you may configure your name and email on a per-repository basis only, it is easier to store this information in the git global configuration file, namely the one stored in your home folder (e.g. `/home/ntc/.gitconfig`).

`!!!` Replace "Alice" in the commands below with your own name and email! This email address could be anything, but it is good practice to use a real email when collaborating with other people so they know how to contact you. `!!!`

```
ntc training ~/labs/vlan-config (master +) $ git config --global user.email "alice@example.com"
ntc training ~/labs/vlan-config (master +) $ git config --global user.name "Alice Smith"

ntc training ~/labs/vlan-config (master +) $ cat ~/.gitconfig
[user]
        email = alice@example.com
        name = Alice
ntc training ~/labs/vlan-config (master +) $
```

### Step 10

Compare the local git config to the global one. Note that if you don't specify which, then you get the computed config from both local and global settings.

```
ntc training ~/labs/vlan-config (master +) $ git config --list --local
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true

ntc training ~/labs/vlan-config (master +) $ git config --list --global
user.email=alice@example.com
user.name=Alice

ntc training ~/labs/vlan-config (master +) $ git config --list
user.email=alice@example.com
user.name=Alice
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```

### Step 11

Perform the commit.

```
ntc training ~/labs/vlan-config (master +) $ git commit -m "add inventory file"
[master (root-commit) b86984d] add inventory file
 1 file changed, 1 insertion(+)
 create mode 100644 inventory

ntc training ~/labs/vlan-config (master) $
```

> Note: the `+` sign is gone from the prompt as the staged files have been commited to the repository.

### Step 12

Check the git status and the git log.

```
ntc training ~/labs/vlan-config (master) $ git status
On branch master
nothing to commit, working tree clean

ntc training ~/labs/vlan-config (master) $ git log
commit b86984dee53c11b14a45d438316bf6ace85a9a94 (HEAD -> master)
Author: Alice <alice@example.com>
Date:   Mon Nov 30 12:32:30 2020 +0000

    add inventory file
```

## Task 2

You are now going to add more files to the repository, creating a working ansible playbook that generates vlan configuration files from a template.

Feel free to copy/paste the contents of the files from the lab guide!

### Step 1

In the `/home/ntc/labs/vlan-config` repository, create a new file named `pb_vlans.yml` with the following contents.

```yaml
---

- name: GENERATE IOS VLAN CONFIGURATION
  hosts: all
  tasks:
    - name: ENSURE OUTPUT FOLDER EXISTS
      file:
        path: output
        state: directory
    - name: USE VLAN TEMPLATE TO GENERATE FILES
      template:
        src: vlans.j2
        dest: output/{{ inventory_hostname }}_vlans.cfg
```

### Step 2

Stage the file in git and confirm the status.

```
ntc training ~/labs/vlan-config (master %) $ git add pb_vlans.yml
ntc training ~/labs/vlan-config (master +) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   pb_vlans.yml

ntc training ~/labs/vlan-config (master +) $
```

### Step 3

Create a new folder named `template` and in it, a file named `vlans.j2` with the following contents.

```
ntc training ~/labs/vlan-config (master +) $ mkdir template
ntc training ~/labs/vlan-config (master +%) $ cat template/vlans.j2
{% for vlan in vlans %}
vlan {{ vlan.id }}
 name {{ vlan.name }}
{% endfor %}
ntc training ~/labs/vlan-config (master +%) $
```

### Step 4

Check the git status. Git notices the existence of a new folder, but since it is not tracked, it doesn't check its contents any further.

```
ntc training ~/labs/vlan-config (master +%) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   pb_vlans.yml

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        template/

ntc training ~/labs/vlan-config (master +%) $
```

### Step 5

Stage the new template file, then check the status and folder structure.

```
ntc training ~/labs/vlan-config (master +%) $ git add template/vlans.j2

ntc training ~/labs/vlan-config (master +) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   pb_vlans.yml
        new file:   template/vlans.j2

ntc training ~/labs/vlan-config (master +) $ tree
.
├── inventory
├── pb_vlans.yml
└── template
    └── vlans.j2

1 directory, 3 files
```

> Note: when you add a file, git automatically also tracks its parent folder (in this case `template`).

### Step 6

You realize you forgot to **disable facts gathering** and set the **connection to local** in the ansible playbook, so you quickly fix it by editing `pb_vlans.yml` and adding in those lines.

Edit and save the file - it should now look as follows:

```yaml
---

- name: GENERATE IOS VLAN CONFIGURATION
  hosts: all
  gather_facts: false
  connection: local
  tasks:
    - name: ENSURE OUTPUT FOLDER EXISTS
      file:
        path: output
        state: directory
    - name: USE VLAN TEMPLATE TO GENERATE FILES
      template:
        src: vlans.j2
        dest: output/{{ inventory_hostname }}_vlans.cfg
```

### Step 7

Check the git status - you have made changes since the file was originally staged, so you can view them.

```
ntc training ~/labs/vlan-config (master *+) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   pb_vlans.yml
        new file:   template/vlans.j2

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   pb_vlans.yml

ntc training ~/labs/vlan-config (master *+) $ git diff pb_vlans.yml
diff --git a/pb_vlans.yml b/pb_vlans.yml
index 654e85d..61ffb2f 100644
--- a/pb_vlans.yml
+++ b/pb_vlans.yml
@@ -2,6 +2,8 @@

 - name: GENERATE IOS VLAN CONFIGURATION
   hosts: all
+  gather_facts: false
+  connection: local
   tasks:
     - name: ENSURE OUTPUT FOLDER EXISTS
       file:
```

As you can see, the two lines are shown as the difference between the working directory and the staged file.

### Step 8

To stage the new changes, add the file again.

```
ntc training ~/labs/vlan-config (master *+) $ git add pb_vlans.yml
ntc training ~/labs/vlan-config (master +) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   pb_vlans.yml
        new file:   template/vlans.j2
```

### Step 9

Create a new commit with these two files and check the log.

```
ntc training ~/labs/vlan-config (master +) $ git commit -m "add playbook and template"
[master d89f061] add playbook and template
 2 files changed, 19 insertions(+)
 create mode 100644 pb_vlans.yml
 create mode 100644 template/vlans.j2

ntc training ~/labs/vlan-config (master) $ git log
commit d89f061822c02865c05642775dbb78e1dc656e2d (HEAD -> master)
Author: Alice <alice@example.com>
Date:   Mon Nov 30 12:38:29 2020 +0000

    add playbook and template

commit b86984dee53c11b14a45d438316bf6ace85a9a94
Author: Alice <alice@example.com>
Date:   Mon Nov 30 12:32:30 2020 +0000

    add inventory file
```

### Step 10

In order for the playbook to actually run, you need some more data, namely the vlans to feed into the template.

Create a `group_vars` folder and in it the file `all.yml` with the contents shown below.

```
ntc training ~/labs/vlan-config (master) $ mkdir group_vars
ntc training ~/labs/vlan-config (master) $ cat group_vars/all.yml
vlans:
  - id: 10
    name: STORAGE
  - id: 20
    name: SERVERS
  - id: 30
    name: USERS

ntc training ~/labs/vlan-config (master %) $ tree
.
├── group_vars
│   └── all.yml
├── inventory
├── pb_vlans.yml
└── template
    └── vlans.j2

2 directories, 4 files
```

### Step 11

Stage the `group_vars` folder. If you add a whole folder, then git will stage **all** the files and subfolders!

```
ntc training ~/labs/vlan-config (master %) $ git add group_vars/
ntc training ~/labs/vlan-config (master +) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   group_vars/all.yml
```

### Step 12

Upon inspecting the folder structure one last time, you notice there's a typo! The `templates` folder is missing an `s` and ansible won't find the `vlans.j2` when it runs.

```
ntc training ~/labs/vlan-config (master +) $ tree
.
├── group_vars
│   └── all.yml
├── inventory
├── output
├── pb_vlans.yml
└── template
    └── vlans.j2

3 directories, 4 files
```

### Step 13

Fix the typo by renaming the folder. Since the folder is tracked by git already, use the `git mv` command to rename it. This performs two actions for you: it renames the folder and stages the changes.

```
ntc training ~/labs/vlan-config (master +) $ git mv template templates

ntc training ~/labs/vlan-config (master +) $ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   group_vars/all.yml
        renamed:    template/vlans.j2 -> templates/vlans.j2
```

### Step 14

Commit the changes.

```
ntc training ~/labs/vlan-config (master +) $ git commit -m "fix templates path and add vlan data"
[master 90a03ce] fix templates path and add vlan data
 2 files changed, 7 insertions(+)
 create mode 100644 group_vars/all.yml
 rename {template => templates}/vlans.j2 (100%)
```

## Task 3

Run the ansible playbook and see what you can do about the files it creates.

### Step 1

The ansible playbook is ready be executed. Run the following command and confirm that the configuration files have been generated appropriately.

```
ntc training ~/labs/vlan-config (master) $ ansible-playbook -i inventory pb_vlans.yml

PLAY [GENERATE IOS VLAN CONFIGURATION] **************************************************************

TASK [ENSURE OUTPUT FOLDER EXISTS] ******************************************************************
changed: [nyc-router-05]
ok: [nyc-router-03]
ok: [nyc-router-02]
ok: [nyc-router-04]
ok: [nyc-router-01]

TASK [USE VLAN TEMPLATE TO GENERATE FILES] **********************************************************
changed: [nyc-router-01]
changed: [nyc-router-03]
changed: [nyc-router-05]
changed: [nyc-router-04]
changed: [nyc-router-02]

PLAY RECAP ******************************************************************************************
nyc-router-01              : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
nyc-router-02              : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
nyc-router-03              : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
nyc-router-04              : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
nyc-router-05              : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ntc training ~/labs/vlan-config (master %) $ tree
.
├── group_vars
│   └── all.yml
├── inventory
├── output
│   ├── nyc-router-01_vlans.cfg
│   ├── nyc-router-02_vlans.cfg
│   ├── nyc-router-03_vlans.cfg
│   ├── nyc-router-04_vlans.cfg
│   └── nyc-router-05_vlans.cfg
├── pb_vlans.yml
└── templates
    └── vlans.j2

3 directories, 9 files
```

### Step 2

Check the git status. Notice how the new output folder is now marked as untracked.

```
ntc training ~/labs/vlan-config (master %) $ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        output/

nothing added to commit but untracked files present (use "git add" to track)
```

### Step 3

Since you don't want to store output configuration files in the git repository, you decide to make git ignore this path.

Edit the file `.gitignore` in the root of the repository (`/home/ntc/labs/vlan-config`) with the following contents.

```
ntc training ~/labs/vlan-config (master %) $ cat .gitignore
output
ntc training ~/labs/vlan-config (master %) $ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

Notice how the `output` folder is not in the untracked list anymore. Since you created the `.gitignore` file, it will show up as one would expect.

> Note: there are many ways to specify paths that git should ignore, in this case you are telling it to ignore any file/folder named `output` together with their contents.

### Step 4

Stage and commit the new git ignore file.

```
ntc training ~/labs/vlan-config (master %) $ git add .gitignore
ntc training ~/labs/vlan-config (master +) $ git commit -m "add output to gitignore"
[master ee8d02b] add output to gitignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
ntc training ~/labs/vlan-config (master) $
```

### Step 5

Notice how the git status shows nothing untracked or modified in the working directory even though the output folder and the configuration files are still there.

```
ntc training ~/labs/vlan-config (master) $ git status
On branch master
nothing to commit, working tree clean

ntc training ~/labs/vlan-config (master) $ tree
.
├── group_vars
│   └── all.yml
├── inventory
├── output
│   ├── nyc-router-01_vlans.cfg
│   ├── nyc-router-02_vlans.cfg
│   ├── nyc-router-03_vlans.cfg
│   ├── nyc-router-04_vlans.cfg
│   └── nyc-router-05_vlans.cfg
├── pb_vlans.yml
└── templates
    └── vlans.j2

3 directories, 9 files
```

### Step 6

Edit the `inventory` file, adding one new line with some new devices.

```
ntc training ~/labs/vlan-config (master *) $ cat inventory
nyc-router-[01:05]
dub-router-[01:05]

ntc training ~/labs/vlan-config (master *) $ git diff
diff --git a/inventory b/inventory
index 60aefb4..3e18a93 100644
--- a/inventory
+++ b/inventory
@@ -1 +1,2 @@
 nyc-router-[01:05]
+dub-router-[01:05]
```

### Step 7

Run ansible again so it generates the configuration files for the newly added devices.

```
ntc training ~/labs/vlan-config (master *) $ ansible-playbook -i inventory pb_vlans.yml

<OUTPUT SNIPPED>

ntc training ~/labs/vlan-config (master *) $ tree
.
├── group_vars
│   └── all.yml
├── inventory
├── output
│   ├── dub-router-01_vlans.cfg
│   ├── dub-router-02_vlans.cfg
│   ├── dub-router-03_vlans.cfg
│   ├── dub-router-04_vlans.cfg
│   ├── dub-router-05_vlans.cfg
│   ├── nyc-router-01_vlans.cfg
│   ├── nyc-router-02_vlans.cfg
│   ├── nyc-router-03_vlans.cfg
│   ├── nyc-router-04_vlans.cfg
│   └── nyc-router-05_vlans.cfg
├── pb_vlans.yml
└── templates
    └── vlans.j2

3 directories, 14 files
```

### Step 8

Check the git status. Notice how the new generated files in the `output` folder are also ignored and only the inventory modification is showing.

```
ntc training ~/labs/vlan-config (master *) $ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   inventory

no changes added to commit (use "git add" and/or "git commit -a")
```

### Step 9

Stage and commit the modified inventory.

```
ntc training ~/labs/vlan-config (master *) $ git add inventory

ntc training ~/labs/vlan-config (master +) $ git commit -m "add dublin routers to inventory"
[master 88d19c7] add dublin routers to inventory
 1 file changed, 1 insertion(+)

ntc training ~/labs/vlan-config (master) $ git status
On branch master
nothing to commit, working tree clean
```
