# asterisk

# CONF-FILES

```
root@861ff513557f:/# cat /etc/asterisk/sip.conf 
;
; SIP Configuration example for Asterisk
;
; Note: Please read the security documentation for Asterisk in order to
; 	understand the risks of installing Asterisk with the sample
;	configuration. If your Asterisk is installed on a public
;	IP address connected to the Internet, you will want to learn
;	about the various security settings BEFORE you start
;	Asterisk.
;----------------------------





[1001]
type=friend
username=1001
secret=1001
context=public
host=dynamic
callerid="max"
mailbox=1001@default



[1002]
type=friend
username=1002
secret=1002
context=public
host=dynamic
callerid="phil"
mailbox=1002@default
```
## Extensions.conf
------------
```
root@f2ae1345f263:/# cat /etc/asterisk/extensions.conf 
; extensions.conf - the Asterisk dial plan
;
; Static extension configuration file, used by
; the pbx_config module. This is where you configure all your
; inbound and outbound calls in Asterisk.
;
; This configuration file is reloaded
; - With the "dialplan reload" command in the CLI
; - With the "reload" command (that reloads everything) in the CLI

;
; The "General" category is for certain variables.

[ani]
exten => _X.,40000(ani),NoOp(ANI: ${EXTEN})
exten => _X.,n,Wait(0.25)
exten => _X.,n,Answer()
exten => _X.,n,Playback(vm-from)
exten => _X.,n,SayDigits(${CALLERID(ani)})
exten => _X.,n,Wait(1.25)
exten => _X.,n,SayDigits(${CALLERID(ani)})	; playback again in case of missed digit
exten => _X.,n,Return()

; For more information on applications, just type "core show applications" at your
; friendly Asterisk CLI prompt.
;
; "core show application <command>" will show details of how you
; use that particular application in this file, the dial plan.
; "core show functions" will list all dialplan functions
; "core show function <COMMAND>" will show you more information about
; one function. Remember that function names are UPPER CASE.


[public]
exten => 1001,1,Dial(SIP/1001)
exten => 1002,1,Dial(SIP/1002)
----------------------------------


```


