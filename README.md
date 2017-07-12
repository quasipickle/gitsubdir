# gitsubdir
A CLI PHP script for syncing only some directories of a GitHub repository.

Useful if you want to only download part of a GitHub project, like the `dist/` directory of [Bootstrap](https://github.com/twbs/bootstrap) for example.

Credit to https://github.com/mfbx9da4/git-sub-dir for the original idea.

## Usage

### Parameters

**-r [Required]** The repository from which to retrieve.  Ex: twbs/bootstrap

**-p** The subdirectory from which to retrieve. Ex: dist

**-b** The branch from which to retrieve. Ex: v4-dev

**-u [Recommended]** The user to authenticate as.  If just the username is provided, you will be prompted for a password.  The password can be also included in the username argument like so: *username:password*.

This parameter is recommended because the rate limit for unauthenticated access is 60, but 5000 for authenticated.

**-d**    The destination directory into which the files should be copied. If not provided, the directory will be the repository name.

**-s**    If set, retrieval will be shallow and only files 1 level deep will be retrieved.  Retrieval is recursive by default.

**-c**    If set, a sync file will be created in the destination directory.  This file can be used subsequently to sync again without needing to remember all the parameters.

**THE PASSWORD WILL NOT BE STORED.  You will be prompted for your password again.**

**--sync**    Use to sync a directory that has a git_sync file in it.  Mustspecify the directory in which to look.

### Example

    gitsubdir -r twbs/bootstrap -p dist -b v4-dev -u johnny5 -d boots -c

This will retrieve all the files and directories in the `dist` directory of the `v4-dev` branch of the `twbs/bootstrap` repository.  The files and directories will be created locally in the `boots` directory.  The command will be run after authenticating as the `johnny5` user.  After completing the retrieval, a `git_sync` file will be created in the `boots` directory.  From here on out, you
can call:

    gitsubdir --sync boots

And the files will be retrieved in the same manner they were initially.
