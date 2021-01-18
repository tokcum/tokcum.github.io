---
layout: post
title:  "Getting ready: the Tools"
author: "tokcum"
location: "Augsburg"
time-required: "20 min"
date: 2021-01-08 22:00:00 +0200
categories: project
tags: setup
---

Proficient software developers have to master many tools, with some of them being so powerful that they represent 
an area of expertise on their own. As I know from my own experience this can be a challenge for newcomers because 
tools can easily distract them from the lesson to be learned, or the job to be done. Facing this challenge myself 
I learned to: 

1. Keep the number of tools at a minimum.
2. Accept to live with some drawbacks instead of keep searching for the non-plus-ultra solution.
3. Make an informed choice and stick to it as long as there is no show-stopper coming up.
4. Evaluate the work environment from time to time and get rid of ballast such as outdated tools and repetitive manual tasks.

So here is my work actual environment:

1. Manjaro Linux
2. Rust Toolchain managed by rustup
3. IntelliJ Idea Community Edition
4. Git with Github

Let me provide you some background information you might find useful.

## Manjaro Linux

I have been working with Linux since I had my first computer back in 1995. Over the years I tried many 
Linux distributions including SuSE, RedHat & CentOS as well as Debian and Ubuntu. After all these years 
I was fed up with the effort required to keep up to date with the never ending stream of releases. More 
than once I experienced a number of issues during updating to a new release and occasionally an installation 
from scratch was the way to go. In hindsight, I tend to think that forcing users to follow a release cycle 
might be a fundamental misconception.

In 2019, I decided to turn to a Linux distribution with a rolling release. I started with Arch Linux and 
shortly after switched to Manjaro Linux as a concession to my family. 
Since then, I enjoy a stable and always up to date Linux system with an unprecedented range of software available 
in the official repos or via the Arch User Repository (AUR). It's simply amazing. I never missed the cacophony 
of repositories in the SuSE ecosystem, the pain with PPAs in Ubuntu or even worse the package manager Snap.

Manjaro offers a variety of desktop environments. I like to have a lean and fast system thus I decided to use 
XFCE as a desktop environment. By the way, [It's FOSS][itsfoss.com_itsfoss-project-site] maintains a valuable 
[Manjaro installation guide][itsfoss.com_install-manjaro-linux].


## Rust toolchain

The Rust toolchain includes all the tools needed to get started with software development in Rust. Introducing 
the different tools would require a series of blog posts on its own. So I won't go into the details here. Let's focus 
on the deployment options though.

When looking for tools as a Linux user, first I check the software repositories. Sticking to software available 
in the repos and installing it via the package manager ensures that all software installed on the system 
is well documented and consequently managed.

In Manjaro, _pacman_ is in charge of package management. The official Arch Linux Wiki offers a comprehensive article 
on [pacman][wiki.archlinux.org_pacman]. From a user's perspective the [pacman tutorial][itsfoss.com_pacman] 
available at [It's FOSS][itsfoss.com_itsfoss-project-site] provides a better start though without missing to dig 
into the details at the end of the article. 
As Manjaro promises to be more user friendly compared to Arch, there is also a graphical front end called 
_pamac-manager_ available in the menu. However, for brevity I use _pacman_ at the command line to search 
for all packages whose name start with _rust_:

    [tobias@chiemsee ~]$ pacman -Ss ^rust
    extra/rust 1:1.48.0-1
        Systems programming language focused on safety, speed and concurrency
    extra/rust-docs 1:1.48.0-1
        Documentation for the Rust programming language
    [...]
    community/rustup 1.23.1-1
        The Rust toolchain installer
    [tobias@chiemsee ~]$

So Manjaro has _rust_ in version 1.48 available in the repos (as of January 8th 2021). Looking for 
other [Rust releases][github.com_rust-lang-releases] reveals that this version was released on November 19th 2020. 
On December 31th Rust release 1.49 was published which is not yet available in Manjaro's repos.

Another option to install Rust is to use [rustup][rustup.rs_rustup-project-site], the official tool to manage 
the Rust toolchain and thus recommended by the Rust project and briefly introduced on 
[Notes about Rust installation][rust-lang.org_rust_install].

However, I do not favor the installation method described at the [rustup website][rustup.rs_rustup-project-site] 
which is based on curl and an installation script. Although this approach is easy to use, 
it deploys software on the system bypassing the package manager. As you may have noticed in the package list above, 
_rustup_ is also available in the Manjaro repos. So I install it from there. Please note that administrative rights 
are mandatory for installation. That's why I have to use _sudo_.

    [tobias@chiemsee ~]$ sudo pacman -S rustup
    resolving dependencies...
    looking for conflicting packages...
    
    Packages (1) rustup-1.23.1-1
    
    Total Installed Size:  6.95 MiB
    
    :: Proceed with installation? [Y/n] Y
    [...]
    [tobias@chiemsee ~]$ pacman -Ss rustup
    community/rustup 1.23.1-1 [installed]
    The Rust toolchain installer
    [tobias@chiemsee ~]$

With _rustup_ installed we are able to manage the Rust toolchain without administrative rights because 
_rustup_ works in our home directory in _~/.rustup_ and installs the tools to ~/.cargo[^1].

So let's get started with _rustup_.

    [tobias@chiemsee ~]$ rustup --version
    rustup 1.23.1 (2020-12-18)
    info: This is the version for the rustup toolchain manager, not the rustc compiler.
    [tobias@chiemsee ~]$ rustup show
    Default host: x86_64-unknown-linux-gnu
    rustup home:  /home/tobias/.rustup
    
    no active toolchain
    [tobias@chiemsee ~]$

So there is no active toolchain yet. For now, I choose to install the latest stable rust release and _rustup_ 
figures out my platform and installs the appropriate toolchain consisting several distinct tools such as _cargo_, 
_clippy_, _rustc_ and others. Finally, this toolchain is set as default. 

    [tobias@chiemsee ~]$ rustup toolchain install stable
    info: syncing channel updates for 'stable-x86_64-unknown-linux-gnu'
    info: latest update on 2020-12-31, rust version 1.49.0 (e1884a8e3 2020-12-29)
    info: downloading component 'cargo'
    [...]
    info: downloading component 'clippy'
    [...]
    info: downloading component 'rustc'
    [...]

    stable-x86_64-unknown-linux-gnu installed - rustc 1.49.0 (e1884a8e3 2020-12-29)
    
    info: default toolchain set to 'stable-x86_64-unknown-linux-gnu'
    [tobias@chiemsee ~]$
    [...]
    [tobias@chiemsee ~]$

We can now check the availability of _rustc_ via _rustup_ or by directly running _rustc_.

    [tobias@chiemsee ~]$ rustup show
    Default host: x86_64-unknown-linux-gnu
    rustup home:  /home/tobias/.rustup
    
    stable-x86_64-unknown-linux-gnu (default)
    rustc 1.49.0 (e1884a8e3 2020-12-29)
    [tobias@chiemsee ~]$ rustc --version
    rustc 1.49.0 (e1884a8e3 2020-12-29)
    [tobias@chiemsee ~]$

By the way _rustup_ is completely covered in the [Rustup Book][rust-lang.github.io_rustup-book].


# IntelliJ IDEA Community Edition

Finally, I would like to develop in an integrated development environment (IDE). IntelliJ IDEA supports Rust 
excellently through a freely available plugin maintained by the IDE software editor [JetBrains][jetbrains.com_website].

Fortunately the Community Edition of IntelliJ IDEA is free of charge and available in the Manjaro repositories.
This allows us to get started quickly. Just call _pacman_ from the console, search and install the package as 
shown previously. From my experience on Arch Linux this package has issues from time to time[^2]. These were 
covered so far by Manjaro due to there additional testing and user focused attitude.

The Rust plugin is installed separately within IntelliJ IDEA in the menu _File > Settings > Plugins_. It has 
dependency to the TOML plugin which is automatically resolved and both plugins get installed [^3]


So, that's it for today. We have our tools up and running and I'm looking forward to setting up the Rust project.


# Further reading

#### in English

[Manjaro Installation Guide, last accessed on 2021-01-26][itsfoss.com_install-manjaro-linux]

[7 Reasons Why I Use Manjaro Linux And You Should Too][itsfoss.com_why-use-manjaro-linux]

[Rust Installation: a brief introduction][rust-lang.org_rust_install]

[Rust at Github: List of Releases][github.com_rust-lang-releases]


# References 

[Arch Linux, last accessed on 2021-01-16][archlinux.org_arch-project-site]

[Pacman in the Arch Linux Wiki, last accessed on 2021-01-17][wiki.archlinux.org_pacman]

[It's FOSS, last accessed on 2021-01-16][itsfoss.com_itsfoss-project-site]

[It's FOSS: Pacman tutorial, last accessed on 2021-01-17][itsfoss.com_pacman]

[JetBrains Website][jetbrains.com_website]

[Manjaro Linux, last accessed on 2021-01-16][manjaro.org_manjaro-project-site]

[rustup.rs: The Rust toolchain installer, last accessed on 2021-01-16][rustup.rs_rustup-project-site]

[Rustup Book, last accessed on 2021-01-17][rust-lang.github.io_rustup-book]



[//]: # (Links)
[archlinux.org_arch-project-site]: https://archlinux.org/
[wiki.archlinux.org_pacman]: https://wiki.archlinux.org/index.php/Pacman
[archlinux.org_forum]: https://bbs.archlinux.org/
[github.com_rust-lang-releases]: https://github.com/rust-lang/rust/releases
[itsfoss.com_itsfoss-project-site]: https://itsfoss.com/
[itsfoss.com_install-manjaro-linux]: https://itsfoss.com/install-manjaro-linux/
[itsfoss.com_why-use-manjaro-linux]: https://itsfoss.com/why-use-manjaro-linux/
[itsfoss.com_pacman]: https://itsfoss.com/pacman-command/
[jetbrains.com_website]: https://www.jetbrains.com/
[manjaro.org_manjaro-project-site]: https://manjaro.org/
[rustup.rs_rustup-project-site]: https://rustup.rs/
[rust-lang.org_rust_install]: https://www.rust-lang.org/tools/install
[rust-lang.github.io_rustup-book]: https://rust-lang.github.io/rustup/index.html

# Footnotes

[^1]: Thinking of a corporate environment where several developers have to work with the same toolchain consistently, the individual installation into personal homes is definitely not the best choice. I have already solved this requirement at work and maybe I describe the approach taken in another post.

[^2]: At the times I worked with Arch Linux in 2019 and 20 I experienced two times issues with this package which stopped my productivity completely. The problems arose from incompatibilities with the JDK package delivered with Arch. JetBrains officially supports only the JDK (called JBR) delivered together with IntelliJ IDEA, but the Arch package maintainers do not include it into the IntelliJ IDEA package for some reason and instead rely on the JDK included with Arch. Browsing through the [Arch Linux forum][archlinux.org_forum] this is not a one time but regular issue. If you are on Arch Linux consider using the AUR package which includes the JBR and just works fine.

[^3]: Again, this might not be the best deployment option in a corporate environment. 