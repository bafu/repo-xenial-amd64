# Steps to Create This Repo

1. Create a local repository:

    ```
    $ mkdir -p myrepo/conf && cd myrepo
    
    # Create repo w/ signature
    $ cat <<EOF > conf/distributions
    Origin: Bofu Chen
    Label: Bofu Github
    Suite: stable
    Codename: xenial
    Architectures: amd64
    Components: main
    Description: Debian packages hosted on Bofu github repository
    SignWith: 3FB8B4C2
    EOF
    
    $ reprepro includedeb xenial <pkg-path>
    ```

1. Create repository on GitHub, and push local repo to it.
1. Add source list file:

    ```
    $ sudo cat <<EOF > /etc/apt/sources.list.d/<src-list>
    deb [arch=amd64] https://raw.githubusercontent.com/bafu/repo-xenial-amd64/master xenial main
    EOF
    ```

# Local Repo

```
$ cat conf/distributions
Label: Local APT repository
Codename: stretch
Architectures: armhf
Components: main
Description: Local APT repository for debootstrap

$ sudo cat <<EOF > /etc/apt/sources.list.d/<src-list>
deb [trusted=yes] file://<repo-dir-path> stretch main
EOF
```

APT parameter `--allow-unauthenticated` is package-level, not repo-level.

# References

* [Creating Remote APT Package Repositories on Github](http://www.hackgnar.com/2016/01/creating-remote-apt-package.html?m=1)
* [https://pmateusz.github.io/linux/2017/06/30/linux-secure-apt-repository.html](https://pmateusz.github.io/linux/2017/06/30/linux-secure-apt-repository.html)
* [How to quickly create a local apt repository for random packages using a Debian based linux distribution?](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian)
