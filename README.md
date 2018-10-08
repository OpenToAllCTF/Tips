# Tips
Useful tips by OTA CTF members. PRs welcome!

## Assembly

* Beginner's guide: [Learning to read \[AT&T\] assembly language](http://patshaughnessy.net/2016/11/26/learning-to-read-x86-assembly-language)
* Big PDF: [The Art of Assembly](http://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/aoaTOC2.pdf)
* Quickly see what assembly different compilers generate: [Compiler Explorer](https://godbolt.org/)
* Quickly disassemble raw bytes: [ODA](https://www.onlinedisassembler.com/odaweb/)
* Quickly assemble x86: [Defuse assembler](https://defuse.ca/online-x86-assembler.htm)

## IDA
* Common hotkeys:

  | Key              | Effect                          |
  |------------------|---------------------------------|
  | `Esc`            | Go back                         |
  | `Ctrl-Enter`     | Go forward                      |
  | `H`, `Q`, `B`    | View as decimal, hex, or binary |
  | `N`/`U`          | Name/Undefine symbol            |
  | `D`, `C`, `P`    | Convert to data, code, function |
* Learn to create and use structs.
* IDAPython is very powerful and worth learning.
* Use FLIRT whenever you see a static binary. You can save a ton of normally wasted time reverse engineering common functions.

## Debugging

### GDB

* Don't suffer through vanilla GDB. Use something like [GEF](https://github.com/hugsy/gef), [PEDA](https://github.com/longld/peda), or [Voltron](https://github.com/snare/voltron).
* Learn these!
  * `command <bp#>` - Run commands when a bp is hit.
  * `ignore <bp#> <count>` - Ignore the next _count_ occurrences of _bp_.
  * `watch|rwatch|awatch <addr> [thread <thread>] [mask <mask>]` - Break when specified address is written to, read from, or either.
  * `hbreak <addr>` - Set a hardware breakpoint.
  * `tbreak <addr>` - Set a temporary breakpoint that disappears once hit.
  * `advance <addr>` - Continue until the specified address.
  * `catch syscall [syscall]` - Break on syscall (all or the specified).
  * `catch signal [signal]` - Break on signal (all or the specified).
  * `bt` - View stack frames (backtrace).
  * `up`/`down` - Move up or down to a different stack frame.
  * `set follow-fork-mode <child|parent>` - Tell gdb to either trace the parent or 'move' to the child on `fork`.
  * `set follow-exec-mode <same|new>` - Tell gdb to either trace the original target or 'move' to the new process on `exec*`.

## Shell-fu
* `file` - Try to determine what type of file you have.
* `strace` - See which syscalls an executable executes.
* `ltrace` - See which library calls an executable executes.
* `ldd` - See which dynamic libraries an executable loads.
* `nm` - Dump a binary's symbols
* Learn to use pipes and [redirection](http://wiki.bash-hackers.org/howto/redirection_tutorial)! When you want to script input, this is very handy, and doing it incorrectly can lead to successful payloads being unusable (e.g. spawning a shell whose _stdin_ is not connected to your terminal).
* To pipe output to an application, but regain access to _stdin_ after, use a subshell:
```bash
(python3 -c "print('AAAApayload')"; cat -) | nc pwn.me.org 5555
```
*  `cd -` - Go back to your last working directory.
* `!!` - Repeats your last command. Can also be used as a parameter.

```bash
cd /root
bash: cd: /root: Permission denied
sudo !!
```

* Readline shortcuts are _super_ handy.

  | Key      | Effect                             |
  |----------|------------------------------------|
  | `Ctrl-E` | Go to end of line                  |
  | `Ctrl-A` | Go to start of line                |
  | `Ctrl-L` | Clear terminal                     |
  | `Ctrl-U` | Delete everything left of cursor   |
  | `Ctrl-K` | Delete everything right of cursor  |
  | `Ctrl-W` | Delete word left                   |
  | `Ctrl-Y` | Paste last deleted text            |
  | `Ctrl-F` | Move cursor forward one char       |
  | `Ctrl-B` | Move cursor back one char          |
  | `Ctrl-P` | Move back one line in history      |
  | `Ctrl-N` | Move forward one line in history   |
  | `Ctrl-R` | Search bash history (start typing) |
  | `Ctrl-G` | Cancel history search              |
## Crypto

[Quipquip](https://quipqiup.com/) : Online tool that will help you solve almost all subsituition cipher

[Decode.fr](https://www.dcode.fr/) : It contains ton of old school cipher

[CyberChef](https://gchq.github.io/CyberChef/) : Try magic mode, it's real MAGIC!

## Hacking channel/stream/podcast :
* Gynvael : [youtube](https://www.youtube.com/user/GynvaelEN/featured) - A channel about computer, security,ctf, etc... Gynvael is GOD
* Liveoverflow : [youtube](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w) - This guy actually hard working, smart and he explain his idea by image, animation makes thing easy to understand
* Socratica : [youtube](https://www.youtube.com/user/SocraticaStudios) - It's not about security (directly), but it's good channel about Math, you CANT escape from MATH when you do ANYTHING with COMPUTER. I learn that the hard way, dont be like me.
* Ricardo Narvaja : [youtube](https://www.youtube.com/channel/UCDeWwrp2LUWkDSymrmnfKDQ) - If you are old school cracker, you MUST know this guy. Brilliant. He also have IDA tutorial that teach me a lot about IDA, patching, unpacking,...etc. It orginally written in Spanish (i guess so) but is translated to English [drive](https://drive.google.com/drive/u/0/folders/0B13TW0I0f8O2ckd2T0lsbXRoYmc) 
* SecurityTube : [youtube](https://www.youtube.com/user/TheSecurityTube) - Good educational resources about Security.
