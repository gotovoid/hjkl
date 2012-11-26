---
layout: post
title: shadow密码格式
category: linux
tags: [linux]
---

## FORMAT

    $enc-id$random-salt$password-hash

    ID | Method   | sLen | hLen | Note
    ───+──────────+──────+──────+───────────────
    -  | DES      | 2    | 11   |
    1  | MD5      | 8    | 22   |
    2a | Blowfish |      |      | not in mainline glibc
    4  | SHA-128  |      | 27   |
    5  | SHA-256  | 8~16 | 43   | since glibc 2.7
    6  | SHA-512  | 8~16 | 86   | since glibc 2.7
    
    +------------------------------------+
    | random-salt  --\                   |
    |                 +--> password-hash |
    | raw-password --/                   |
    +------------------------------------+

note: random-salt prevents [rainbow-table][1] cracking.

## KEYGEN
======

    $ openssl passwd -1 -salt SALTsalt PASSWORD
    $1$SALTsalt$BvkiiEvpuamJDOU5kLDHo/

    $ md5pass PASSWORD SALTsalt
    $1$SALTsalt$BvkiiEvpuamJDOU5kLDHo/

    $ sha1pass PASSWORD SALTsalt
    $4$SALTsalt$x5WQcbquvS/VWQx0Lu3v5b1hMlA$

    $ mkpasswd -m sha-512 PASSWORD SALTsalt
    $6$SALTsalt$XDDCmSZNELjXLtrNgQfDffc8wvd.m3HFJ4G0nOVjz/kdGAQPg9eJ7EZcMjx6u0hbak7PswaAbJw.hEfDdhRkh/
    
    $ python -c 'import crypt; print crypt.crypt("PASSWORD", "$6$SALTsalt$")'
    $6$SALTsalt$XDDCmSZNELjXLtrNgQfDffc8wvd.m3HFJ4G0nOVjz/kdGAQPg9eJ7EZcMjx6u0hbak7PswaAbJw.hEfDdhRkh/

[1]: http://www.codinghorror.com/blog/2007/09/rainbow-hash-cracking.html
