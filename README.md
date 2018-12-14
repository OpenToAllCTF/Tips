# Tips
Useful tips by OTA CTF members. PRs welcome!

## Assembly

* Beginner's guide: [Learning to read \[AT&T\] assembly language](http://patshaughnessy.net/2016/11/26/learning-to-read-x86-assembly-language)
* Big PDF: [The Art of Assembly](http://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/aoaTOC2.pdf)
* Quickly see what assembly different compilers generate: [Compiler Explorer](https://godbolt.org/)
* Quickly disassemble raw bytes: [ODA](https://www.onlinedisassembler.com/odaweb/)
* Quickly assemble x86: [Defuse assembler](https://defuse.ca/online-x86-assembler.htm)

## Binary Exploitation Technique

* [Modern Binary Exploitation](https://github.com/RPISEC/MBE)
* [Basic Return Oriented Programming](http://codearcana.com/posts/2013/05/28/introduction-to-return-oriented-programming-rop.html)
* [Blind Return Oriented Programming](http://www.scs.stanford.edu/brop/)
* [Signature Return Oriented Programming](https://www.cs.vu.nl/~herbertb/papers/srop_sp14.pdf)
* [ROP Practice Problems](https://ropemporium.com/)
* [Heap Overflow](https://github.com/shellphish/how2heap)
* [Pwntools Beginner Tutorial](http://www.auxy.xyz/tutorial/2018/09/01/Pwntools-Step-By-Step.html)
* [File Stream Oriented Programming](https://www.slideshare.net/AngelBoy1/play-with-file-structure-yet-another-binary-exploit-technique)

## IDA
* Common hotkeys:

  | Key              | Effect                          |
  |------------------|---------------------------------|
  | `Esc`            | Go back                         |
  | `Ctrl-Enter`     | Go forward                      |
  | `H`, `Q`, `B`    | View as decimal, hex, or binary |
  | `N`/`U`          | Name/Undefine symbol            |
  | `D`, `C`, `P`    | Convert to data, code, function |
  | `Ctrl-w`         | Save                            |
* Learn to create and use structs.
* IDAPython is very powerful and worth learning.
* Use FLIRT whenever you see a static binary. You can save a ton of normally wasted time reverse engineering common functions.
* Code coverage and tracing analysis is a useful technique to assist with reverse engineering. IDA has built in coverage and trace highlighting capabilities features. [Lighthouse](https://github.com/gaasedelen/lighthouse) is also a great plugin for coverage analysis.
* [Keypatch](http://www.keystone-engine.org/keypatch) is a useful plugin that offers extra features compared to the built-in assembler

## Debugging

### GDB

* Don't suffer through vanilla GDB. Use something like [GEF](https://github.com/hugsy/gef), [PEDA](https://github.com/longld/peda), or [Voltron](https://github.com/snare/voltron).
* You can also combine [PEDA](https://github.com/longld/peda) with [Pwngdb](https://github.com/scwuaptx/Pwngdb), which is a powerful add-on that supports advanced heap exploitation and FILE stream oriented exploitation features.
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

### Redressing a Stripped Libc
* Often times when we do pwnables, we are given the pwnable along with a stripped version of the libc that the pwnable is using on the remote server. If we want an easier time debugging with the provided libc preloaded, here are some steps we can take to add symbols back to the stripped libc. (dependencies: [eu-unstrip](https://helpmanual.io/help/eu-unstrip/)) 
  1. run `strings <stripped-libc> | grep glibc` to determine the libc version
  1. download the associated debug symbol file (eg.[https://launchpad.net/ubuntu/xenial/amd64/libc6-dbg/2.23-0ubuntu5](https://launchpad.net/ubuntu/xenial/amd64/libc6-dbg/2.23-0ubuntu5))
  1. merge stripped libc file with debug symbol  file using `eu-unstrip` like so: `eu-unstrip <stripped-libc> <symbol-file>`
  1. now `<symbol-file>` will be your newly redressed libc w/symbols!

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

[kt.gy tools](https://kt.gy/tools.html) : Fast online tool to decode your string 

## Jail Challenges

### Python Jails
[Gynvael Python Jail tips](https://gynvael.coldwind.pl/n/python_sandbox_escape)

#### Useful functions
* eval() / exec() / compile(), execute any python code
* dir() / type()
* globals() / locals() / vars(), finding useful variables
* getattr() / setattr(), useful when you need to call object.banned(). You can do getattr(object, "ban"+"ned") or something along the lines

#### Interesting Behaviour
* "A""B" == "AB", useful when `+` is blocked

### Bash Jails

#### Reading files
* Sometimes `cat` is filtered or banned, these are some alternatives
* fold
* nl (numbered)
* head (head portion of file)
* tail (tail portion of file)

## _hooks
In libc, there are `*_hook` function pointers that are called that are writeable:

```bash
$ less ./db/local-acd0f91e833f06b2a822be84579f70edf4e80050.symbols | grep _hook
__free_hook 001b18b0
argp_program_version_hook 001b3794
_dl_open_hook 001b35d4
__malloc_hook 001b0768
__realloc_hook 001b0764
__malloc_initialize_hook 001b18b4
__after_morecore_hook 001b18ac
__memalign_hook 001b0760
```
By default, these pointers are NULL. These function pointers are only called IF they are not NULL:

```C
void
__libc_free(void* mem)
{
  mstate ar_ptr;
  mchunkptr p;                          /* chunk corresponding to mem */

  void (*hook) (void *, const void *)
    = force_reg (__free_hook);
  if (__builtin_expect (hook != NULL, 0)) {
    (*hook)(mem, RETURN_ADDRESS (0));
    return;
  }
```

If you can overwrite one of these pointers, you can control RIP the next time the associated libc function is called!
Useful if FULL RELRO is enabled/the GOT is read-only and we have a write-what-where!

### Protips
* `printf()` actually calls `malloc()` if printing anything out with a width > 65535-32!
* any memory corruption error you trigger will call `alloca()`/`__malloc_hook`

## Null Termination
#### Do NOT read past first null byte
* strcpy()
* strncpy()

#### Do read past first null byte
* read()
* gets()
* fgets()
* memcpy()
* scanf()

#### Does copy the terminating nullbyte from src to dst
* strcpy()

## Hacking channel/stream/podcast/blog :
* Gynvael : [youtube](https://www.youtube.com/user/GynvaelEN/featured) - A channel about computer, security, ctf, etc... Gynvael is GOD
* LiveOverflow : [youtube](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w) - This guy is actually hard working, smart and he explains his idea using animations making things easy to understand
* Socratica : [youtube](https://www.youtube.com/user/SocraticaStudios) - It's not about security (directly), but it's a good channel for Math, you CAN'T escape MATH if you are doing ANYTHING with COMPUTERS. I learnt that the hard way, don't be like me.
* Ricardo Narvaja : [youtube](https://www.youtube.com/channel/UCDeWwrp2LUWkDSymrmnfKDQ) - If you are an old school cracker, you WOULD know this guy. HE is Brilliant. He also has IDA tutorials that taught me a lot about IDA, patching, unpacking...etc. It is orginally in Spanish (i guess so) but the English translated version is available here [drive](https://drive.google.com/drive/u/0/folders/0B13TW0I0f8O2ckd2T0lsbXRoYmc) 
* SecurityTube : [youtube](https://www.youtube.com/user/TheSecurityTube) - Good educational resources about Security.
* Murmus CTF: [youtube](https://www.youtube.com/channel/UCUB9vOGEUpw7IKJRoR4PK-A) - CTF player who livestreams walkthroughs from various ctfs.
* 360 Core Security : [link](http://blogs.360.cn/post/) a blog all about security research, 0day... of 360 Core Security Team. Very interesting and advanced.
## Stories
* Stuxnet : [wired](https://www.wired.com/2011/07/how-digital-detectives-deciphered-stuxnet/) - A story about Stuxnet, the malware that wrecked havoc in Iran's nuclear power plant
* Mirai : [wired](https://www.wired.com/story/mirai-botnet-minecraft-scam-brought-down-the-internet/) - A story about Mirai, the IOT botnet that brought down the Internet
* Edward Snowden : [wired](https://www.wired.com/2014/08/edward-snowden/) - The untold story of Edward Snowden
* SilkRoad [wired](https://www.wired.com/2015/04/silk-road-1/ https://www.wired.com/2015/04/silk-road-2/) - A story about the rise and fall of Silk Road, an online drug marketplace by Ross Ulbricht(Dread Pirate Roberts)
* SilkRoad [wired](https://www.wired.com/story/russian-hackers-attack-ukraine/) - A story about the Russian attacks on critical infrastructure of Ukraine
* Finfisher hack [pastebin](https://pastebin.com/cRYvK4jb) - A story by the person claiming to be Phineas Fisher who hacked a spyware company, pretty good read in my opinion
* HackingTeam hack [pastebin](https://pastebin.com/0SNSvyjJ) - A story by the person claiming to be Phineas Fisher who hacked the Italian company HackingTeam and leaked their data, again a very good read
* Spanish Police hack [vimeo](https://vimeo.com/167411059) - A video by Phineas Fisher showing how he hacked the Spanish Police because of their human rights violation
