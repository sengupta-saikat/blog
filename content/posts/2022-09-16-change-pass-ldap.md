---
title: "Change Password of Active Directory Accounts via LDAP"
author: ["Saikat"]
date: 2020-08-15
draft: false
description: "All the front matter variables available in Congo."
slug: "getting-started"
tags: ["installation", "docs"]
categories: ["TIL"]
---

## Overview
I recently had 

## Code

```py
import ldap


def update_pass():
    ad_server = "ldaps://ldap.server.com"
    ad_dn = "CN={0},OU=xx,DC=yy,DC=zz,DC=org"

    username = 'my-username'
    old_pwd = 'my-old-passwd'
    new_pwd = 'my-new-passwd'

    # LDAP connection initialization
    ldap_conn = ldap.initialize(ad_server)
    # Set LDAP protocol version used
    ldap_conn.protocol_version = ldap.VERSION3

    # Bind
    ldap_conn.simple_bind_s(ad_dn.format(username), old_pwd)

    # Now, perform the password update
    old_pwd_utf16 = '"{0}"'.format(old_pwd).encode('utf-16-le')
    new_pwd_utf16 = '"{0}"'.format(new_pwd).encode('utf-16-le')

    mod_list = [
        (ldap.MOD_DELETE, "unicodePwd", old_pwd_utf16),
        (ldap.MOD_ADD, "unicodePwd", new_pwd_utf16),
    ]

    ldap_conn.modify_s(ad_dn.format(username), mod_list)
    print("Password successfully updated.")


if __name__ == '__main__':
    update_pass()
```

## Conclusion
So this is it