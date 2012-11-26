---
layout: post
title: 发送gmail
category: google
tags: [google, email]
---

## SMTP Protocol

    > EHLO
    <
    > AUTH plain
    <
    > AHVzZXJAZ21haWwuY29tAFBBU1NXRA==
    <
    > MAIL FROM: <user@gmail.com>
    <
    > RCPT TO:   <user@yahoo.com>
    <
    > DATA
    <
    From: me
    To: you
    Subject: =?UTF-8?b?5L2g5aW95LiW55WMCg==?=
    Content-Type: text/html

    <b>hello, world</b>
    .
    <
    > quit
    <

## Command

    $ ncat -C --ssl smtp.gmail.com 465

    $ stunnel -c -r smtp.gmail.com:465

    $ openssl s_client -connect stmp.gmail.com:465 -starttls smtp

    $ curl smtps://smtp.gmail.com \
           -u user@gmail.com \
           --mail-from user@gmail.com \
           --mail-rcpt user@yahoo.com

note:

- press {Ctrl-V + Enter} to input '\r'
- press {Ctrl-D} to end input

## References:

- <http://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol>
- <http://en.wikipedia.org/wiki/MIME>
- <http://www.fehcom.de/qmail/smtpauth.html>
