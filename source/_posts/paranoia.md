---
title: Paranoia
url: 95.html
id: 95
categories:
  - Messaging
date: 2013-11-30 13:09:15
tags:
---

[https://github.com/n0g/arcane](http://github.n0g.at/arcane "Don't let *them* read your mail. Encrypt it now.  http://github.n0g.at/arcane")

$ torsocks ./arcane --hostname xxxmailserver.onion --username
yourusername --key AAAAAAAA

IMAP4 Password:
IMAP Server: xxxmailserver.onion
IMAP Port: 143
IMAP SSL: False
IMAP Username: yourusername
IMAP Mailbox: "INBOX"
.

IMAP Server: xxxmailserver.onion
IMAP Port: 143
IMAP SSL: False
IMAP Username: yourusername
IMAP Mailbox: "INBOX.Trash"


IMAP Server: xxxmailserver.onion
IMAP Port: 143
IMAP SSL: False
IMAP Username: yourusername
IMAP Mailbox: "INBOX.Sent"


IMAP Server: xxxmailserver.onion
IMAP Port: 143
IMAP SSL: False
IMAP Username: yourusername
IMAP Mailbox: "INBOX.Drafts"

A note: you can compile torsocks in a VM like virtualbox and edit /usr/local/etc/torsocks.conf to point to the tor daemon running on the host. In VBox's NAT networking mode the host can be accessed through the gateway IP.