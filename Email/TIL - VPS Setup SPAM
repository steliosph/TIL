##  TIL - Email Setup X-SPAM
Setting up an email for VPS ended up being rather on the easy site.
I have recently migrated all of my websites from my reseller account to a VPS, and so i had to deal with all of the server "handling"

After some searching i ended with Linode. Until know everything is perfect.

With the guide at there website
https://linode.com/docs/email/email-with-postfix-dovecot-and-mysql
i have managed to set up the email server linked to a database where i can easily add manage users.

I believed everything was running smoothly until the day i noticed that my emails at the major Email providers were not being delived.

It appears that i was marked as SPAM.
The emails that i have been sending had the following in there headers
tests=[BAYES_40=-0.001, MISSING_MID=0.497, MISSING_MIMEOLE=1.899, SPF_PASS=-0.001, XPRIO=1.999]
BAYES_40 = This is the history of the email that if it has been previously marked as SPAM it will get a higher score.
MISSING_MID = The email header. All proper emails should contain the Message-Id headers
MISSING_MIMEOLE = The message is pretending to be generate by a MS email program and uses the X-MSMail-Priority header but is missing the X-MimeOLE which is a Microsoft email characteristic.
SPF_PASS = A method to prevent sender address forgery.
XPRIO = ??


From here i had a rather high Spam Value.
X-Spam-Score: 4.393
You definetely want to keep that below the 4.0.
The one thing that we could try and remove was the microsoft MIMEOLE with a High value of 1.899
This was adding in my email headers the following 
X-Priority: 3
X-MSMail-Priority: Normal


In my postfix directory $ /etc/postifix/
i have created the following file : header_checks 
with the text 
```
/^X-MimeOLE:/   IGNORE
/^X-MSMail-Priority:/   IGNORE
```

And added the the checks in the  main.cf
```
# Header Check
header_checks = regexp:/etc/postfix/header_checks
```



This has removed the MIMEOLE problems and have droped my X-Spam-Score down to 2.8.






