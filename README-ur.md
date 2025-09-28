🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [polski](README-pl.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md) ∙ [Urdu](README-ur.md)*
# The Art of Command Line  

Note: Mein isay revise karne ka plan kar raha hoon aur ek naye co-author ki talaash mein hoon jo isay zyada comprehensive guide banane mein madad kare. Ye bohot popular hai, lekin ye aur bhi broad aur thoda deep ho sakta hai. Agar tum likhne ka shauq rakhte ho aur is material mein expert level ke qareeb ho aur madad karne ke liye tayar ho, to mujhe note bhejo josh (0x40) holloway.com par. –[jlevy](https://github.com/jlevy), [Holloway](https://www.holloway.com). Shukriya!

- [Meta](#meta)
- [Basics](#basics)
- [Rozana Istemaal](#everyday-use)
- [Files aur Data ko Process karna](#processing-files-and-data)
- [System debugging](#system-debugging)
- [One-liners](#one-liners)
- [Obscure lekin Kaam ke](#obscure-but-useful)
- [Sirf macOS ke liye](#macos-only)
- [Sirf Windows ke liye](#windows-only)
- [Mazeed Resources](#more-resources)
- [Disclaimer](#disclaimer)



![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Command line par fluency ek skill hai jo aksar nazarandaz ki jati hai ya phir ise pur-asrar (arcane) samjha jata hai, lekin ye aapki flexibility aur productivity ko ek engineer ke tor par behtareen banati hai — dono obvious aur subtle tareeqon se. Ye ek notes aur tips ka intikhab hai jo command-line use karte waqt humne faida mand paaye hain jab hum Linux par kaam kar rahe thay. Kuch tips bohot basic hain, aur kuch bohot specific, advanced, ya phir ajeeb (obscure) hain. Ye page lamba nahi hai, lekin agar aap yahan likhi hui sari cheezon ko use aur yaad rakh saktay hain, to aap bohot kuch jaante hain.

Ye kaam [bohot se authors aur translators](./AUTHORS.md) ka nateeja hai.
Iska kuch hissa [asal mein](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands) [Quora par](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix) [appear hua tha](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know), lekin baad mein isay GitHub par shift kar diya gaya, jahan asal author se zyada talented logon ne is mein bohot behtareen sudhaar kiye.
[**Barah-e-karam sawal bhejein**](https://airtable.com/shrzMhx00YiIVAWJg) agar aapka koi sawal command line se related hai. [**Barah-e-karam contribute karein**](/CONTRIBUTING.md) agar aapko koi ghalti nazar aaye ya koi cheez aur behtar ho sakti ho!

## Meta  

Scope:  

- Ye guide dono beginners aur experienced users ke liye hai. Goals hain *breadth* (har cheez jo important hai), *specificity* (sabse common case ke concrete examples dena), aur *brevity* (aisi cheezon se bachna jo essential nahi hain ya aisi digressions jo aap easily aur jaga check kar saktay ho). Har tip essential hai kisi na kisi situation mein ya bohot zyada time save karti hai alternatives ke muqable mein.  
- Ye likhi gayi hai Linux ke liye, siwaye un sections ke jo "[macOS only](#macos-only)" aur "[Windows only](#windows-only)" hain. Bohot se doosri cheezen apply hoti hain ya install ki ja sakti hain doosray Unices ya macOS (ya hatta ke Cygwin) par.  
- Focus hai interactive Bash par, lekin bohot se tips doosray shells aur general Bash scripting par bhi apply hoti hain.  
- Isme shamil hain dono "standard" Unix commands aur wo jo require karte hain special package installs – jab tak wo itne important ho ke unko include karna zaroori ho.  

Notes:  

- Isko ek page tak rakhne ke liye, content implicitly include kiya gaya hai by reference. Aap itne smart hain ke detail aur jaga dekh lenge jab aapko idea ya command pata chal jaye jo Google karni hai. Use `apt`, `yum`, `dnf`, `pacman`, `pip` ya `brew` (jahan appropriate ho) naye programs install karne ke liye.  
- Use [Explainshell](http://explainshell.com/) taake aapko helpful breakdown milay ke commands, options, pipes etc. kya karte hain.  

## Basics  

- Basic Bash seekho. Asal mein, `man bash` type karo aur kam az kam pura skim karo; ye follow karna kaafi easy hai aur zyada lamba bhi nahi. Alternate shells achhi ho sakti hain, lekin Bash powerful hai aur hamesha available hoti hai (sirf zsh, fish, etc. seekhna, jo tempting lagta hai apne laptop par, bohot si situations mein restrict karta hai, jaise ke jab aap existing servers use kar rahe ho).  

- Kam az kam ek text-based editor achhi tarah seekho. `nano` editor sabse simple editors mein se ek hai basic editing ke liye (open karna, edit karna, save karna, search karna). Lekin, ek power user ke liye text terminal mein Vim (`vi`) ka koi substitute nahi hai – ye mushkil seekhnay wala lekin purana, fast aur full-featured editor hai. Bohot se log classic Emacs bhi use karte hain, khaaskar bade editing tasks ke liye. (Of course, koi bhi modern software developer jo ek extensive project par kaam kar raha hai, sirf pure text-based editor use karne ke chances bohot kam hain; usay modern graphical IDEs aur tools se bhi familiar hona chahiye.)  

- Documentation dhoondhna:  
  - Ye jaanno ke official documentation `man` se kaise parhte hain (agar inquisitive ho, to `man man` section numbers list karta hai, misal ke taur par 1 hai "regular" commands ke liye, 5 hai files/conventions ke liye, aur 8 hai administration ke liye). Man pages ko `apropos` ke zariye dhoondo.  
  - Ye jaanno ke kuch commands executables nahi hote, balkay Bash builtins hote hain, aur tum un par madad `help` aur `help -d` se le sakte ho. Tum jaan sakte ho ke koi command ek executable hai, shell builtin hai ya alias hai `type command` use karke.  
  - `curl cheat.sh/command` tumhain ek chhoti si "cheat sheet" dega jisme common examples honge ke ek shell command kaise use hota hai.  

- Output aur input ki redirection seekho `>` aur `<` ke sath, aur pipes seekho `|` ke sath. Jaanno ke `>` output file ko overwrite karta hai aur `>>` append karta hai. Stdout aur stderr ke bare mein seekho.  

- File glob expansion seekho `*` ke sath (aur shayad `?` aur `[`...`]`), aur quoting, aur double `"` aur single `'` quotes ka farq samjho. (Neeche variable expansion par aur dekho.)  

- Bash job management se familiar ho jao: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.  

- `ssh` seekho, aur passwordless authentication ke basics, `ssh-agent`, `ssh-add`, etc. ke zariye.  

- Basic file management: `ls` aur `ls -l` (khaaskar, seekho ke `ls -l` ke har column ka matlab kya hai), `less`, `head`, `tail` aur `tail -f` (ya aur behtareen, `less +F`), `ln` aur `ln -s` (hard aur soft links ke farq aur advantages seekho), `chown`, `chmod`, `du` (disk usage ka ek quick summary ke liye: `du -hs *`). Filesystem management ke liye, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Seekho inode kya hota hai (`ls -i` ya `df -i`).  

- Basic network management: `ip` ya `ifconfig`, `dig`, `traceroute`, `route`.  

- Ek version control management system seekho aur use karo, jaise `git`.  

- Regular expressions achhi tarah seekho, aur `grep`/`egrep` ke various flags jaanno. `-i`, `-o`, `-v`, `-A`, `-B`, aur `-C` options jaanna laazmi hai.  

- `apt-get`, `yum`, `dnf` ya `pacman` (distro ke mutabiq) use karna seekho packages dhoondhne aur install karne ke liye. Aur ensure karo ke tumhare paas `pip` ho Python-based command-line tools install karne ke liye (neeche kuch aise tools hain jo `pip` se install karna sabse easy hai).  

## Rozana Istemaal (Everyday use)

- Bash mein, **Tab** use karo arguments ko complete karne ke liye ya available commands list karne ke liye, aur **ctrl-r** use karo command history mein search karne ke liye (dabane ke baad, type karo search karne ke liye, **ctrl-r** baar baar dabao aur zyada matches cycle karo, **Enter** dabao taake found command execute ho jaye, ya right arrow dabao taake result current line mein aa jaye editing ke liye).  

- Bash mein, **ctrl-w** use karo last word delete karne ke liye, aur **ctrl-u** use karo cursor se start of line tak ka content delete karne ke liye. **alt-b** aur **alt-f** use karo word ke hisaab se move karne ke liye, **ctrl-a** use karo cursor ko line ke shuruat mein le jane ke liye, **ctrl-e** use karo cursor ko line ke end mein le jane ke liye, **ctrl-k** use karo line ke end tak delete karne ke liye, **ctrl-l** use karo screen clear karne ke liye. Sab default keybindings Bash mein dekhne ke liye `man readline` use karo. Bohot zyada hain. Misal ke taur par, **alt-.** previous arguments cycle karta hai, aur **alt-*** ek glob expand karta hai.  

- Agar tumhein vi-style key-bindings pasand hain, to `set -o vi` use karo (aur `set -o emacs` use karo wapas karne ke liye).  

- Lambi commands edit karne ke liye, apna editor set karne ke baad (misal ke taur par `export EDITOR=vim`), **ctrl-x** **ctrl-e** current command ko ek editor mein open karega multi-line editing ke liye. Ya vi style mein, **escape-v**.  

- Recent commands dekhne ke liye `history` use karo. Saath mein `!n` lagao (jahan `n` command number hai) taake usay dobara execute kar sako. Bohot abbreviations bhi hain jo tum use kar sakte ho, sabse useful shayad `!$` hai last argument ke liye aur `!!` hai last command ke liye (man page mein "HISTORY EXPANSION" dekho). Lekin, inhein aksar asaani se replace kiya ja sakta hai **ctrl-r** aur **alt-.** se.  

- Apne home directory mein jaane ke liye `cd` use karo. Home directory ke relative files access karne ke liye `~` prefix use karo (misal: `~/.bashrc`). `sh` scripts mein home directory refer karne ke liye `$HOME` use karo.  

- Previous working directory mein wapas jaane ke liye: `cd -`.  

- Agar tum aadhi command type kar chuke ho aur beech mein apna irada badal lo, to **alt-#** dabao taake shuru mein `#` add ho jaye aur wo ek comment ban kar enter ho jaye (ya use karo **ctrl-a**, **#**, **enter**). Phir tum usko baad mein command history ke zariye wapas la sakte ho.  

- `xargs` (ya `parallel`) use karo. Ye bohot powerful hai. Dhyaan rahe tum control kar sakte ho kitne items ek line per execute hon (`-L`) aur parallelism (`-P`). Agar sure nahi ho ke ye sahi kaam karega, pehle `xargs echo` use karo. Saath hi, `-I{}` bhi handy hai. Examples:  
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```
- `pstree -p` ek helpful display hai process tree ka.  

- `pgrep` aur `pkill` use karo processes ko name ke zariye dhoondhne ya signal bhejne ke liye (`-f` helpful hai).  

- Ye jaanno ke tum processes ko kaunse signals bhej sakte ho. Misal ke taur par, ek process suspend karne ke liye `kill -STOP [pid]` use karo. Puri list ke liye, `man 7 signal` dekho.  

- Agar tum chahte ho ke ek background process hamesha ke liye chalta rahe, to `nohup` ya `disown` use karo.  

- Check karo kaunse processes listening hain `netstat -lntp` ya `ss -plat` se (TCP ke liye; UDP ke liye `-u` add karo) ya `lsof -iTCP -sTCP:LISTEN -P -n` se (jo macOS par bhi kaam karta hai).  

- Open sockets aur files ke liye `lsof` aur `fuser` bhi dekho.  

- System kitne waqt se chal raha hai ye jaannay ke liye `uptime` ya `w` use karo.  

- `alias` use karo commonly used commands ke shortcuts banane ke liye. Misal ke taur par, `alias ll='ls -latr'` ek naya alias `ll` create karta hai.  

- Apne commonly used aliases, shell settings aur functions `~/.bashrc` mein save karo, aur [arrange karo taake login shells usay source karein](http://superuser.com/a/183980/7106). Isse tumhara setup tumhari sabhi shell sessions mein available hoga.  

- Environment variables ke settings aur wo commands jo login par execute honi chahiyein, unhein `~/.bash_profile` mein rakho. Alag configuration chahiye hogi un shells ke liye jo graphical environment logins aur `cron` jobs se launch hoti hain.  

- Apne configuration files (misal: `.bashrc` aur `.bash_profile`) ko various computers ke darmiyan Git se synchronize karo.  

- Ye samjho ke jab variables aur filenames mein whitespace ho to ehtiyaat ki zarurat hoti hai. Apne Bash variables ko quotes mein rakho, misal: `"$FOO"`. `-0` ya `-print0` options ko prefer karo taake null characters filenames ko delimit karein, misal: `locate -0 pattern | xargs -0 ls -al` ya `find / -print0 -type d | xargs -0 ls -al`. Filenames jisme whitespace ho unpar iterate karne ke liye ek for loop mein, apna IFS sirf newline par set karo: `IFS=$'\n'`.  

- Bash scripts mein, debugging output ke liye `set -x` use karo (ya variant `set -v`, jo raw input log karta hai, including unexpanded variables aur comments). Strict modes use karo jab tak koi strong reason na ho use na karne ka: `set -e` use karo taake errors (nonzero exit code) par abort ho jaye. `set -u` use karo unset variable usages detect karne ke liye. `set -o pipefail` bhi consider karo, taake pipes ke andar errors par bhi abort ho jaye (lekin agar ye use karte ho to aur detail parh lo, kyunki ye topic thoda subtle hai). Zyada involved scripts ke liye, `trap` use karo EXIT ya ERR par. Ek useful habit ye hai ke script ko aise shuru karo, jo common errors detect aur abort kar de aur ek message print kare:  
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Bash scripts mein, subshells (jo parentheses `()` ke sath likhe jate hain) ek convenient tareeqa hai commands ko group karne ka. Ek common misaal hai temporary taur par ek different working directory mein move karna, misal ke taur par:  

```bash
      # current dir mein kuch karo
      (cd /some/other/dir && other-command)
      # original dir mein wapas continue karo
```

- Bash mein, note karo ke variables expand karne ke bohot tareeqe hain. Variable exist karta hai check karna: `${name:?error message}`. Misal ke taur par, agar ek Bash script ko ek single argument chahiye, to bas likho `input_file=${1:?usage: $0 input_file}`. Agar koi variable khali ho to ek default value use karna: `${name:-default}`. Agar tum previous example mein ek additional (optional) parameter add karna chaho, to aisa likho `output_file=${2:-logfile}`. Agar `$2` omit ho jaye aur khali ho, to `output_file` set ho jayega `logfile`. Arithmetic expansion: `i=$(( (i + 1) % 5 ))`. Sequences: `{1..10}`. Strings trim karna: `${var%suffix}` aur `${var#prefix}`. Misal ke taur par agar `var=foo.pdf`, to `echo ${var%.pdf}.txt` print karega `foo.txt`.  

- Brace expansion `{`...`}` use karke tumhe bar bar similar text re-type karna nahi padega aur combinations automate ho jate hain. Ye helpful hai misalon mein jaise: `mv foo.{txt,pdf} some-dir` (jo dono files move karta hai), `cp somefile{,.bak}` (jo expand hota hai `cp somefile somefile.bak` mein), ya `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (jo saari possible combinations expand karta hai aur ek directory tree create karta hai). Brace expansion sabse pehle hoti hai, kisi aur expansion se pehle.  

- Expansions ka order hai: pehle brace expansion; phir tilde expansion, parameter aur variable expansion, arithmetic expansion, aur command substitution (ye left-to-right hoti hai); phir word splitting; aur phir filename expansion. (Misal ke taur par, ek range `{1..20}` variables ke sath `{$a..$b}` likh ke nahi banayi ja sakti. Iske liye `seq` ya ek `for` loop use karo, jaise: `seq $a $b` ya `for((i=a; i<=b; i++)); do ... ; done`.)  

- Kisi command ka output ek file ki tarah treat kiya ja sakta hai `<(some command)` ke zariye (isko process substitution kehte hain). Misal ke taur par, local `/etc/hosts` ko ek remote ke sath compare karo:  
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Jab tum scripts likh rahe ho to tum chaho ge ke apna sara code curly braces ke andar rakho. Agar closing brace missing ho, to tumhari script execute nahi hogi syntax error ki wajah se. Ye sense banata hai jab tumhari script web se download hone wali ho, kyunke ye partially downloaded scripts ko execute hone se rokta hai:  

```bash
{
      # Tumhara code yahan
}
```

- Ek "here document" allow karta hai [redirection of multiple lines of input](https://www.tldp.org/LDP/abs/html/here-docs.html) jaise ke file se aa rahi ho:  
```bash 
cat <<EOF
input
on multiple lines
EOF
```

- Bash mein, standard output aur standard error dono ko redirect karo is tarah: `some-command >logfile 2>&1` ya `some-command &>logfile`. Aksar, ensure karne ke liye ke ek command open file handle na chhod de standard input ka, jo ke us terminal se tied hota hai jisme tum ho, ye bhi achhi practice hai ke `</dev/null` add kar do.  

- `man ascii` use karo ek achhi ASCII table ke liye, jisme hex aur decimal values hoti hain. General encoding info ke liye, `man unicode`, `man utf-8`, aur `man latin1` madadgar hain.  

- `screen` ya [`tmux`](https://tmux.github.io/) use karo screen ko multiplex karne ke liye, khaaskar remote ssh sessions mein useful hai aur detach/reattach karne ke liye. `byobu` screen ya tmux ko enhance kar sakta hai zyada information aur easy management dekar. Ek aur minimal alternative sirf session persistence ke liye hai [`dtach`](https://github.com/bogner/dtach).  

- ssh mein, port tunnel karna seekhna `-L` ya `-D` (aur kabhi kabhi `-R`) ke sath useful hai, misal ke taur par remote server se websites access karne ke liye.  

- Apni ssh configuration mein kuch optimizations karna useful ho sakta hai; misal ke taur par, ye `~/.ssh/config` settings rakhta hai jo certain network environments mein dropped connections avoid karti hain, compression use karta hai (jo scp ke sath low-bandwidth connections par helpful hai), aur multiplex channels ko same server ke sath ek local control file ke through use karta hai:  

```bash
  TCPKeepAlive=yes
  ServerAliveInterval=15
  ServerAliveCountMax=6
  Compression=yes
  ControlMaster auto
  ControlPath /tmp/%r@%h:%p
  ControlPersist yes
```

- Kuch aur options jo ssh ke relevant hain wo security sensitive hote hain aur unhein ehtiyaat ke sath enable karna chahiye, misal ke taur par per subnet ya host ya trusted networks mein: `StrictHostKeyChecking=no`, `ForwardAgent=yes`  

- [`mosh`](https://mosh.org/) ko ssh ka ek alternative samjho jo UDP use karta hai, jo dropped connections avoid karta hai aur safar mein convenience deta hai (server-side setup ki zaroorat hoti hai).  

- Ek file ke permissions ko octal form mein lena, jo system configuration ke liye useful hai lekin `ls` mein available nahi hota aur asaani se ghalat ho sakta hai, use karo is tarah:  
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Kisi doosre command ke output se values ka interactive selection karne ke liye, [`percol`](https://github.com/mooz/percol) ya [`fzf`](https://github.com/junegunn/fzf) use karo.  

- Doosre command (jaise `git`) ke output ke base par files ke sath interact karne ke liye, `fpp` ([PathPicker](https://github.com/facebook/PathPicker)) use karo.  

- Ek simple web server banane ke liye jo current directory (aur subdirs) ke sab files ko serve kare, aur network par kisi bhi insaan ko available ho, use karo:  
`python -m SimpleHTTPServer 7777` (port 7777 aur Python 2 ke liye) aur `python -m http.server 7777` (port 7777 aur Python 3 ke liye).  

- Kisi command ko doosre user ke taur par run karne ke liye, `sudo` use karo. By default ye root ke taur par run hota hai; doosra user specify karne ke liye `-u` use karo. `-i` use karo login hone ke liye us user ke taur par (tumse tumhara _apna_ password poocha jaye ga).  

- Shell ko doosre user ke sath switch karne ke liye, `su username` ya `su - username` use karo. Dusra wala, "-" ke sath, ek environment deta hai jaise doosra user abhi abhi login hua ho. Username omit karne ka matlab hai root. Tumse us user ka password poocha jaye ga _jiske paas tum switch kar rahe ho_.  

- Command lines par [128K limit](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) ke bare mein jaanno. Ye "Argument list too long" error common hai jab bohot saare files par wildcard matching hoti hai. (Jab aisa hota hai, to alternatives jaise `find` aur `xargs` help kar sakte hain.)  

- Ek basic calculator (aur obviously Python ka access general tor par) ke liye, `python` interpreter use karo. Misal:  
```
>>> 2+3
5
```

## Files aur Data ko Process karna

- Current directory mein ek file ko naam se dhoondhne ke liye, `find . -iname '*something*'` use karo (ya similar). Kahi bhi ek file naam se dhoondhne ke liye, `locate something` use karo (lekin yaad rakho ke `updatedb` shayad abhi recent banai gayi files ko index na kiya ho).  

- Source ya data files mein general searching ke liye, `grep -r` se zyada advanced aur fast options hain, jinmein (rough order mein purane se naye tak) [`ack`](https://github.com/beyondgrep/ack2), [`ag`](https://github.com/ggreer/the_silver_searcher) ("the silver searcher"), aur [`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep) shamil hain.  

- HTML ko text mein convert karne ke liye: `lynx -dump -stdin`  

- Markdown, HTML, aur har qisam ke document conversion ke liye, [`pandoc`](http://pandoc.org/) try karo. Misal ke taur par, ek Markdown document ko Word format mein convert karne ke liye:  
  `pandoc README.md --from markdown --to docx -o temp.docx`  

- Agar tumhein XML handle karna zaroori ho, to `xmlstarlet` purana hai lekin acha hai.  

- JSON ke liye, [`jq`](http://stedolan.github.io/jq/) use karo. Interactive use ke liye [`jid`](https://github.com/simeji/jid) aur [`jiq`](https://github.com/fiatjaf/jiq) bhi dekho.  

- YAML ke liye, [`shyaml`](https://github.com/0k/shyaml) use karo.  

- Excel ya CSV files ke liye, [csvkit](https://github.com/onyxfish/csvkit) provide karta hai `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.  

- Amazon S3 ke liye, [`s3cmd`](https://github.com/s3tools/s3cmd) convenient hai aur [`s4cmd`](https://github.com/bloomreach/s4cmd) fast hai. Amazon ka [`aws`](https://github.com/aws/aws-cli) aur improved [`saws`](https://github.com/donnemartin/saws) AWS-related tasks ke liye essential hain.  

- `sort` aur `uniq` ke bare mein jaanno, specially uniq ke `-u` aur `-d` options — neeche one-liners mein dekho. `comm` bhi dekho.  

- `cut`, `paste`, aur `join` jaanno text files ko manipulate karne ke liye. Bohot log `cut` use karte hain lekin `join` bhool jaate hain.  

- `wc` jaanno newlines (`-l`), characters (`-m`), words (`-w`) aur bytes (`-c`) count karne ke liye.  

- `tee` jaanno stdin se ek file mein copy karne ke liye aur saath hi stdout par bhejne ke liye, jaise `ls -al | tee file.txt`.  

- Complex calculations ke liye, jinmein grouping, fields reverse karna, aur statistical calculations shamil hain, [`datamash`](https://www.gnu.org/software/datamash/) consider karo.  

- Jaanno ke locale bohot se command line tools ko subtle tareeqe se affect karta hai, jaise sorting order (collation) aur performance. Aksar Linux installations `LANG` ya dusre locale variables ko ek local setting (jaise US English) par set karte hain. Lekin aware raho ke agar tum locale change karte ho to sorting change ho jayegi. Aur jaanno ke i18n routines sort ya dusre commands ko *bohot dafa* slow bana dete hain. Kuch situations mein (jaise neeche set operations ya uniqueness operations) tum i18n routines ko ignore karke traditional byte-based sort order use kar sakte ho, `export LC_ALL=C` use karke.  

- Tum ek specific command ka environment set kar sakte ho uski invocation ke sath environment variable prefix karke, jaise:  
  `TZ=Pacific/Fiji date`  

- Basic `awk` aur `sed` seekho simple data munging ke liye. [One-liners](#one-liners) mein examples dekho.  


- Ek ya zyada files mein, ek string ke saare occurrences ko replace karne ke liye, inplace:  
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```
- Multiple files rename karne ke liye aur/ya files ke andar search aur replace karne ke liye, [`repren`](https://github.com/jlevy/repren) try karo. (Kuch cases mein `rename` command bhi multiple renames allow karta hai, lekin ehtiyaat karo kyunke iska functionality har Linux distribution par same nahi hota.)  

```sh
      # Filenames, directories, aur contents ka full rename foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Backup files recover karna whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Upar wala same kaam, rename use karke, agar available ho:
      rename 's/\.bak$//' *.bak
```

- Jaise man page kehti hai, `rsync` asal mein ek fast aur bohot hi versatile file copying tool hai. Ye machines ke darmiyan synchronize karne ke liye mashhoor hai lekin locally bhi utna hi useful hai. Jab security restrictions allow karti hain, `rsync` use karna `scp` ki jagah transfer ko recover karne deta hai bina dobara se shuru kiye. Ye un [sabse fast tareeqon](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) mein se bhi hai jo bohot zyada files delete karne ke liye use hote hain:  
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Files process karte waqt progress monitor karne ke liye use karo [`pv`](http://www.ivarch.com/programs/pv.shtml), [`pycp`](https://github.com/dmerejkowsky/pycp), [`pmonitor`](https://github.com/dspinellis/pmonitor), [`progress`](https://github.com/Xfennec/progress), `rsync --progress`, ya block-level copying ke liye `dd status=progress`.  

- `shuf` use karo file se random lines shuffle karne ya select karne ke liye.  

- `sort` ke options jaanno. Numbers ke liye `-n` use karo, ya `-h` human-readable numbers handle karne ke liye (misal ke taur par `du -h` se). Keys kaise kaam karte hain samjho (`-t` aur `-k`). Khaaskar, dhyaan rahe ke tumhein `-k1,1` likhna hoga sirf pehle field ke hisaab se sort karne ke liye; `-k1` ka matlab hai poori line ke hisaab se sort. Stable sort (`sort -s`) useful ho sakta hai. Misal ke taur par, pehle field 2 ke hisaab se sort karne ke liye aur phir secondary taur par field 1 ke hisaab se, tum use kar sakte ho:  
  `sort -k1,1 | sort -s -k2,2`  

- Agar kabhi tumhein Bash command line mein ek tab literal likhna ho (misal ke taur par `-t` argument ke liye sort mein), to **ctrl-v** **[Tab]** dabao ya `$'\t'` likho (dusra option behtar hai kyunki copy/paste kiya ja sakta hai).  

- Source code patch karne ke liye standard tools hain `diff` aur `patch`. Saath hi dekho `diffstat` jo diff ka summary statistics deta hai aur `sdiff` jo side-by-side diff dikhata hai. Note karo `diff -r` poore directories ke liye kaam karta hai. Changes ka ek summary dekhne ke liye use karo:  
  `diff -r tree1 tree2 | diffstat`  
  Files compare aur edit karne ke liye `vimdiff` use karo.  

- Binary files ke liye, `hd`, `hexdump` ya `xxd` use karo simple hex dumps ke liye, aur `bvi`, `hexedit` ya `biew` binary editing ke liye.  

- Binary files ke liye, `strings` (saath mein `grep`, etc.) tumhein text ke tukray dhoondhne mein madad karta hai.  

- Binary diffs (delta compression) ke liye `xdelta3` use karo.  

- Text encodings convert karne ke liye, `iconv` try karo. Ya `uconv` aur advanced use ke liye; ye kuch advanced Unicode cheezein support karta hai. Misal ke taur par:  

```sh
      # Hex codes ya characters ke asal names dikhata hai (debugging ke liye useful):
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Lowercase karta hai aur sab accents remove karta hai (expand karke aur drop karke):
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```

- Files ko pieces mein split karne ke liye, `split` dekho (size ke hisaab se split karne ke liye) aur `csplit` (pattern ke hisaab se split karne ke liye).  

- Date aur time: Current date aur time helpful [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format mein hasil karne ke liye use karo `date -u +"%Y-%m-%dT%H:%M:%SZ"` (dusre options [problematic hain](https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option), [dekho](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)). Date aur time expressions manipulate karne ke liye, use karo `dateadd`, `datediff`, `strptime` etc. jo [`dateutils`](http://www.fresse.org/dateutils/) mein milte hain.  

- `zless`, `zmore`, `zcat`, aur `zgrep` use karo compressed files par operate karne ke liye.  

- File attributes `chattr` ke zariye set kiye ja sakte hain aur ye file permissions ka ek lower-level alternative dete hain. Misal ke taur par, accidental file deletion se bachne ke liye immutable flag lagao:  
  `sudo chattr +i /critical/directory/or/file`  

- `getfacl` aur `setfacl` use karo file permissions save aur restore karne ke liye. Misal ke taur par:  
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

- Khali files jaldi banane ke liye, `truncate` use karo (banata hai [sparse file](https://en.wikipedia.org/wiki/Sparse_file)), `fallocate` (ext4, xfs, btrfs aur ocfs2 filesystems ke liye), `xfs_mkfile` (lagbhag har filesystem ke liye, aata hai xfsprogs package ke sath), `mkfile` (Unix-like systems jaise Solaris, Mac OS ke liye).  

## System debugging  

- Web debugging ke liye, `curl` aur `curl -I` handy hain, ya unke `wget` equivalents, ya phir modern [`httpie`](https://github.com/jkbrzt/httpie).  

- Current CPU/disk status jaan’ne ke liye, classic tools hain `top` (ya behtareen `htop`), `iostat`, aur `iotop`. `iostat -mxz 15` use karo basic CPU aur har partition ka detailed disk stats aur performance insight ke liye.  

- Network connection details ke liye, `netstat` aur `ss` use karo.  

- Ek quick overview ke liye ke system mein kya chal raha hai, `dstat` especially useful hai. Sabse broad overview ke sath details ke liye, [`glances`](https://github.com/nicolargo/glances) use karo.  

- Memory status jaan’ne ke liye, `free` aur `vmstat` run karo aur unka output samjho. Khaaskar, "cached" value ka dhyaan rakho — ye Linux kernel ke file cache ki memory hoti hai, jo asal mein "free" value mein count hoti hai.  

- Java system debugging ek alag cheez hai, lekin ek simple trick Oracle aur kuch aur JVMs par ye hai ke tum `kill -3 <pid>` run karo aur ek full stack trace aur heap summary (jisme generational garbage collection details bhi hoti hain jo kaafi informative hoti hain) stderr/logs mein dump ho jayegi. JDK ke tools `jps`, `jstat`, `jstack`, `jmap` useful hain. [SJK tools](https://github.com/aragozin/jvm-tools) zyada advanced hain.  

- [`mtr`](http://www.bitwizard.nl/mtr/) use karo ek behtareen traceroute ke taur par, network issues identify karne ke liye.  

- Agar dekhna ho ke disk kyon full hai, to [`ncdu`](https://dev.yorhel.nl/ncdu) usual commands jaise `du -sh *` ke muqable mein waqt bachata hai.  

- Yeh jaan’ne ke liye ke kaunsa socket ya process bandwidth use kar raha hai, [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ya [`nethogs`](https://github.com/raboof/nethogs) try karo.  

- `ab` tool (jo Apache ke sath aata hai) quick-and-dirty web server performance check ke liye helpful hai. Zyada complex load testing ke liye, `siege` try karo.  

- Serious network debugging ke liye, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), ya [`ngrep`](http://ngrep.sourceforge.net/) use karo.  

- `strace` aur `ltrace` ke bare mein jaanno. Ye helpful hote hain agar koi program fail ho raha ho, hang ho raha ho, ya crash ho raha ho aur tumhein wajah nahi pata, ya tumhein ek general idea chahiye performance ka. Profiling option (`-c`) ka dhyaan rakho, aur running process ko attach karne ki ability (`-p`). Trace child option (`-f`) use karo taake important calls miss na hoon.  

- `ldd` ke bare mein jaanno shared libraries check karne ke liye — lekin [kabhi bhi untrusted files par run mat karo](http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).  

- Seekho ke running process se kaise connect karte hain `gdb` ke zariye aur uske stack traces nikalte hain.  

- `/proc` use karo. Kabhi kabhi live problems debug karte waqt bohot hi helpful hota hai. Examples: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (yahan `xxx` process id ya pid hai).  

- Jab debug karna ho ke pichle waqt mein kyon kuch galat hua, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) bohot helpful hai. Ye historic statistics dikhata hai CPU, memory, network, etc. ke bare mein.  

- Zyada gehre systems aur performance analyses ke liye, `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_%28Linux%29), aur [`sysdig`](https://github.com/draios/sysdig) dekho.  

- Dekho ke tum kaunse OS par ho `uname` ya `uname -a` se (general Unix/kernel info) ya `lsb_release -a` se (Linux distro info).  

- `dmesg` use karo jab bhi koi cheez ajeeb behave kar rahi ho (ye hardware ya driver issues ho sakte hain).  

- Agar tumne ek file delete ki aur expected disk space free nahi hua jaise `du` report karta hai, check karo ke kya wo file abhi bhi kisi process ke zariye use ho rahi hai:  
`lsof | grep deleted | grep "filename-of-my-big-file"`  

## One-liners  

Kuch examples commands ko mila kar use karne ke:  

- Kabhi kabhi ye bohot madadgar hota hai ke tum text files ka set intersection, union, aur difference kar sako `sort`/`uniq` ke zariye. Misaal ke taur par `a` aur `b` text files hain jo already uniqued hain. Ye fast hai, aur arbitrary size ki files par kaam karta hai, hatta ke bohot si gigabytes tak. (Sort memory se limited nahi hai, lekin tumhein `-T` option use karna par sakta hai agar `/tmp` ek chhoti root partition par ho). Upar wale `LC_ALL` wale note ko bhi dekho aur `sort` ka `-u` option (neeche clarity ke liye chhoda gaya hai).  

```sh
      sort a b | uniq > c        # c hai a union b  
      sort a b | uniq -d > c     # c hai a intersect b  
      sort a b b | uniq -u > c   # c hai set difference a - b  
```

- Do JSON files ko pretty-print karo, unki syntax normalize karke, phir result ko color aur paginate karo:  
```
      diff <(jq --sort-keys . < file1.json) <(jq --sort-keys . < file2.json) | colordiff | less -R
```

- `grep . *` use karo taake ek directory ke saare files ka content jaldi examine kar sako (har line filename ke sath pair hoti hai), ya `head -100 *` (taake har file ka ek heading aa jaye). Ye kaafi useful hai un directories ke liye jo config settings se bhari hoti hain, jaise `/sys`, `/proc`, `/etc`.  

- Ek text file ke teesray column mein saare numbers ko sum karna (ye shayad 3X faster aur 3X kam code hai equivalent Python se):  
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Files ke tree par sizes/dates dekhne ke liye, ye ek recursive `ls -l` ki tarah hai lekin `ls -lR` se zyada easy hai read karne ke liye:  
```sh
      find . -type f -ls
```


- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```
- Changes ko continuously monitor karne ke liye, `watch` use karo. Misal ke taur par, ek directory mein files ke changes check karo `watch -d -n 2 'ls -rtlh | tail'` ke sath, ya network settings troubleshoot karte waqt apne wifi settings ko dekhne ke liye `watch -d -n 2 ifconfig`.  

- Ye function run karo taake is document se ek random tip mil jaye (Markdown ko parse karta hai aur ek item extract karta hai):  
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          sed '/cowsay[.]png/d' |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80 | iconv -t US
      }
```

## Obscure lekin Kaam ke (Obscure but useful)

- `exr`: arithmetic ya boolean operations perform karo ya regular expressions evaluate karo  

- `m4`: simple macro processor  

- `yes`: ek string bohot dafa print karo  

- `cal`: acha calendar  

- `env`: ek command run karo (scripts mein useful)  

- `printenv`: environment variables print karo (debugging aur scripts mein useful)  

- `look`: English words (ya ek file ki lines) dhoondo jo ek string se start hoti hain  

- `cut`, `paste` aur `join`: data manipulation  

- `fmt`: text paragraphs format karo  

- `pr`: text ko pages/columns mein format karo  

- `fold`: text ki lines wrap karo  

- `column`: text fields ko aligned, fixed-width columns ya tables mein format karo  

- `expand` aur `unexpand`: tabs aur spaces ke darmiyan convert karo  

- `nl`: line numbers add karo  

- `seq`: numbers print karo  

- `bc`: calculator  

- `factor`: integers ko factor karo  

- [`gpg`](https://gnupg.org/): files ko encrypt aur sign karo  

- `toe`: terminfo entries ki table  

- `nc`: network debugging aur data transfer  

- `socat`: socket relay aur tcp port forwarder (bilkul `netcat` jaisa)  

- [`slurm`](https://github.com/mattthias/slurm): network traffic visualization  

- `dd`: data ko files ya devices ke darmiyan move karo  

- `file`: ek file ka type identify karo  

- `tree`: directories aur subdirectories ko ek nesting tree ki tarah display karo; `ls` jaisa lekin recursive  

- `stat`: file info  

- `time`: ek command execute karo aur uska time nikaalo  

- `timeout`: ek command specified waqt ke liye execute karo aur jab woh waqt complete ho to process ko stop kar do  

- `lockfile`: ek semaphore file create karo jo sirf `rm -f` se remove ho sakti hai  

- `logrotate`: logs ko rotate, compress aur mail karo  

- `watch`: ek command bar bar run karo, results show karo aur/ya changes highlight karo  

- [`when-changed`](https://github.com/joh/when-changed): koi bhi command run karta hai jab bhi file change hoti hai. `inotifywait` aur `entr` bhi dekho.  

- `tac`: files ko reverse mein print karo  

- `comm`: sorted files ko line by line compare karo  

- `strings`: binary files se text extract karo  

- `tr`: character translation ya manipulation  

- `iconv` ya `uconv`: text encodings ke liye conversion  

- `split` aur `csplit`: files ko split karo  

- `sponge`: saara input pehle read karo likhne se pehle, useful jab same file ko read aur write karna ho, misal ke taur par `grep -v something some-file | sponge some-file`  

- `units`: unit conversions aur calculations; furlongs per fortnight ko twips per blink mein convert karta hai (yeh bhi dekho: `/usr/share/units/definitions.units`)  

- `apg`: random passwords generate karta hai  

- `xz`: high-ratio file compression  

- `ldd`: dynamic library info  

- `nm`: object files se symbols  

- `ab` ya [`wrk`](https://github.com/wg/wrk): web servers ka benchmarking  

- `strace`: system call debugging  

- [`mtr`](http://www.bitwizard.nl/mtr/): network debugging ke liye better traceroute  

- `cssh`: visual concurrent shell  

- `rsync`: files aur folders ko sync karo SSH ke zariye ya local file system mein  

- [`wireshark`](https://wireshark.org/) aur [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): packet capture aur network debugging  

- [`ngrep`](http://ngrep.sourceforge.net/): network layer ke liye grep  

- `host` aur `dig`: DNS lookups  

- `lsof`: process file descriptor aur socket info  

- `dstat`: useful system stats  

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview  

- `iostat`: Disk usage stats  

- `mpstat`: CPU usage stats  

- `vmstat`: Memory usage stats  

- `htop`: `top` ka improved version  

- `last`: login history  

- `w`: kaun logged on hai  

- `id`: user/group identity info  

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): historic system stats  

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ya [`nethogs`](https://github.com/raboof/nethogs): socket ya process ke hisaab se network utilization  

- `ss`: socket statistics  

- `dmesg`: boot aur system error messages  

- `sysctl`: Linux kernel parameters ko run time par view aur configure karo  

- `hdparm`: SATA/ATA disk manipulation/performance  

- `lsblk`: block devices list karo: tumhare disks aur partitions ka tree view  

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, jisme CPU, BIOS, RAID, graphics, devices, etc. shamil hain  

- `lsmod` aur `modinfo`: kernel modules list karo aur details dikhao  

- `fortune`, `ddate`, aur `sl`: um, well, yeh depend karta hai ke tum steam locomotives aur Zippy quotations ko "useful" samajhte ho ya nahi 😅  


## Sirf macOS ke liye (macOS only)

Ye items sirf macOS par relevant hain.  

- Package management ke liye `brew` (Homebrew) aur/ya `port` (MacPorts). Ye macOS par upar diye gaye bohot se commands install karne ke liye use ho sakte hain.  

- Kisi bhi command ka output ek desktop app mein copy karo `pbcopy` se aur input paste karo `pbpaste` se.  

- macOS Terminal mein Option key ko alt key (jaise upar diye gaye commands mein **alt-b**, **alt-f**, etc.) enable karne ke liye: Preferences -> Profiles -> Keyboard mein jao aur "Use Option as Meta key" select karo.  

- Ek file ko desktop app ke sath open karne ke liye, `open` ya `open -a /Applications/Whatever.app` use karo.  

- Spotlight: Files search karne ke liye `mdfind` aur metadata list karne ke liye (jaise photo EXIF info) `mdls` use karo.  

- Ye jaanno ke macOS BSD Unix par based hai, aur bohot se commands (misal ke taur par `ps`, `ls`, `tail`, `awk`, `sed`) Linux se subtly different hote hain, jo zyadatar System V-style Unix aur GNU tools se influenced hai. Tum aksar difference pehchan sakte ho jab man page ke heading mein likha hota hai "BSD General Commands Manual." Kuch cases mein GNU versions bhi install kiye ja sakte hain (misal ke liye `gawk` aur `gsed` GNU awk aur sed ke liye). Agar cross-platform Bash scripts likh rahe ho, to aise commands avoid karo (misal ke liye Python ya `perl` consider karo) ya phir carefully test karo.  

- macOS release information lene ke liye `sw_vers` use karo.  

## Sirf Windows ke liye (Windows only)

Ye items *sirf* Windows par relevant hain.  

### Windows par Unix tools hasil karne ke tareeqe  

- Microsoft Windows par Unix shell ki power hasil karo [Cygwin](https://cygwin.com/) install karke. Is document mein describe ki gayi ziada cheezein out of the box kaam karengi.  

- Windows 10 par tum [Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about) use kar sakte ho, jo ek familiar Bash environment provide karta hai Unix command line utilities ke sath.  

- Agar tum mainly GNU developer tools (jaise GCC) Windows par use karna chahte ho, to [MinGW](http://www.mingw.org/) aur iska [MSYS](http://www.mingw.org/wiki/msys) package consider karo, jo utilities provide karta hai jaise bash, gawk, make aur grep. MSYS mein sari features nahi hoti compared to Cygwin. MinGW khas taur par useful hai Unix tools ke native Windows ports banane ke liye.  

- Ek aur option Windows par Unix look aur feel hasil karne ka hai [Cash](https://github.com/dthree/cash). Note karo ke is environment mein sirf bohot kam Unix commands aur command-line options available hain.  

### Useful Windows command-line tools  

- Tum ziada tar Windows system administration tasks command line se perform aur script kar sakte ho `wmic` seekh kar aur use karke.  

- Native command-line Windows networking tools jo tumhein useful lag sakte hain un mein shamil hain `ping`, `ipconfig`, `tracert`, aur `netstat`.  

- Tum [bohot si useful Windows tasks](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) perform kar sakte ho `Rundll32` command invoke karke.  

### Cygwin tips aur tricks  

- Additional Unix programs install karo Cygwin ke package manager se.  

- `mintty` use karo apna command-line window ke liye.  

- Windows clipboard access karo `/dev/clipboard` ke zariye.  

- `cygstart` run karo kisi bhi arbitrary file ko uske registered application ke sath open karne ke liye.  

- Windows registry access karo `regtool` ke sath.  

- Note karo ke ek `C:\` Windows drive path Cygwin ke andar `/cygdrive/c` ban jata hai, aur Cygwin ka `/` Windows par `C:\cygwin` ke andar nazar aata hai. Cygwin aur Windows-style file paths convert karo `cygpath` se. Ye ziada tar scripts mein useful hota hai jo Windows programs invoke karte hain.  

## Mazeed Resources (More resources)

- [awesome-shell](https://github.com/alebcay/awesome-shell): Shell tools aur resources ki ek curated list.  
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): macOS command line ke liye ek zyada detail guide.  
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/): Behtareen shell scripts likhne ke liye.  
- [shellcheck](https://github.com/koalaman/shellcheck): Ek shell script static analysis tool. Asal mein, bash/sh/zsh ke liye lint.  
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Wo afsosnak tor par complex minutiae jo batati hai ke filenames ko shell scripts mein sahi handle kaise karein.  
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Zyada commands aur tools jo data science karne mein helpful hain, isi naam ki kitab se.  

## Disclaimer  

Choti tasks ke ilawa, code aise likha jata hai taake doosre log usay parh saken. Power ke sath responsibility bhi aati hai. Ye fact ke tum *kar sakte ho* Bash mein kuch, iska matlab ye nahi ke tumhe karna chahiye! ;)  

## License  

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)  

Ye kaam [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/) ke under licensed hai.  


