---
layout: post
title: Linux Shell and Bash
description: A Tech Talk on Linux and the Bash shell.
toc: True
comments: True
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 1}, 'csp': {'week': 0, 'categories': ['6.B']}, 'csa': {'week': 1}}
type: hacks
---

## Bash Display
> Hello Mr.Mortinson, this is a display of my Linux shell and bash

### Define variable
The following code cell <mark>defines 3 variables and assigns each a value</mark>.  There are some extra command, called a HERE document, that write these variables to a file.  This is so we can use these variables over and over below.


```python
%%script bash

# Dependency Variables, set to match your project directories

cat <<EOF > /tmp/variables.sh
export project_dir=$HOME/vscode  # change vscode to different name to test git clone
export project=\$project_dir/teacher  # change teacher to name of project from git clone
export project_repo="https://github.com/nighthawkcoders/teacher.git"  # change to project of choice
EOF
```

### Output the value of a variable
The following code cell <mark>outputs the value of the variables</mark>, using the echo command.  For visual understanding in the output, each echo command provide a title before the $variable 


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

# Output shown title and value variables
echo "Project dir: $project_dir"
echo "Project: $project"
echo "Repo: $project_repo"
```

    Project dir: /home/withereddagger/vscode
    Project: /home/withereddagger/vscode/teacher
    Repo: https://github.com/nighthawkcoders/teacher.git


## Project Setup and Analysis with Bash Scripts
The bash scripts that follow automate what was done in the setup procedures.  The purpose of this is to show that many of the commands we performed can be added to a script, then performed automatically.

### Pull Code
> Pull code from GitHub to your machine. This is a <mark>bash script</mark>, a sequence of commands, that will create a project directory and add the "project" from GitHub to the vscode directory.  There is conditional logic to make sure that clone only happen if it does not (!) exist.   Here are some key elements in this code...

- cd command (change directory), remember this from terminal session
- if statements (conditional statement, called selection statement by College Board), code inside only happens if condition is met


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Using conditional statement to create a project directory and project"

cd ~    # start in home directory

# Conditional block to make a project directory
if [ ! -d $project_dir ]
then 
    echo "Directory $project_dir does not exists... makinng directory $project_dir"
    mkdir -p $project_dir
fi
echo "Directory $project_dir exists." 

# Conditional block to git clone a project from project_repo
if [ ! -d $project ]
then
    echo "Directory $project does not exists... cloning $project_repo"
    cd $project_dir
    git clone $project_repo
    cd ~
fi
echo "Directory $project exists." 
```

    Using conditional statement to create a project directory and project
    Directory /home/withereddagger/vscode exists.
    Directory /home/withereddagger/vscode/teacher exists.


### Look at files Github project
> All computers contain files and directories.  The clone brought more files from cloud to your machine.  Review the bash shell script, observe the commands that show and interact with files and directories.  These were used during setup.

- "ls" lists computer files in Unix and Unix-like operating systems
- "cd" offers way to navigate and change working directory
- "pwd" print working directory
- "echo" used to display line of text/string that are passed as an argument


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list top level or root of files with project pulled from github"
ls

```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/withereddagger/vscode/teacher
    
    list top level or root of files with project pulled from github
    Gemfile
    LICENSE
    Makefile
    README.md
    _config.yml
    _data
    _includes
    _layouts
    _notebooks
    _posts
    assets
    csa.md
    csp.md
    csse.md
    images
    index.md
    indexBlogs.md
    scripts


### Look at file list with hidden and long attributes
> Most linux commands have options to enhance behavior.  The enhanced listing below shows permission bits, owner of file, size and date.

[ls reference](https://www.rapidtables.com/code/linux/ls.html)


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"
cd $project
pwd

echo ""
echo "list all files in long format"
ls -al   # all files -a (hidden) in -l long listing
```

    Navigate to project, then navigate to area wwhere files were cloned
    /home/withereddagger/vscode/teacher
    
    list all files in long format
    total 100
    drwxr-xr-x 12 withereddagger withereddagger 4096 Aug 22 10:24 .
    drwxr-xr-x  7 withereddagger withereddagger 4096 Aug 29 10:08 ..
    drwxr-xr-x  8 withereddagger withereddagger 4096 Aug 25 10:10 .git
    drwxr-xr-x  3 withereddagger withereddagger 4096 Aug 22 10:24 .github
    -rw-r--r--  1 withereddagger withereddagger  157 Aug 22 10:24 .gitignore
    -rw-r--r--  1 withereddagger withereddagger  122 Aug 22 10:24 Gemfile
    -rw-r--r--  1 withereddagger withereddagger 1081 Aug 22 10:24 LICENSE
    -rw-r--r--  1 withereddagger withereddagger 3131 Aug 22 10:24 Makefile
    -rw-r--r--  1 withereddagger withereddagger 6853 Aug 22 10:24 README.md
    -rw-r--r--  1 withereddagger withereddagger  607 Aug 22 10:24 _config.yml
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 _data
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 _includes
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 _layouts
    drwxr-xr-x  3 withereddagger withereddagger 4096 Aug 22 10:24 _notebooks
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 _posts
    drwxr-xr-x  4 withereddagger withereddagger 4096 Aug 22 10:24 assets
    -rw-r--r--  1 withereddagger withereddagger   92 Aug 22 10:24 csa.md
    -rw-r--r--  1 withereddagger withereddagger   98 Aug 22 10:24 csp.md
    -rw-r--r--  1 withereddagger withereddagger  108 Aug 22 10:24 csse.md
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 images
    -rw-r--r--  1 withereddagger withereddagger 5149 Aug 22 10:24 index.md
    -rw-r--r--  1 withereddagger withereddagger   53 Aug 22 10:24 indexBlogs.md
    drwxr-xr-x  2 withereddagger withereddagger 4096 Aug 22 10:24 scripts



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for posts"
export posts=$project/_posts  # _posts inside project
cd $posts  # this should exist per fastpages
pwd  # present working directory
ls -l  # list posts
```

    Look for posts
    /home/withereddagger/vscode/teacher/_posts
    total 88
    -rw-r--r-- 1 withereddagger withereddagger  7685 Aug 22 10:24 2023-08-16-Tools_Equipment.md
    -rw-r--r-- 1 withereddagger withereddagger  4650 Aug 22 10:24 2023-08-16-pair_programming.md
    -rw-r--r-- 1 withereddagger withereddagger  7137 Aug 22 10:24 2023-08-17-markdown-html_fragments.md
    -rw-r--r-- 1 withereddagger withereddagger  6659 Aug 22 10:24 2023-08-23-javascript-calculator.md
    -rw-r--r-- 1 withereddagger withereddagger 10642 Aug 22 10:24 2023-08-30-agile_methodolgy.md
    -rw-r--r-- 1 withereddagger withereddagger  3849 Aug 22 10:24 2023-08-30-javascript-music-api.md
    -rw-r--r-- 1 withereddagger withereddagger  5312 Aug 22 10:24 2023-09-06-javascript-motion-mario-oop.md
    -rw-r--r-- 1 withereddagger withereddagger  4812 Aug 22 10:24 2023-09-13-java-free_response.md
    -rw-r--r-- 1 withereddagger withereddagger 13220 Aug 22 10:24 2023-10-16-java-api-pojo-jpa.md
    -rw-r--r-- 1 withereddagger withereddagger  6819 Aug 22 10:24 2023-11-13-jwt-java-spring.md



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for notebooks"
export notebooks=$project/_notebooks  # _notebooks is inside project
cd $notebooks   # this should exist per fastpages
pwd  # present working directory
ls -l  # list notebooks
```

    Look for notebooks
    /home/withereddagger/vscode/teacher/_notebooks
    total 744
    -rw-r--r-- 1 withereddagger withereddagger  13014 Aug 22 10:24 2023-08-01-cloud_database.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   8992 Aug 22 10:24 2023-08-01-mario_player.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  43705 Aug 22 10:24 2023-08-02-cloud-workspace-automation.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  22060 Aug 22 10:24 2023-08-03-mario_block.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  11791 Aug 22 10:24 2023-08-03-mario_platform.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  19450 Aug 22 10:24 2023-08-03-mario_tube.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  24387 Aug 22 10:24 2023-08-04-mario_background.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   3496 Aug 22 10:24 2023-08-07-mario_lesson.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  10110 Aug 22 10:24 2023-08-15-java-hello.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  25624 Aug 22 10:24 2023-08-16-github_pages_setup.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  16156 Aug 22 10:24 2023-08-16-linux_shell.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  12761 Aug 25 10:11 2023-08-16-python_hello.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   9425 Aug 22 10:24 2023-08-23-github_pages_anatomy.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  22668 Aug 22 10:24 2023-08-23-java-console_games.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   9038 Aug 22 10:24 2023-08-23-python_tricks.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  10152 Aug 22 10:24 2023-08-30-javascript_top_10.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   9689 Aug 22 10:24 2023-08-30-showcase-S1-pair.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   7192 Aug 22 10:24 2023-09-05-python-flask-anatomy.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  22157 Aug 22 10:24 2023-09-06-AWS-deployment.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  14380 Aug 22 10:24 2023-09-06-java-primitives.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  11671 Aug 22 10:24 2023-09-06-javascript-input.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  13706 Aug 22 10:24 2023-09-12-java_menu_class.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   9562 Aug 22 10:24 2023-09-13-java_fibonaccii_class.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  44217 Aug 22 10:24 2023-09-13-javascript_output.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  43423 Aug 22 10:24 2023-09-13-python-pandas_intro.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  11578 Aug 22 10:24 2023-09-20-java-image_2D.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  26739 Aug 22 10:24 2023-09-20-javascript_motion_dog.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  13599 Aug 22 10:24 2023-10-02-java-spring-anatomy.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  12429 Aug 22 10:24 2023-10-09-java-chatgpt.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  15632 Aug 22 10:24 2023-10-09-javascript_api.ipynb
    -rw-r--r-- 1 withereddagger withereddagger 113091 Aug 22 10:24 2023-10-09-python_machine_learing_fitness.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  16271 Aug 22 10:24 2023-11-13-jwt-python-flask.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  15951 Aug 22 10:24 2023-11-13-vulnerabilities.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  18328 Aug 22 10:24 2023-11-20-jwt-java-spring-challenge.md
    -rw-r--r-- 1 withereddagger withereddagger  10745 Aug 22 10:24 2024-01-04-cockpit-setup.ipynb
    drwxr-xr-x 2 withereddagger withereddagger   4096 Aug 22 10:24 files



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Look for images in notebooks, print working directory, list files"
cd $notebooks/images  # this should exist per fastpages
pwd
ls -l
```

    Look for images in notebooks, print working directory, list files
    /home/withereddagger/vscode/studentProjectCSP1/_notebooks
    total 1152
    -rw-r--r-- 1 withereddagger withereddagger 992221 Sep  4 21:08 2023-07-15-machine_learning.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  44387 Sep  7 22:00 2023-08-16-linux_shell.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  12763 Sep  4 21:07 2023-08-16-python_hello.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   5415 Aug 17 19:41 2023-08-17-AP-pseudo-vs-python.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   5506 Aug 29 21:00 2023-08-17-Markdown_Table_Code_Hack.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   8948 Aug 29 21:00 2023-08-21-HTML_Image_Hack.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   8615 Aug 17 19:41 2023-08-21-VSCode-GitHub_Pages.ipynb
    -rw-r--r-- 1 withereddagger withereddagger   3549 Sep  4 21:06 2023-09-01-yes_quiz.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  11036 Sep  7 21:18 2023-09-05-galaga.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  11273 Sep  4 21:08 2023-09-06-javascript-input.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  14912 Sep  7 09:59 2023-09-06-javascript-output-jquery.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  12429 Sep  7 10:00 2023-10-09-java-chatgpt.ipynb
    -rw-r--r-- 1 withereddagger withereddagger  17885 Sep  7 21:21 2023-10-09-javascript_api.ipynb


    bash: line 6: cd: /images: No such file or directory


### Look inside a Markdown File
> "cat" reads data from the file and gives its content as output


```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

echo "Navigate to project, then navigate to area wwhere files were cloned"

cd $project
echo "show the contents of README.md"
echo ""

cat README.md  # show contents of file, in this case markdown
echo ""
echo "end of README.md"

```

    Navigate to project, then navigate to area wwhere files were cloned
    show the contents of README.md
    
    ## Teacher Blog site
    This site is intended for the development of Teacher content.  This blogging site is built using GitHub Pages [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).
    - The purpose is to build lessons and distribute across different Computer Science sections (CSSE, CSP, CSA), a pathway that covers 3 years of High School Instruction.
    - The primary languages and frameworks that are taught are `JavaScript/HTML/CSS`, `Python/Flask`, `Java/Spring`.  Read below for more details.
    - In this course, Teacher content is not exclusively developed by Teachers.  In fact, many Students have been invited to develop and publish content into this repository.  Their names will appear as authors on the content which they aided in producing.
    - This site has incorporated ideas and has radically modified scripts from the now deprecated [fastpages](https://github.com/fastai/fastpages) repository.
    - This site includes assistance and guideance from ChatGPT, [chat.openai.com](https://chat.openai.com/) 
    
    ### Courses and Pathway
    The focus of the Del Norte Computer Science three-year pathway is `Full Stack Web Development`.  This focus provides a variety of technologies and exposures.  The intention of the pathway is breadth and exposure.
    - `JavaScript` documents are focused on frontend development and for entry class into the Del Norte Computer Science pathway.  JavaScript documents and materials are a prerequisites to Python and Java classes.
    - `Python` documents are focused on backend development and requirements for the AP Computer Science Principles exam.
    - `Java` documents are focused on backend development and requirements for the AP Computer Sciene A exam.
    - `Data Structures` materials embedded into JavaScript, Python, or Java documents are focused on college course articulation.
    
    ### Resources and Instruction
    The materials, such as this README, as well as `Tools`, `DevOps`, and `Collaboration` resources are integral part of this course and Computer Science in general.  Everything in our environment is part of our learning of Computer Science. 
    - `Visual Studio Code` is key the code-build-debug cycle editor used in this course, [VSCode download](https://code.visualstudio.com/).  This is an example of a resource, but inside of it it has features for collaboration.
    - `Tech Talks`, aka lectures, are intended to be interactive and utilize `Jupyter Notebooks` and Websites.  This is an example of blending instruction and tools together, which in turn provide additional resources for learning.  For instance, deep knowledge on  GitHub Pages and Notebooks are valuable in understanding principles behind Full Stack Development and Data Science. 
    
    ## GitHub Pages
    All `GitHub Pages` websites are managed on GitHub infrastructure. GitHub uses `Jekyll` to tranform your content into static websites and blogs. Each time we change files in GitHub it initiates a GitHub Action that rebuilds and publishes the site with Jekyll.  
    - GitHub Pages is powered by: [Jekyll](https://jekyllrb.com/).
    - Publised teacher website: [nighthawkcoders.github.io/teacher](https://nighthawkcoders.github.io/teacher/)
    
    ## Preparing a Preview Site 
    In all development, it is recommended to test your code before deployment.  The GitHub Pages development process is optimized by testing your development on your local machine, prior to files on GitHub
    
    Development Cycle. For GitHub pages, the tooling described below will create a development cycle  `make-code-save-preview`.  In the development cycle, it is a requirement to preview work locally, prior to doing a VSCode `commit` to git.
    
    Deployment Cycle.  In the deplopyment cycle, `sync-github-action-review`, it is a requirement to complete the development cycle prior to doing a VSCode `sync`.  The sync triggers github repository update.  The action starts the jekyll build to publish the website.  Any step can have errors and will require you to do a review.
    
    ### WSL and/or Ubuntu installation requirements
    - The result of these step is Ubuntu tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/ubuntu/)
    ```bash
    # 
    # WSL/Ubuntu setup
    #
    mkdir mkdir vscode
    git clone https://github.com/nighthawkcoders/teacher.git
    # run script, path vscode/teacher are baked in script
    ~/vscode/teacher/scripts/activate_ubuntu.sh
    #=== !!!Start a new Terminal!!! ===
    #=== Continue to next section ===
    ```
    
    ### MacOs installation requirements 
    - Ihe result of these step are MacOS tools to run preview server.  These procedures were created using [jekyllrb.com](https://jekyllrb.com/docs/installation/macos/). 
    
    ```bash
    # 
    # MacOS setup
    #
    mkdir mkdir vscode
    git clone https://github.com/nighthawkcoders/teacher.git
    # run script, path vscode/teacher are baked in script
    ~/vscode/teacher/scripts/activate_macos.sh
    #=== !!!Start a new Terminal!!! ===
    #=== Continue to next section ===
    ```
    
    
    ### Run Preview Server
    - The result of these step is server running on: http://0.0.0.0:4100/teacher/.  Regeneration messages will run in terminal on any save and update site upon refresh.  Terminal is active, press the Enter or Return key in the terminal at any time to see prompt to enter commands.
    
    - Complete installation
    ```bash
    cd ~/vscode/teacher
    bundle install
    make
    ```
    - Run Server.  This requires running terminal commands `make`, `make stop`, `make clean`, or `make convert` to manage the running server.  Logging of details will appear in terminal.   A `Makefile` has been created in project to support commands and start processes.
    
        - Start preview server in terminal
        ```bash
        cd ~/vscode/teacher  # my project location, adapt as necessary
        make
        ```
    
        - Terminal output of shows server address. Cmd or Ctl click http location to open preview server in browser. Example Server address message... 
        ```
        Server address: http://0.0.0.0:4100/teacher/
        ```
    
        - Save on ipynb or md activiates "regeneration". Refresh browser to see updates. Example terminal message...
        ```
        Regenerating: 1 file(s) changed at 2023-07-31 06:54:32
            _notebooks/2024-01-04-cockpit-setup.ipynb
        ```
    
        - Terminal message are generated from background processes.  Click return or enter to obtain prompt and use terminal as needed for other tasks.  Alway return to root of project `cd ~/vscode/teacher` for all "make" actions. 
            
    
        - Stop preview server, but leave constructed files in project for your review.
        ```bash
        make stop
        ```
    
        - Stop server and "clean" constructed files, best choice when renaming files to eliminate potential duplicates in constructed files.
        ```bash
        make clean
        ```
    
        - Test notebook conversions, best choice to see if IPYNB conversion is acting up.
        ```bash
        make convert
        ```
        
    end of README.md


## Env, Git and GitHub
> Env(ironment) is used to capture things like path to Code or Home directory.  Git and GitHub is NOT Only used to exchange code between individuals, it is often used to exchange code through servers, in our case deployment for Website.   All tools we use have a behind the scenes relationships with the system they run on (MacOS, Windows, Linus) or a relationship with servers which they are connected to (ie GitHub).  There is an "env" command in bash.  There are environment files and setting files (.git/config) for Git.  They both use a key/value concept.

- "env" show setting for your shell
- "git clone" sets up a director of files
- "cd $project" allows user to move inside that directory of files
- ".git" is a hidden directory that is used by git to establish relationship between machine and the git server on GitHub.  


```python
%%script bash

# This command has no dependencies

echo "Show the shell environment variables, key on left of equal value on right"
echo ""

env
```

    Show the shell environment variables, key on left of equal value on right
    
    SHELL=/bin/bash
    PYTHONUNBUFFERED=1
    WSL2_GUI_APPS_ENABLED=1
    WSL_DISTRO_NAME=Ubuntu-22.04
    ELECTRON_RUN_AS_NODE=1
    VSCODE_AMD_ENTRYPOINT=vs/workbench/api/node/extensionHostProcess
    NAME=DESKTOP-SLNJLQO
    PWD=/home/withereddagger/vscode/studentProjectCSP1/_notebooks
    LOGNAME=withereddagger
    PYDEVD_IPYTHON_COMPATIBLE_DEBUGGING=1
    HOME=/home/withereddagger
    LANG=C.UTF-8
    WSL_INTEROP=/run/WSL/392_interop
    LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
    WAYLAND_DISPLAY=wayland-0
    CLICOLOR=1
    VSCODE_L10N_BUNDLE_LOCATION=
    GEM_HOME=/home/withereddagger/gems
    LESSCLOSE=/usr/bin/lesspipe %s %s
    VSCODE_HANDLES_SIGPIPE=true
    TERM=xterm-color
    LESSOPEN=| /usr/bin/lesspipe %s
    USER=withereddagger
    GIT_PAGER=cat
    PYTHONIOENCODING=utf-8
    DISPLAY=:0
    SHLVL=1
    PAGER=cat
    VSCODE_CWD=/mnt/c/Users/Waheg/AppData/Local/Programs/Microsoft VS Code
    MPLBACKEND=module://matplotlib_inline.backend_inline
    XDG_RUNTIME_DIR=/run/user/1000/
    WSLENV=VSCODE_WSL_EXT_LOCATION/up
    VSCODE_WSL_EXT_LOCATION=/mnt/c/Users/Waheg/.vscode/extensions/ms-vscode-remote.remote-wsl-0.80.2
    XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
    PATH=/bin:/home/withereddagger/.vscode-server/bin/6c3e3dba23e8fadc360aed75ce363ba185c49794/bin/remote-cli:/home/withereddagger/.local/bin:/home/withereddagger/gems/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Program Files/Eclipse Adoptium/jdk-8.0.382.5-hotspot/bin:/mnt/c/Program Files (x86)/VMware/VMware Player/bin/:/mnt/c/Program Files/National Instruments/Shared/OpenVINO/:/mnt/c/Program Files/Common Files/Oracle/Java/javapath:/mnt/c/Program Files (x86)/Razer Chroma SDK/bin:/mnt/c/Program Files/Razer Chroma SDK/bin:/mnt/c/Program Files (x86)/Common Files/Oracle/Java/javapath:/mnt/c/Program Files (x86)/Razer/ChromaBroadcast/bin:/mnt/c/Program Files/Razer/ChromaBroadcast/bin:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/NVIDIA Corporation/NVIDIA NvDLISR:/mnt/c/Windows/system32/config/systemprofile/AppData/Local/Microsoft/WindowsApps:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/dotnet/:/mnt/c/Program Files/Git/cmd:/mnt/c/Program Files/CMake/bin:/mnt/c/Program Files/nodejs/:/mnt/c/Users/Waheg/AppData/Local/Programs/Python/Python311/Scripts/:/mnt/c/Users/Waheg/AppData/Local/Programs/Python/Python311/:/mnt/c/Users/Waheg/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/Waheg/AppData/Local/Programs/Microsoft VS Code/bin:/mnt/c/src/flutter/flutter/bin:/mnt/c/Program Files/CMake/bin:/mnt/c/Users/Waheg/AppData/Roaming/npm:/snap/bin:/home/withereddagger/.vscode-server/bin/6c3e3dba23e8fadc360aed75ce363ba185c49794/bin/remote-cli:/home/withereddagger/.local/bin:/home/withereddagger/gems/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/wsl/lib:/mnt/c/Program Files/Eclipse Adoptium/jdk-8.0.382.5-hotspot/bin:/mnt/c/Program Files (x86)/VMware/VMware Player/bin/:/mnt/c/Program Files/National Instruments/Shared/OpenVINO/:/mnt/c/Program Files/Common Files/Oracle/Java/javapath:/mnt/c/Program Files (x86)/Razer Chroma SDK/bin:/mnt/c/Program Files/Razer Chroma SDK/bin:/mnt/c/Program Files (x86)/Common Files/Oracle/Java/javapath:/mnt/c/Program Files (x86)/Razer/ChromaBroadcast/bin:/mnt/c/Program Files/Razer/ChromaBroadcast/bin:/mnt/c/Windows/system32:/mnt/c/Windows:/mnt/c/Windows/System32/Wbem:/mnt/c/Windows/System32/WindowsPowerShell/v1.0/:/mnt/c/Windows/System32/OpenSSH/:/mnt/c/Program Files (x86)/NVIDIA Corporation/PhysX/Common:/mnt/c/Program Files/NVIDIA Corporation/NVIDIA NvDLISR:/mnt/c/Windows/system32/config/systemprofile/AppData/Local/Microsoft/WindowsApps:/mnt/c/WINDOWS/system32:/mnt/c/WINDOWS:/mnt/c/WINDOWS/System32/Wbem:/mnt/c/WINDOWS/System32/WindowsPowerShell/v1.0/:/mnt/c/WINDOWS/System32/OpenSSH/:/mnt/c/Program Files/dotnet/:/mnt/c/Program Files/Git/cmd:/mnt/c/Program Files/CMake/bin:/mnt/c/Program Files/nodejs/:/mnt/c/Users/Waheg/AppData/Local/Programs/Python/Python311/Scripts/:/mnt/c/Users/Waheg/AppData/Local/Programs/Python/Python311/:/mnt/c/Users/Waheg/AppData/Local/Microsoft/WindowsApps:/mnt/c/Users/Waheg/AppData/Local/Programs/Microsoft VS Code/bin:/mnt/c/src/flutter/flutter/bin:/mnt/c/Program Files/CMake/bin:/mnt/c/Users/Waheg/AppData/Roaming/npm:/snap/bin
    DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
    VSCODE_NLS_CONFIG={"locale":"en","osLocale":"en","availableLanguages":{}}
    HOSTTYPE=x86_64
    PULSE_SERVER=unix:/mnt/wslg/PulseServer
    VSCODE_HANDLES_UNCAUGHT_ERRORS=true
    VSCODE_IPC_HOOK_CLI=/run/user/1000/vscode-ipc-144c404d-14a5-4026-92cc-9e6c857e9bca.sock
    _=/bin/env



```python
%%script bash

# Extract saved variables
source /tmp/variables.sh

cd $project

echo ""
echo "show the secrets of .git"
cd .git
ls -l

echo ""
echo "look at config file"
cat config
```

    
    show the secrets of .git
    total 56
    -rw-r--r--  1 withereddagger withereddagger   102 Aug 25 10:38 FETCH_HEAD
    -rw-r--r--  1 withereddagger withereddagger    21 Aug 22 10:24 HEAD
    drwxr-xr-x  2 withereddagger withereddagger  4096 Aug 22 10:24 branches
    -rw-r--r--  1 withereddagger withereddagger   267 Aug 22 10:24 config
    -rw-r--r--  1 withereddagger withereddagger    73 Aug 22 10:24 description
    drwxr-xr-x  2 withereddagger withereddagger  4096 Aug 22 10:24 hooks
    -rw-r--r--  1 withereddagger withereddagger 11702 Aug 22 10:24 index
    drwxr-xr-x  2 withereddagger withereddagger  4096 Aug 22 10:24 info
    drwxr-xr-x  3 withereddagger withereddagger  4096 Aug 22 10:24 logs
    drwxr-xr-x 57 withereddagger withereddagger  4096 Aug 25 10:38 objects
    -rw-r--r--  1 withereddagger withereddagger   112 Aug 22 10:24 packed-refs
    drwxr-xr-x  5 withereddagger withereddagger  4096 Aug 22 10:24 refs
    
    look at config file
    [core]
    	repositoryformatversion = 0
    	filemode = true
    	bare = false
    	logallrefupdates = true
    [remote "origin"]
    	url = https://github.com/nighthawkcoders/teacher.git
    	fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "main"]
    	remote = origin
    	merge = refs/heads/main


## Advanced Student Request - Make a file in Bash
> This example was requested by a student (Jun Lim, CSA). The request was to make jupyer file using bash, I adapted the request to markdown.  This type of thought will have great extrapolation to coding and possibilities of using List, Arrays, or APIs to build user interfaces.  JavaScript is a language where building HTML is very common.

> To get more interesting output from terminal, this will require using something like mdless (https://github.com/ttscoff/mdless).  This enables see markdown in rendered format.
- On Desktop [Install PKG from MacPorts](https://www.macports.org/install.php)
- In Terminal on MacOS
    - [Install ncurses](https://ports.macports.org/port/ncurses/)
    - ```gem install mdless```
    
> Output of the example is much nicer in "jupyter"


```bash
%%bash
# Print a greeting
echo "Welcome to the Enhanced Interactive Bash Script in Jupyter Notebook!"

# Display the current date and time
date

# List files in the current directory
ls

# Create a new directory and enter it
mkdir example_directory
cd example_directory

# Create a sample text file
echo "This is the initial content of the file." > sample.txt

# Display the original content of the file
echo "Original content of 'sample.txt':"
cat sample.txt

# Define a variable with new content
new_content="This is the updated content of the file."

# Write the new content to the file
echo "$new_content" > sample.txt

# Display the updated content of the file
echo "Updated content of 'sample.txt':"
cat sample.txt

# Perform some basic arithmetic
echo "5 + 3 = $((5 + 3))"
echo "10 / 2 = $((10 / 2))"

# Display system information
echo "System Information:"
uname -a

# Display available disk space
df -h

# Create and manipulate an array
fruits=("Apple" "Banana" "Cherry" "Date")
echo "Fruits in the array:"
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done

# Perform a loop with conditional statements
echo "Numbers from 1 to 10 (even numbers only):"
for ((i=1; i<=10; i++)); do
    if ((i % 2 == 0)); then
        echo "$i"
    fi
done

# Exit the created directory
cd ..

# Remove the example directory and its contents
rm -r example_directory

# Print a farewell message
echo "Thanks for using the Enhanced Interactive Bash Script!"

```

    Welcome to the Enhanced Interactive Bash Script in Jupyter Notebook!
    Thu Sep  7 22:00:21 PDT 2023
    2023-07-15-machine_learning.ipynb
    2023-08-16-linux_shell.ipynb
    2023-08-16-python_hello.ipynb
    2023-08-17-AP-pseudo-vs-python.ipynb
    2023-08-17-Markdown_Table_Code_Hack.ipynb
    2023-08-21-HTML_Image_Hack.ipynb
    2023-08-21-VSCode-GitHub_Pages.ipynb
    2023-09-01-yes_quiz.ipynb
    2023-09-05-galaga.ipynb
    2023-09-06-javascript-input.ipynb
    2023-09-06-javascript-output-jquery.ipynb
    2023-10-09-java-chatgpt.ipynb
    2023-10-09-javascript_api.ipynb
    Original content of 'sample.txt':
    This is the initial content of the file.
    Updated content of 'sample.txt':
    This is the updated content of the file.
    5 + 3 = 8
    10 / 2 = 5
    System Information:
    Linux DESKTOP-SLNJLQO 5.15.90.1-microsoft-standard-WSL2 #1 SMP Fri Jan 27 02:56:13 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
    Filesystem      Size  Used Avail Use% Mounted on
    none            3.9G  4.0K  3.9G   1% /mnt/wsl
    none            458G  386G   72G  85% /usr/lib/wsl/drivers
    none            3.9G     0  3.9G   0% /usr/lib/wsl/lib
    /dev/sdc       1007G  4.1G  952G   1% /
    none            3.9G   96K  3.9G   1% /mnt/wslg
    rootfs          3.9G  1.9M  3.9G   1% /init
    none            3.9G  892K  3.9G   1% /run
    none            3.9G     0  3.9G   0% /run/lock
    none            3.9G     0  3.9G   0% /run/shm
    none            3.9G     0  3.9G   0% /run/user
    tmpfs           4.0M     0  4.0M   0% /sys/fs/cgroup
    none            3.9G  320K  3.9G   1% /mnt/wslg/versions.txt
    none            3.9G  320K  3.9G   1% /mnt/wslg/doc
    drvfs           458G  386G   72G  85% /mnt/c
    snapfuse        128K  128K     0 100% /snap/bare/5
    snapfuse         74M   74M     0 100% /snap/core22/858
    snapfuse         74M   74M     0 100% /snap/core22/864
    snapfuse         92M   92M     0 100% /snap/gtk-common-themes/1535
    snapfuse         54M   54M     0 100% /snap/snapd/19457
    snapfuse         41M   41M     0 100% /snap/snapd/19993
    snapfuse        131M  131M     0 100% /snap/ubuntu-desktop-installer/1229
    snapfuse        131M  131M     0 100% /snap/ubuntu-desktop-installer/1231
    Fruits in the array:
    Apple
    Banana
    Cherry
    Date
    Numbers from 1 to 10 (even numbers only):
    2
    4
    6
    8
    10
    Thanks for using the Enhanced Interactive Bash Script!



