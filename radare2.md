# Radare2 Cheatsheet

```bash
# Getting radare2
git clone https://github.com/radare/radare2.git
cd radare2
./sys/install.sh
# make uninstall
# make purge
```

## Basics
> Always use a secure environment before starting unknown binaries

* Start the binary with radare `r2 sth.bin`
* Use `X?` at any time on the cli to get info about the commands, where X is an command, or nothing for general info
  
### Analysis
> Check `a?`, and `aa?` for more

* `a` - analysis info
* `aa` - analyze all (check `aa?` for more analysis)
* `aaa` - Even more analysis

### Flags

After the analysis, flags are associated to interesting offsets (e.g: Strings). Flags can be grouped into ‘flag spaces’. A flag space is a namespace for flags of similar characteristics or type. 
* `fs` - list flag-spaces
* `fs <flagspace>` - select it
* `f` - print the flags in it

> Tip: use `fs *` to return to root fs

### Strings / references

* `iz` – List strings in data sections
* `izz` – Search for Strings in the whole binary
* `axt` stands for analyze x-refs to
* `axt @@ str.*`
  * `@@` - foreach
  * `str.*` - object in str.
  * `axt` - analyze X-refs

### Seeking

> See more with `s?`

* `afl` - analyze function list
* `s main` - change current offset to main function

### Disassembling 
Here it is good to have some assembly knowledge in order to be able to come up with 'pseudo-code' for what is happening.

* `pdf` - Print Disassemble Function at current offset
* `pdf @ sym.foo` -  pdf at offset of sym.foo

### Visual Modes

#### `V` - visual mode

Shortcuts:
* `p/P` - cycle between views
* `q` - quit
* `x/X` - list refs to current offset
* `:command` - execute cmds inside visual mode
* `;<comment>` / `;-` / `;!` - comment add / remove / add with default editor
* `m<key>` / `'<key>` - mark / goto an interesting offset

#### `VV` Graph Mode
In this mode, letters will appear next 

* `o<letter>` - jump to function highlighted with the letter
* `r` - toggle jumphints / leahints

#### Shell commands
* `!cmd` - execute any shell command from inside r2 shell

#### Running program

* `ood` - open debugging session
* `dc` - debugging continue