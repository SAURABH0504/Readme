## What is Git?

Git is a free and open source version control system.
Git is a distributed application model whereas SVN is a centralized model. Distributed applications are generally more robust as they do not have a single point of failure like a centralized server.

## What is version control?

Version control means management of documents, computer programs, large websites, and other collections of information. We basically save file to the git and again when we make changes to the file we again add files to the git again and again. We can look at all the changes we have made over time.

## Is git centralized or decentralized?

Git is inherently neither decentralized nor distributed it is offline and just like a real life git, it doesn't care.

## Terms

Directory ->Folder

CLI -> Command Line Interface

cd -> change directory

Repository -> Project, or the folder/place where your project is kept.

Github -> A website to host your repository online.

## Git Commands

clone - Used to save the repository that is hosted somewhere to the local machine.
.._ add -> Track your files and changes in Git.
.._ commit -> Save your files in Git.
.._ push -> Upload Git commits to a remote repo, like Github
.._ pull -> Download changes from remote repo to your local machine, the opposite of push.

..\_ git status -> It shows all the file that are updated, created or deleted within the repository.

## Local & Remote

Local repository are the directory which are stored on your local machine and remote repository are the repository that are stored on some other system it can be a server or another system.

## init

Git init is the one way to start a new project. It created a new file into the repository which is .git file and it will track all the changes in the repository and store it in .git file.

## config

The git config command can accept arguments to specify which configuration level to operate on.
There are three types of configuration.

- -- local -> On this level the configuration is stored on the local level which is stored in the /.gitconfig file inside the local repository.

- -- global -> Global level configuration is user specific means it is applied to an operating system user. The global configuration is stored on user's home directory. ~ /.gitconfig or C:\Users\\.gitconfig on windows

- -- system -> System level configuration is applied across an entire machine. This covers all the users on an operating system and all repos.
  clone. The system configuration file lives in a gitconfig file in the root path. On windows it can be found at C:\ProgramData\Git\config

  git config --global user.email "your_email@example.com"

- color.ui -> It will disable all the colored terminal output
  git config --global color.ui false

## fetch

Git fetch command downloads commits, files, and refs from a remote repository into your local repo. Fetching is what you do when you want to see what everybody else has been working on. Git isolates fetched content from existing local content. it has absolutely no effect on your local development work.
The fetched contents has to be explicitly checked out using git checkout command.

### How git fetch works with remote branches

Git stores all commits of local and remote branch.

-     To Output local branch  --> git branch
-     To Output remote branch  --> git branch -r
  Git keeps local and remote branch commits seprate from each other.
  You can check out a remote branch just like a local one, but this puts you in a detached HEAD state (just like checking out an old commit). You can think of them as read-only branches.

You can inspect remote branch using git checkout and git log commands.If you approve the changes a remote branch contains, you can merge it into a local branch with a normal git merge.

-         $ git fetch < repository Url>
  To fetch a specific branch
-      $ git fetch <branch URL><branch name>
  To fetch all branch simultaneously
-       git fetch -all

## pull

Pull is a command which is used to save all the changes from the remote repository to the local repository. - git pull = git fetch + git merge -

-     $ git pull <option> [<repository URL><refspec>...]

-     $git pull --no-commit <remote>

  Similar to the default invocation, fetches the remote content but does not create a new merge commit.(A commit which has multiple parents)

-     git pull --verbose
  Gives verbal output during a pull which displays the content being downloaded and the merge details.

## push

The "git push" command is used to push into the repository. The push command can be considered as a tool to transfer commits between local and remote repositories. The basic syntax is given below:

-     git push < option > < Remote URL > < branch name >

## add

Before saving the file in the git we need to first tell git about the added files.

..\_ git add -> This command is used to track the file before it can be saved to the git. All the files with the git add command will be staged to git i.e it adds changes in the working directory to the staging area.

-      git add <file>
-      git add <directory>
-      git add -p
  Begin an interactive staging session that lets you choose portions of a file to add to the next commit. This will present you with a chunk of changes and prompt you for a command. Use y to stage the chunk, n to ignore the chunk, s to split it into smaller chunks, e to manually edit the chunk, and q to exit.

## commit

After tracking the file by the git using add command we can save file to git using git commit.

..\_ git commit -> It is used with -m for passing the message. A commit is the Git equivalent of a "save". The git commit command is used to Commit a snapshot of the staging directory to the repositories commit history.

</git commit -m "Your Message"/>

Git internal state management mechnaism consist of three trees. Trees are, however, node and pointer-based data structures that Git uses to track a timeline of edits.

### Git's three internal state management mechanism's, The Commit Tree (HEAD), The Staging Index, and The Working Directory.

## The Working directory

This tree is in sync with the local filesystem and is representative of immediate changes made to content in files and directories.
The changes in the file are part of the first tree and can be checked by using git status command which shows changes in the working directory.

## The Staging index

This tree is tracking working directory changes, that have been promoted with git add, to be stored in the next commit. This tree works on internal caching mechanism.

git ls-files -s -> This command shows hash of the files in the staging area. The Commit History stores its own object SHA's for identifying pointers to commits and refs and the Staging Index has its own object SHA's for tracking versions of files in the index.

#### To promote file to the staging index

git add <file-name>

It is important to note that git status is not a true representation of the Staging Index. The git status command output displays changes between the Commit History and the Staging Index.

## Commit History

The final tree is the Commit History. The git commit command adds changes to a permanent snapshot that lives in the Commit History. This snapshot also includes the state of the Staging Index at the time of commit. The changeset has been added to the Commit History. Invoking git status at this point shows that there are no pending changes to any of the trees. Executing git log will display the Commit History. Now that we have followed this changeset through the three trees we can begin to utilize git reset.

## Git checkout

Git checkout is an act of switching out between different versions of git. By default HEAD pointer points to the main branch or the cureent branch and previous commit.
Now if we want to revert back to the previous commit we need commit id

To get commit id ->

-     git log -oneline

Now to switch between commit we do

-     git checkout <commit_id>

This is not permanent and will not have any effect on the previous commit and changes here will not reflect in the current state. It is just used to checkout the previous commit.

## Git Reset

Git Reset is just like Git checkout but git reset, moves both the HEAD and branch refs to the specified commit.
In addition to upgrading the commit ref pointers, git reset will modift the state of all the three trees. The ref pointer modification always happens and is an update to the third tree, the Commit tree.

- --hard -> This is the most direct, DANGEROUS, and frequently used option. The Commit History ref pointers are updated to the specified commit. Then, the Staging Index and Working Directory are reset to match that of the specified commit. This means any pending work that was hanging out in the Staging Index and Working Directory will be lost.

- --mixed -> This is the default operating mode where ref pointers are updated. The staging index is updated by matching with the specified commit. The working directory remains unchanges.
- git reset --mixed <commit_id>
- --soft -> When the --soft argument is passed, the ref pointers are updated and the reset stops there.

## Git revert

The git revert command can be considered an 'undo' type command, however, it is not a traditional undo operation. Instead of removing the commit from the project history, it figures out how to invert the changes introduced by the commit and appends a new commit with the resulting inverse content. This prevents Git from losing history.

## Git rm

The rm command is used to remove files from the staging area.

- $git rm <file>

- $git rm -f <file>
  The -foption is used to override the safety check that Git makes to ensure that the files in HEAD match the current content in the staging index and working directory.
- $git rm -r <file>
  The -r option is shorthand for 'recursive'. When operating in recursive mode git rm will remove a target directory and all the contents of that directory.

## Git amend

The git commit --amend command is a convenient way to modify the most recent commit. It lets you combine staged changes with the previous commit instead of creating an entirely new commit.

Change most recent Git commit message

    git commit --amend -m "an updated commit message"

Changing committed files # Edit hello.py and main.py

    git add hello.py
    git commit # Realize you forgot to add the changes from main.py
    git add main.py
    git commit --amend --no-edit

## Git Rebase vs Git Merge

## Git diff

The git diff command shows the differences between the files in two commits or between your current repository and a previous commit. This command displays changes denotes by headers and metadata for the files that have changed.

    git diff HEAD ./path/to/file

By default git diff will execute the comparison against HEAD. Omitting HEAD in the example above git diff ./path/to/file

    git diff --cached ./path/to/file

- git diff head shows difference between staging index and local repository.
- git diff --cached shows difference between staging index and working repository.

## log

Git log is a utility tool to review and read a history of everything that happens to a repository. Generally, the git log is a record of commits. A git log contains the following data:

A commit hash, which is a 40 character checksum data generated by SHA (Secure Hash Algorithm) algorithm. It is a unique number.
Commit Author metadata: The information of authors such as author name and email.
Commit Date metadata: It's a date timestamp for the time of the commit.
Commit title/message: It is the overview of the commit given in the commit message.

## stash

git stash temporarily shelves (or stashes) changes we've made to our working copy so we can work on something else, and then come back and re-apply them later on.

To stash : git stash
To re-apply : git stash pop

### Who is author in git?

The author is the person who originally wrote the code. The committer, on the other hand, is assumed to be the person who committed the code on behalf of the original author
