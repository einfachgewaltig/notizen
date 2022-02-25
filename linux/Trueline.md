Trueline
========



[https://awesomeopensource.com/project/petobens/trueline](https://awesomeopensource.com/project/petobens/trueline)

























[![media-PcBpPT](media/media-PcBpPT.gif)
](https://awesomeopensource.com)Awesome Open SourceAwesome Open SourceTruelineFast and extensible bash powerline prompt with true color and fancy icon supportStars278


Licensemit[Open Issues](https://github.com/petobens/trueline/issues)[7](https://github.com/petobens/trueline/issues)Most Recent Commit9 months ago


[Repo](https://github.com/petobens/trueline)Related Projects[Shell Projects (228,493)](https://awesomeopensource.com/projects/shell)[Bash Projects (7,110)](https://awesomeopensource.com/projects/bash)[Terminal Projects (4,217)](https://awesomeopensource.com/projects/terminal)[Prompt Projects (472)](https://awesomeopensource.com/projects/prompt)[Powerline Projects (153)](https://awesomeopensource.com/projects/powerline)[Ps1 Projects (127)](https://awesomeopensource.com/projects/ps1)
# 


Trueline: Bash Powerline Style Prompt with True Color Support

Trueline is a fast and extensible [Powerline](https://awesomeopensource.com/project/powerline/powerline)
style bash prompt with true color (24-bit) and fancy glyph support.

The pure Bash code implementation and overall features are modelled after the excellent
[Pureline](https://awesomeopensource.com/project/chris-marsh/pureline) command prompt. However Trueline also
adds the ability to use RGB color codes, expands icon/glyph usage across prompt segments
(inspired by [Powerlevel9k](https://awesomeopensource.com/project/bhilburn/powerlevel9k)), simplifies
configuration and, among other goodies, shows the current input mode (when in vi-mode).

![media-CElSKF](media/media-CElSKF.png)


## 


Installation

Download the 
```
trueline.sh
```
script in this repo and source it from within your 
```
.bashrc
```

file:

```

```
$> git clone https://github.com/petobens/trueline ~/trueline
$> echo 'source ~/trueline/trueline.sh' >> ~/.bashrc

```

```

or alternatively

```

```
$> wget https://raw.githubusercontent.com/petobens/trueline/master/trueline.sh -P ~/
$> echo 'source ~/trueline.sh' >> ~/.bashrc

```

```

If you use a font that supports "Powerline" glyphs, such as those included in the
wonderful [Nerd Fonts](https://awesomeopensource.com/project/ryanoasis/nerd-fonts) project, then the prompt
should render properly and no further configuration is necessary (as long as you like the
default settings shown in the image above).

## 


Customization

Customizing and extending the prompt is easy and there are several segment options
available to do so.

All settings go inside your 
```
.bashrc
```
and must be defined before actually sourcing the

```
trueline.sh
```
file (otherwise default settings will be used). To see how this works let's
start with a simple configuration example:

```

```
declare -A TRUELINE_COLORS=(
[light_blue]='75;161;207'
[grey]='99;99;100'
[pink]='199;88;157'
)

declare -a TRUELINE_SEGMENTS=(
'working_dir,light_blue,black,normal'
'git,grey,black,normal'
'time,white,black,normal'
'newline,pink,black,bold'
)

declare -A TRUELINE_SYMBOLS=(
[git_modified]='*'
[git_github]=''
[segment_separator]=''
[working_dir_folder]='...'
[working_dir_separator]='/'
[working_dir_home]='~'
[newline]='❯'
[clock]='🕒'
)

TRUELINE_GIT_SHOW_STATUS_NUMBERS=false
TRUELINE_GIT_MODIFIED_COLOR='grey'
TRUELINE_WORKING_DIR_SPACE_BETWEEN_PATH_SEPARATOR=false

_trueline_time_segment() {
local prompt_time="${TRUELINE_SYMBOLS[clock]} \t"
if [[ -n "$prompt_time" ]]; then
local fg_color="$1"
local bg_color="$2"
local font_style="$3"
local segment="$(_trueline_separator)"
segment+="$(_trueline_content "$fg_color" "$bg_color" "$font_style" " $prompt_time ")"
PS1+="$segment"
_trueline_record_colors "$fg_color" "$bg_color" "$font_style"
fi
}

source ~/trueline/trueline.sh

```

```

which generates the following prompt (that essentially replicates the minimal ZSH
[Pure](https://awesomeopensource.com/project/sindresorhus/pure) prompt):

![media-hgkaje](media/media-hgkaje.png)


You can see in the config above that there are basically 5 different/relevant settings:
colors, segments, symbols, options and extensions. Let's break each of these down.

### 


Colors

Colors are defined by means of an associative array named 
```
TRUELINE_COLORS
```
. The keys of
this array are color names and the values RGB color codes:

```

```
declare -A TRUELINE_COLORS=(
[color_name]='red;green;blue'
)

```

```

Default colors are loosely based on [Atom's One Dark
theme](https://atom.io/themes/one-dark-syntax) and given by:

```

```
declare -A TRUELINE_COLORS=(
[black]='36;39;46'
[cursor_grey]='40;44;52'
[green]='152;195;121'
[grey]='171;178;191'
[light_blue]='97;175;239'
[mono]='130;137;151'
[orange]='209;154;102'
[purple]='198;120;221'
[red]='224;108;117'
[special_grey]='59;64;72'
[white]='208;208;208'
)

```

```

Any 
```
TRUELINE_COLORS
```
array defined in the bashrc file prior to sourcing the Trueline
script will actually update the default array above (in the sense that it will overwrite
existing keys and add non-existing ones). This basically means that default colors can
always be used and the array only needs to be defined when new extra colors are truly
needed.

*Note:* you can define any color name you want except for 
```
default_bg
```
which is used by
Trueline to obtain the default terminal background color.

### 


Segments

Prompt segments are defined in an ordered array called 
```
TRUELINE_SEGMENTS
```
that has the
following structure:

```

```
declare -a TRUELINE_SEGMENTS=(
'segment_name,segment_fg_color,segment_bg_color,font_style'
)

```

```

where the segment foreground and background color names are keys of the 
```
TRUELINE_COLORS
```

array and the font style is either 
```
bold
```
, 
```
dim
```
, 
```
italic
```
, 
```
normal
```
or 
```
underlined
```
. The
order of the elements in the array define the order in which each segment is rendered in
the prompt.

Trueline offers the following segments (status indicates whether they are enabled/rendered
by default):




Segment Name
Status
Description




aws_profile
enabled
current AWS profile


bg_jobs
enabled
number of background jobs


cmd_duration
disabled
last command execution time


conda_env
enabled
current anaconda environment


exit_status
enabled
return code of last command


git
enabled
git branch/remote and repository status


newline
disabled
splits prompt segments across multiple lines


read_only
enabled
indicator of read only directory


user
enabled
username and host (conditional on ssh status)


venv
enabled
Python virtual environment


working_dir
enabled
current working directory




but more segments can be easily added (see [Extensions](https://awesomeopensource.com/project/petobens/trueline#Extensions)).

To enable the newline segment one could use the following config:

```

```
declare -a TRUELINE_SEGMENTS=(
'working_dir,mono,cursor_grey,normal'
'git,grey,special_grey,normal'
'newline,black,orange,bold'
)

```

```

which results in:
![media-GVQQhp](media/media-GVQQhp.png)


### 


Symbols

Symbols (i.e icons/glyphs) are defined through an associative array named

```
TRUELINE_SYMBOLS
```
where each entry key is a (predefined) segment symbol name and the
value is the actual symbol/icon:

```

```
declare -A TRUELINE_SYMBOLS=(
[segment_symbol_name]='|' # actual symbol
)

```

```

The following table shows the current predefined symbol names along with their default
values (i.e either the actual glyph or the corresponding nerd-font unicode code):




Symbol Name
Glyph

Symbol Name
Glyph




aws_profile
U+f52c

ps2
...


bg_jobs
U+f085

read_only
U+f023


exit_status
blank

segment_separator
U+e0b0


git_ahead
U+f55c

ssh
U+f817


git_behind
U+f544

timer
U+fa1e


git_bitbucket
U+f171

venv (and conda)
U+e73c


git_branch
U+e0a0

vimode_cmd
N


git_github
U+f408

vimode_ins
I


git_gitlab
U+f296

working_dir_folder
U+e5fe


git_modified
U+f44d

working_dir_home
U+f015


newline
U+f155

working_dir_separator
U+e0b1


newline_root
U+f52c







As with 
```
TRUELINE_COLORS
```
, any 
```
TRUELINE_SYMBOLS
```
array defined in the bashrc file prior
to sourcing the Trueline script will actually update the array with the default symbols
shown above (thus such array needs to be defined only when overriding some icon or adding
new ones).

### 


Options

Most Trueline settings are controlled with the 3 structures defined above. However
Trueline also defines a series of variables that control some extra options. In particular
we can distinguish between intra-segment and external options. These, along with their
default values, are defined as follows:

#### 


Intra-segment

The next segments have (sub)settings of their own:


- git:



```
TRUELINE_GIT_SHOW_STATUS_NUMBERS=true
```
: boolean variable that determines
whether to show (or not) the actual number of modified files and commits
behind/ahead next to the corresponding modified-behind/ahead status symbol.

- 

```
TRUELINE_GIT_MODIFIED_COLOR='red'
```
: foreground color for symbol and number of
modified files.

- 

```
TRUELINE_GIT_BEHIND_AHEAD_COLOR='purple'
```
: foreground color for symbol and
number of commits behind/ahead.



- user:



```
TRUELINE_USER_ROOT_COLORS=('black' 'red')
```
: root user foreground and
background colors.

- 

```
TRUELINE_USER_SHOW_IP_SSH=false
```
: boolean variable that determines whether to
show the ip address or hostname in a ssh connection.

- 

```
TRUELINE_USER_ALWAYS_SHOW_HOSTNAME=false
```
: boolean variable that determines
whether to always show the ip address or hostname (not just in a ssh connection).

- 

```
TRUELINE_USER_SHORTEN_HOSTNAME=false
```
: boolean variable that determines
whether to display the full hostname (host.domain.com), or the shortened hostname
(host).



- working_dir:



```
TRUELINE_WORKING_DIR_SPACE_BETWEEN_PATH_SEPARATOR=true
```
: boolean variable that
determines whether to add (or not) a space before and after the path separator.

- 

```
TRUELINE_WORKING_DIR_ABBREVIATE_PARENT_DIRS=false
```
: boolean variable that when
set to true shows the full working directory (instead of trimming it). Each parent
directory is shortened to 
```
TRUELINE_WORKING_DIR_ABBREVIATE_PARENT_DIRS_LENGTH
```
.

- 

```
TRUELINE_WORKING_DIR_ABBREVIATE_PARENT_DIRS_LENGTH=1
```
: length of each parent
directory when 
```
TRUELINE_WORKING_DIR_ABBREVIATE_PARENT_DIRS
```
is enabled.





#### 


External


- 

```
TRUELINE_SHOW_VIMODE=false
```
: boolean variable that determines whether or not to show
the current vi mode (if this is set to 
```
true
```
and vi-mode is not already enabled then
Trueline will enabled it; vi-mode must be otherwise enabled separately in your

```
.bashrc
```
via 
```
set -o vi
```
). When set to 
```
true
```
a new segment is shown first (i.e
before any other segment defined in 
```
TRUELINE_SEGMENTS
```
) and it's appearance can be
controlled by means of the following variables:



```
TRUELINE_VIMODE_INS_COLORS_STYLE=('black' 'light_blue' 'bold')
```
: insert mode
segment foreground/background colors and font style.

- 

```
TRUELINE_VIMODE_CMD_COLORS_STYLE=('black' 'green' 'bold')
```
: command mode
segment foreground/background colors and font style.

- 

```
TRUELINE_VIMODE_INS_CURSOR='vert'
```
: insert mode cursor shape (possible
values are 
```
vert
```
, 
```
block
```
and 
```
under
```
).

- 

```
TRUELINE_VIMODE_CMD_CURSOR='block'
```
: command mode cursor shape (possible
values are 
```
vert
```
, 
```
block
```
and 
```
under
```
).





### 
Extensions

New segments can be easily added to the prompt by following this template:

```

```
_trueline_new_segment_name_segment() {
local some_content=$(...)
if [[ -n "$some_content" ]]; then
local fg_color="$1"
local bg_color="$2"
local font_style="$3"
local segment="$(_trueline_separator)"
segment+="$(_trueline_content "$fg_color" "$bg_color" "$font_style" " $some_content ")"
PS1+="$segment"
_trueline_record_colors "$fg_color" "$bg_color" "$font_style"
fi
}

```

```

and then simply including the 
```
new_segment_name
```
in your 
```
TRUELINE_SEGMENTS
```
array.

PRs with complicated segments are welcome!





Get A Weekly Email With Trending Projects For These TopicsNo Spam. Unsubscribe easily at any time. Shell (228,493)  Bash (7,110)  Terminal (4,217)  Prompt (472)  Powerline (153)  Ps1 (127) Related Projects[Shell Bash Projects (5,469)](https://awesomeopensource.com/projects/bash/shell)[Shell Terminal Projects (940)](https://awesomeopensource.com/projects/shell/terminal)[Bash Terminal Projects (439)](https://awesomeopensource.com/projects/bash/terminal)[Shell Bash Terminal Projects (320)](https://awesomeopensource.com/projects/bash/shell/terminal)[Shell Prompt Projects (198)](https://awesomeopensource.com/projects/prompt/shell)[Terminal Prompt Projects (92)](https://awesomeopensource.com/projects/prompt/terminal)[Bash Prompt Projects (90)](https://awesomeopensource.com/projects/bash/prompt)[Shell Powerline Projects (82)](https://awesomeopensource.com/projects/powerline/shell)[Shell Bash Prompt Projects (69)](https://awesomeopensource.com/projects/bash/prompt/shell)[Shell Terminal Prompt Projects (50)](https://awesomeopensource.com/projects/prompt/shell/terminal)[Bash Powerline Projects (37)](https://awesomeopensource.com/projects/bash/powerline)[Bash Terminal Prompt Projects (32)](https://awesomeopensource.com/projects/bash/prompt/terminal)[Shell Bash Terminal Prompt Projects (28)](https://awesomeopensource.com/projects/bash/prompt/shell/terminal)[Prompt Powerline Projects (25)](https://awesomeopensource.com/projects/powerline/prompt)[Shell Bash Powerline Projects (24)](https://awesomeopensource.com/projects/bash/powerline/shell)[Bash Ps1 Projects (23)](https://awesomeopensource.com/projects/bash/ps1)[Shell Ps1 Projects (20)](https://awesomeopensource.com/projects/ps1/shell)[Terminal Powerline Projects (18)](https://awesomeopensource.com/projects/powerline/terminal)[Shell Prompt Powerline Projects (16)](https://awesomeopensource.com/projects/powerline/prompt/shell)[Bash Prompt Powerline Projects (15)](https://awesomeopensource.com/projects/bash/powerline/prompt)[Shell Bash Ps1 Projects (13)](https://awesomeopensource.com/projects/bash/ps1/shell)[Bash Prompt Ps1 Projects (11)](https://awesomeopensource.com/projects/bash/prompt/ps1)[Shell Terminal Powerline Projects (10)](https://awesomeopensource.com/projects/powerline/shell/terminal)[Shell Bash Prompt Powerline Projects (9)](https://awesomeopensource.com/projects/bash/powerline/prompt/shell)[Shell Prompt Ps1 Projects (7)](https://awesomeopensource.com/projects/prompt/ps1/shell)[Bash Terminal Ps1 Projects (7)](https://awesomeopensource.com/projects/bash/ps1/terminal)[Shell Bash Prompt Ps1 Projects (6)](https://awesomeopensource.com/projects/bash/prompt/ps1/shell)[Bash Terminal Prompt Ps1 Projects (6)](https://awesomeopensource.com/projects/bash/prompt/ps1/terminal)[Shell Bash Terminal Prompt Ps1 Projects (4)](https://awesomeopensource.com/projects/bash/prompt/ps1/shell/terminal)[Shell Bash Terminal Ps1 Projects (4)](https://awesomeopensource.com/projects/bash/ps1/shell/terminal)[Advertising 📦 9](https://awesomeopensource.com/categories/advertising)[All Projects](https://awesomeopensource.com/projects)[Application Programming Interfaces 📦 120](https://awesomeopensource.com/categories/application-programming-interfaces)[Applications 📦 181](https://awesomeopensource.com/categories/applications)[Artificial Intelligence 📦 72](https://awesomeopensource.com/categories/artificial-intelligence)[Blockchain 📦 70](https://awesomeopensource.com/categories/blockchain)[Build Tools 📦 111](https://awesomeopensource.com/categories/build-tools)[Cloud Computing 📦 79](https://awesomeopensource.com/categories/cloud-computing)[Code Quality 📦 28](https://awesomeopensource.com/categories/code-quality)[Collaboration 📦 30](https://awesomeopensource.com/categories/collaboration)[Command Line Interface 📦 48](https://awesomeopensource.com/categories/command-line-interface)[Community 📦 81](https://awesomeopensource.com/categories/community)[Companies 📦 60](https://awesomeopensource.com/categories/companies)[Compilers 📦 60](https://awesomeopensource.com/categories/compilers)[Computer Science 📦 74](https://awesomeopensource.com/categories/computer-science)[Configuration Management 📦 39](https://awesomeopensource.com/categories/configuration-management)[Content Management 📦 167](https://awesomeopensource.com/categories/content-management)[Control Flow 📦 197](https://awesomeopensource.com/categories/control-flow)[Data Formats 📦 77](https://awesomeopensource.com/categories/data-formats)[Data Processing 📦 266](https://awesomeopensource.com/categories/data-processing)[Data Storage 📦 132](https://awesomeopensource.com/categories/data-storage)[Economics 📦 60](https://awesomeopensource.com/categories/economics)[Frameworks 📦 198](https://awesomeopensource.com/categories/frameworks)[Games 📦 122](https://awesomeopensource.com/categories/games)[Graphics 📦 103](https://awesomeopensource.com/categories/graphics)[Hardware 📦 148](https://awesomeopensource.com/categories/hardware)[Integrated Development Environments 📦 47](https://awesomeopensource.com/categories/integrated-development-environments)[Learning Resources 📦 147](https://awesomeopensource.com/categories/learning-resources)[Legal 📦 28](https://awesomeopensource.com/categories/legal)[Libraries 📦 119](https://awesomeopensource.com/categories/libraries)[Lists Of Projects 📦 21](https://awesomeopensource.com/categories/lists-of-projects)[Machine Learning 📦 336](https://awesomeopensource.com/categories/machine-learning)[Mapping 📦 61](https://awesomeopensource.com/categories/mapping)[Marketing 📦 15](https://awesomeopensource.com/categories/marketing)[Mathematics 📦 55](https://awesomeopensource.com/categories/mathematics)[Media 📦 228](https://awesomeopensource.com/categories/media)[Messaging 📦 97](https://awesomeopensource.com/categories/messaging)[Networking 📦 304](https://awesomeopensource.com/categories/networking)[Operating Systems 📦 84](https://awesomeopensource.com/categories/operating-systems)[Operations 📦 120](https://awesomeopensource.com/categories/operations)[Package Managers 📦 52](https://awesomeopensource.com/categories/package-managers)[Programming Languages 📦 229](https://awesomeopensource.com/categories/programming-languages)[Runtime Environments 📦 96](https://awesomeopensource.com/categories/runtime-environments)[Science 📦 42](https://awesomeopensource.com/categories/science)[Security 📦 375](https://awesomeopensource.com/categories/security)[Social Media 📦 26](https://awesomeopensource.com/categories/social-media)[Software Architecture 📦 70](https://awesomeopensource.com/categories/software-architecture)[Software Development 📦 68](https://awesomeopensource.com/categories/software-development)[Software Performance 📦 57](https://awesomeopensource.com/categories/software-performance)[Software Quality 📦 127](https://awesomeopensource.com/categories/software-quality)[Text Editors 📦 45](https://awesomeopensource.com/categories/text-editors)[Text Processing 📦 131](https://awesomeopensource.com/categories/text-processing)[User Interface 📦 310](https://awesomeopensource.com/categories/user-interface)[User Interface Components 📦 465](https://awesomeopensource.com/categories/user-interface-components)[Version Control 📦 29](https://awesomeopensource.com/categories/version-control)[Virtualization 📦 68](https://awesomeopensource.com/categories/virtualization)[Web Browsers 📦 38](https://awesomeopensource.com/categories/web-browsers)[Web Servers 📦 25](https://awesomeopensource.com/categories/web-servers)[Web User Interface 📦 194](https://awesomeopensource.com/categories/web-user-interface)[Privacy policy](https://awesomeopensource.com/pages/privacy)"Trueline" and other potentially trademarked words, copyrighted images and copyrighted readme contents likely belong to the legal entity who owns the "[Petobens](https://github.com/petobens)" organization. Awesome Open Source is not affiliated with the legal entity who owns the "[Petobens](https://github.com/petobens)" organization.
All non readme contents or Github based topics or project metadata copyright Awesome Open Source 2018-2022