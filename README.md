# Add Datasets to nbteach JupyterHub

Datasets added to this repository are automatically synced to user accounts on the nbteach JupyterHub. Everytime a user logs in a script runs [nbgitpuller](https://github.com/jupyterhub/nbgitpuller) to sync the files in this repository to the user's `.data` directory.

You probably don't want to add too many large data sets to the repository. The sync doesn't download the files every time, but it does make sure it has the most recent version of the files added to it. If the repository grows to 1G that means every user will have 1G of files on their account. New users will have to wait for that full 1G to be downloaded to their account. In the future I can probably update this to have users access a central database, but it doesn't work that way for now.

The repository has to be public or the sync won't work. We might be able to work around this in the future. But for now, **only upload datasets that are okay to make public**. 

## Using the Data

The files in this repository are synced to the `.data` folder on every user account. The .`data` folder isn't visible on accounts, nor is it writeable (you can't add, delete, or modify anything in it), but it's readable. So you can access datasets like this:

```r
read.csv(".data/okcupid_profiles.csv")
```

However... **don't do this. When you publish notebooks the path won't work.** Keep reading...

The `.data` folder is in the user's home directory. The home directory is also where you are able to create new notebooks. When you publish a notebook, that notebook is placed in the user's `classwork` directory. Paths data do not start with a "/" are relative to the current directory. If you use the R code above, it will search for the dataset in a `.data` directory within the `classwork` directory (and this place doesn't exist).

To access the .data folder from anywhere, you need to use an absolute path. The absolute path to the `.data` directory is `/home/jovyan/.data`. To shorten this path, there is a special path character "~" which expands to the home directory (`/home/jovyan`). If you  use this character, you can construct an absolute path to `.data` directory from anywhere:

```r
read.csv("~/.data/okcupid_profiles.csv")
```
