---
title: One of Gmail's spam defenses that I bumped into
url: 235.html
id: 235
categories:
  - Messaging
date: 2014-03-11 17:43:14
tags:
---

\# sendmail -v *@gmail.com
Subject: Hello World!
This is an email to myself.
.
*@gmail.com... Connecting to \[127.0.0.1\] via relay...
220 transfusion.vm ESMTP Sendmail 8.14.4/8.14.4/Debian-2.1ubuntu4; Mon, 10 Mar 2014 05:57:40 -0400; (No UCE/UBE                                                                   ) logging access from: localhost(OK)-localhost \[127.0.0.1\]
>>\> EHLO transfusion.vm
250-transfusion.vm Hello localhost \[127.0.0.1\], pleased to meet you
250-ENHANCEDSTATUSCODES
250-PIPELINING
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ETRN
250-AUTH DIGEST-MD5 CRAM-MD5
250-DELIVERBY
250 HELP
>>\> VERB
250 2.0.0 Verbose mode
>>\> MAIL From: SIZE=50 AUTH=root@transfusion.vm
250 2.1.0 ... Sender ok
>>\> RCPT To:<*@gmail.com>
>>\> DATA
250 2.1.5 <*@gmail.com>... Recipient ok
354 Enter mail, end with "." on a line by itself
>>\> .

050 <*@gmail.com>... Connecting to gmail-smtp-in.l.google.com. via esmtp...
050 220 mx.google.com ESMTP t3si9104892qar.125 - gsmtp
050 >>> EHLO transfusion.vm
050 250-mx.google.com at your service, \[2a01:**:****:***::*\]
050 250-SIZE 35882577
050 250-8BITMIME
050 250-STARTTLS
050 250-ENHANCEDSTATUSCODES
050 250 CHUNKING
050 >>> STARTTLS
050 220 2.0.0 Ready to start TLS
050 >>> EHLO transfusion.vm
050 250-mx.google.com at your service, \[2a01:**:****:***::*\]
050 250-SIZE 35882577
050 250-8BITMIME
050 250-ENHANCEDSTATUSCODES
050 250 CHUNKING
050 >>> MAIL From: SIZE=331
050 250 2.1.0 OK t3si9104892qar.125 - gsmtp
050 >>> RCPT To:<*@gmail.com>
050 250 2.1.5 OK t3si9104892qar.125 - gsmtp
050 >>> DATA
050 354  Go ahead t3si9104892qar.125 - gsmtp
050 >>> .
050 550-5.7.1 \[2a01:**:****:***::*\] Our system has detected that this message does
050 550-5.7.1 not meet IPv6 sending guidelines regarding PTR records and
050 550-5.7.1 authentication. Please review
050 550-5.7.1 https://support.google.com/mail/?p=ipv6\_authentication\_error for more
050 550 5.7.1 information. t3si9104892qar.125 - gsmtp
050 ... Connecting to local...
050 ... Sent
250 2.0.0 s2A9ve5k026538 Message accepted for delivery
*@gmail.com... Sent (s2A9ve5k026538 Message accepted for delivery)
Closing connection to \[127.0.0.1\]
>>\> QUIT
221 2.0.0 transfusion.vm closing connection
You have new mail in /var/mail/root