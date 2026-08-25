### Cloud Init Formatting:
```
--===============0266095039302191565==
Content-Type: text/plain; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="pre-config.txt"

### Pre License Validation CLI Commands

--===============0266095039302191565==
Content-Type: text/plain; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="license-token.txt"
 
### License (BYOL or FortiFlex)
 
--===============0266095039302191565==
Content-Type: text/plain; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="post-config.txt"

### Post License Validation CLI Commands
 
--===============0266095039302191565==--
```

### Info
- Before and after the first FortiOS CLI commands, there should be a break (empty line).
- "next" and "end" needs to be accurately configured.
- Variables used within the cloud-init file must be parsed within the Terraform based VM creation process.

### FortiFlex Example
```
--===============0266095039302191565==
Content-Type: text/plain; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="license-token.txt"
 
LICENSE-TOKEN:ABCDEFG123456
 
--===============0266095039302191565==
```

### Troubleshooting
```
diag debug cloudinit show
```
Shows the order of the performed commands from the cloud-init file.
