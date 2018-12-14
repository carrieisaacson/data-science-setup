# Machine Setup

Description of my current machine setup optimized for data science projects.
My philosophy is to keep the default Python environment very sparse. When I start a new project I start a new environment, install the standard DS packages (e.g. numpy, pandas, scikit), use cookiecutter for a standard directory structure and start a new git repo (not necessarily in that order).

This documents my essential setup details, in case my current machine explodes or gets run over by a bus or something.

Eventually I'll explore using docker for some or all projects. 


# General

(Chrome)[https://www.google.com/chrome/]
(KeePassX)[https://www.keepassx.org/]
(Dropbox)[https://www.dropbox.com/install]

## Install Homebrew

The missing package manager for macOS. Installation instructions can be found on the [Homebrew homepage](https://brew.sh/).

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


# Data Science Environment Setup

## Sublime

Download and install Sublime Text 3
(Sublime)[https://www.sublimetext.com/3]

### Create symbolic link `subl`

Check `/usr/local/bin` directory is in your `PATH`:
```
echo $PATH
```

If not, edit `nano ~/.bash_profile` and add:
```
# Binary locations
export PATH=/bin:/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin:$PATH

# Make Sublime default editor (optional)
export EDITOR='subl -w'
```

Terminal:
```
source ~/.bash_profile 
```

Create symbolic link. In terminal:
```
sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl
```

### TODO: Install Python Linters


## Git

Following the instructions on [GitHub](https://help.github.com/articles/set-up-git/):

### Update Git
1. [Download and install the latest version of Git.](https://git-scm.com/downloads)
2. [Set your username in Git.](https://help.github.com/articles/setting-your-username-in-git)

In terminal:
```
git config --global user.name "Carrie Isaacson"
git config --global user.name
```

3. [Set your commit email address in Git.](https://help.github.com/articles/setting-your-commit-email-address-in-git)

In terminal:
```
git config --global user.email "email@example.com"
git config --global user.email
```

### Authenticating with GitHub from Git
Set up for cloning via HTTPS which is the strategy Github recommends (over cloning via SSH). Caching password using `osxkeychain`. Additional setup required for 2-factor.

Set up [caching GitHub password](https://help.github.com/articles/caching-your-github-password-in-git/).

Password will be stored after first prompt for username / password.

### TODO: Terminal

https://medium.com/swlh/power-up-your-terminal-using-oh-my-zsh-iterm2-c5a03f73a9fb

## R
Install R and R Studio.

[R](https://cran.r-project.org/bin/macosx/)
[RStudio](https://www.rstudio.com/products/rstudio/download/#download)

## Python

### Conda
Install Python 3 using Miniconda. I prefer this installation as it is much lighter than the full Anaconda distribution (35 packages vs 150+ / 3GB). 

Conda serves as both package manager (instead of `pip`, which is still available) and environment manager (instead of `virtualenv`). 
For an excellent bite-sized review of why-to-choose Conda, take a gander at [Conda: Myths and Misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/).

#### Useful References
* (Conda vs pip vs virtualenv)[https://conda.io/docs/commands.html]
* (Condo official cheat sheet PDF)[https://conda.io/docs/_downloads/conda-cheatsheet.pdf]
* (Save the Environment with Anaconda)[https://medium.com/data-science-in-practice/saving-the-environment-with-anaconda-ad68e603d8c5].

#### Install Conda / Save Default Environment

[miniconda](https://conda.io/miniconda.html)
Note: restart terminal before testing install
```
which python
```
```
conda list
```

I'm making a conscious effort here to keep the default environment as tidy as possible. Save default environment (for when I inevitably install packages in there I didn’t mean to).
```
conda env export --name root > base_env.yaml
conda list --export > base_env.txt
```

### Data Science Environment Creator

#### Cookiecutter

I was swayed by discussion with Peter Bull (DrivenData) on the (DataFramed Podcast)[https://www.datacamp.com/community/podcast/human-centered-design-data-science] that we would all be better off if data science projects had standard directory structures, an approach adopted by many frameworks eg Rails. The thinking is that this approach makes it easier to jump into someone else's project and orient quickly. 

In addition this standard structure encourages best practices, such as separating raw and processed data files and maintaining a project README.

For now I am adopting the DrivenData data science cookiecutter, but this includes infrastructure I do not or rarely require in my projects. For example, this setup includes requirements for packaging and command-line interfacts, neither are useful for a basic data-analysis task. This seems a little at odds with the general keepin-it-tidy approach. As I work with this framework I will consider preparing my own cookiecutter that fits my typical workflows.

```
conda create --name cookiecutter
conda activate cookiecutter
conda install -c conda-forge cookiecutter
conda deactivate
```

The following are external requirements specified in the cookiecutter that will not be installed by default at this time. I'll revisit this later:
```
# external requirements
click
Sphinx
coverage
awscli
flake8
python-dotenv>=0.5.1
```

#### Starting a Data Science Project

TODO: Convert this to a bash file. Write instructions.

Bash file:

```
conda deactivate
conda update conda

conda activate cookiecutter
cookiecutter https://github.com/drivendata/cookiecutter-data-science
conda deactivate

# create environment 
conda create --name $ENVIRONMENT_NAME
conda activate $ENVIRONMENT_NAME

conda install numpy
conda install scipy
conda install pandas
conda install scikit-learn
conda install matplotlib
conda install jupyter
conda install -c conda-forge jupyterlab

cd $ENVIRONMENT_NAME
conda env export > requirements.yaml
conda list --export > requirements.txt
```

Aliasing the bash file:

To start a new project: 


## TODO: Jupyter

