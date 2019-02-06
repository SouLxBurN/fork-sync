# Fork Sync
This is a small bash script I have written for syncing multiple modules that share dependancies and branch names.

# Setup
* Modify the `projects` file in the project.
  * Create a new line for each repository on your system you wish to sync.
  * __Path must be absolute:__ `/path/from/root/to/project/`
  * Lines starting with # are ignored in the projects file.
* You probably need to give syncb executable privledges.
  * `sudo chmod +x syncb`
* Create an alias and environment variable your shell's configuration file i.e. `.bashrc` or `.zshrc`
  * Example: `export SYNCB_HOME=~/projects/fork-sync/`
  * Example: `alias syncb="~/projects/fork-sync/syncb"`
  * __You can skip this part and run the script directly if you want.__
* Thats all you need!

# Prerequisuites
* You have to have git CLI installed. (duh)
* This script assumes `upstream` is set to the original remote respository. (The repo you forked)
* This script assumes `origin` is set to the remote fork respository. (Your remote fork)

# Execution
```bash
> syncb {branchName}
```

# How it works
The script will iterate over each project listed in the __`projects`__ file.
1. Stash any current changes.
2. Fetch from __origin__ and __upstream__.
3. Checkout the specified branch from __origin__, if it doesn't exist, __upstream__
   * If its unable to checkout, script will stop for that project, pop stash, and move on.
4. Pull any changes from the __upstream__ repository.
5. Push any new changes from __upstream__ to __origin__.
6. Pop the stash, leaving your uncommitted changes back the way they were! (Unless they conflict with new changes).
