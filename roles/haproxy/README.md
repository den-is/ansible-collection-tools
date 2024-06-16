# HAProxy - free, very fast and reliable reverse-proxy

## Requirements
- Minimum supproted HAProxy v2.6+
- Supports systemd based OSs
- Role requires privileged permissions. Run as user `root` or `become:true`.

## Installation from official packages and compilation
Role supports installation from packages on Debian based OSs.

Compilation method is available too. Especially for situation when no official OS packages available. (RedHat based OSs)
Default compilation command:

- `make -j $(nproc) TARGET=linux-glibc USE_OPENSSL=1 USE_LUA=1 USE_PCRE2_JIT=1 USE_SYSTEMD=1 USE_ZLIB=1`

Command altered using `haproxy_compile_cmd` and `haproxy_compile_cmd_extra`

## HAProxy configuration
By default role provides very basic minimalistic configuration template.
Configuration is provided for `compilation` scenario and optional during installation during instalation from package.

You almost always will want to provide your own template using `haproxy_cfg_template_file` configuration value.
Ansible will try to find template file its search paths [doc](https://docs.ansible.com/ansible/latest/playbook_guide/playbook_pathing.html)

Your template might be using custom variables. Don't forget to supply them to role/play using one of many possible methods.

## Links
- https://www.haproxy.org
- https://docs.haproxy.org
- https://www.haproxy.com/documentation
- https://github.com/haproxy/haproxy
- https://git.haproxy.org
- https://haproxy.debian.net

# compilation commands:
- original update to 3.0
  - make -j $(nproc) TARGET=linux-glibc USE_OPENSSL=1 USE_LUA=1 USE_PCRE=1 USE_SYSTEMD=1 USE_ZLIB=1
  - custom var:
    - make -j $(nproc) TARGET=linux-glibc USE_OPENSSL=1 USE_LUA=1 USE_PCRE2=1 USE_SYSTEMD=1 USE_ZLIB=1 USE_QUIC=1 USE_QUIC_OPENSSL_COMPAT=1
- haproxy 2.6:
  - make -j $(nproc) TARGET=linux-glibc USE_OPENSSL=1 USE_LUA=1 USE_PCRE=1 USE_PCRE2=1 USE_SYSTEMD=1 USE_ZLIB=1
  USE_PCRE2_JIT=1

PCRE Support:
https://discourse.haproxy.org/t/compile-error-with-haproxy-2-1-4-and-use-static-pcre-1-on-centos-8/5202/5
https://discourse.haproxy.org/t/compile-pcre2-or-pcre/4944/2
https://stackoverflow.com/questions/70273084/regex-differences-between-pcre-and-pcre2
https://php.watch/versions/7.3/pcre2
https://www.pcre.org/
https://github.com/PCRE2Project/pcre2/issues/51
