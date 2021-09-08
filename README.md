# Machine Setup

Description of my current machine setup optimized for data science projects.
My philosophy is to keep the default Python environment very sparse. When I start a new project I start a new environment, install the standard DS packages (e.g. numpy, pandas, scikit), use cookiecutter for a standard directory structure and start a new git repo (not necessarily in that order).

This setup culminates with a script to initialize a data science project in a consistent manner.

This documents my essential setup details, in case my current machine explodes or gets run over by a bus or something.

TODO: alternative using docker for some or all projects. 
TODO: fork and simplify cookiecutter-data-science


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

## TODO: PyCharm

Install the [PyCharm Community IDE](https://www.jetbrains.com/pycharm/download/#section=mac) 

## TODO: Install Python Linters


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

```
git config --global credential.helper osxkeychain
```

Create a [personal access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

Password will be stored after first prompt for username / password.


## Tweaking Terminal (Zsh, Oh-my-Zsh, iTerm2)

Make the Terminal environment a little more useful and a lot more colourful using iTerm2 and Oh-my-Zsh. Instructions adapted from [here](https://medium.com/swlh/power-up-your-terminal-using-oh-my-zsh-iterm2-c5a03f73a9fb) and [here](https://medium.freecodecamp.org/jazz-up-your-zsh-terminal-in-seven-steps-a-visual-guide-e81a8fd59a38).

This is especially useful for Git tracking, as Zsh / Oh-my-Zsh do things like indicate which branch you're on and colour coding when there are uncomitted changes. It's very helpful when using command-line Git.

### Zsh

[The Z shell](http://www.zsh.org/) (also known as zsh) is a Unix shell that is built on top of bash (the default shell for macOS) with additional features.

```
brew install zsh
```

### Oh My Zsh

[Oh My Zsh](https://ohmyz.sh/) is an open source, community driven framework for managing zsh configuration. It has a lot of features to customise the terminal and a lot of themes available.

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### iTerm2

[iTerm2](https://www.iterm2.com/) is a replacement for Terminal and the successor to iTerm.

Features:
* Split Panes - new split: &#8984; + d; switch between views &#8984; + [
* Hotkey Window - Totally worth it setting up a Dedicated Hotkey Window. [How to set it up](https://www.iterm2.com/documentation-hotkey.html)
* Search
* Autocomplete
* Mouseless Copy
* Paste History
* Instant Replay

Download and install [here](https://www.iterm2.com/downloads.html).

Note: I had a problem with losing my $PATH. I had to add the following to the top of my `open ~/.zshrc` file and restart iTerm:

```
# Specify $PATH
source ~/.bash_profile
```


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
conda list --export > base_env.txt
```

#### Environments

I like to create environments for general work areas.
If a project is likely to be productionalized later (as opposed to a general analysis env or working on dbt models), then creating a separate env is appropriate.

I like having a general analysis (name it how you like, "analysis") that you can dump every package under the sun into. If a project is going to be shared
```
conda create --name analysis
conda install numpy
conda install scipy
conda install pandas
conda install scikit-learn
conda install matplotlib
conda install jupyter
conda install jupyterlab
```

### Accessing Snowflake via Python Connector


```
conda activate analysis
pip install --upgrade snowflake-sqlalchemy
pip install pandas
```

(did I miss other required installs here?)


Here's how I load snowflake passwords. I create a package (<packagename>) with a very basic script for loading credentials and 
Make a new directory in the analysis env in the folder lib/python<version>/site-packages using 

```
cd ~/opt/miniconda3/envs/analysis/lib/python3.9/site-packages
mkdir <packagename>
touch __init__.py
subl __init__.py
```

Insert the following, sourced [here](https://www.analyticsvidhya.com/blog/2021/05/one-stop-shop-for-connecting-snowflake-to-python/), into __init__.py:

```
from sqlalchemy import create_engine
from snowflake.sqlalchemy import URL

def connect_to_snowflake():
	url = URL(
	    account = '<accountname>',
	    user = '<username>',
	    password = '<password>',
	    warehouse= '<warehousename>',
	)
	engine = create_engine(url)
	cxn = engine.connect()
    print('connection extablished usage: pd.read_sql(<query_name>, <cxn>)')
    return(cxn)
```

Note that account name appears in the snowflake UI url 
https://<accountname>.snowflakecomputing.com/console#/internal/worksheet
https://app.snowflake.com/us-west-2/<accountname>

Usage:

```
import <packagename>

query = '''select * from <snowflake DB tablename>'''
data = pd.read_sql(query, cxn)
```


### Install DBT

Create an environment for working in the dbt_models repo:
```
conda create --name dbt_models
```

[DBT installation instructions](https://docs.getdbt.com/dbt-cli/installation)

