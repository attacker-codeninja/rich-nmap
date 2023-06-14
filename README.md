# rich-nmap

![Demo](./assets/demo.gif)

A wrapper around [nmap](https://nmap.org/) that supports additional output formats.

# Setup

a) With [pipx](https://github.com/pypa/pipx).

~~~ bash
pipx install git+https://github.com/dadevel/rich-nmap.git@main
~~~

b) With [pip](https://github.com/pypa/pip).

~~~ bash
pip install --user git+https://github.com/dadevel/rich-nmap.git@main
~~~

# Usage

Discover web servers and scan them with [nuclei](https://github.com/projectdiscovery/nuclei).

~~~ bash
rich-nmap -f csv 192.168.1.0/24 -- -n -Pn -T4 -p 80,443,8000,8080,8443 -sT -sV --version-intensity 0 | \
  awk -F , '$5 == "http" || $5 == "https" { printf("%s://%s:%s\n", $5, $1, $3); }' | \
  nuclei -silent -automatic-scan
~~~
