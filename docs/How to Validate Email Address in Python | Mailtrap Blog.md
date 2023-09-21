---
tags:
  - programming
share: "true"
---
#programming

Source: Unknown (not mine).

When you gather emails from your users or visitors, you want to make sure they’re valid and functional. Otherwise, you risk cutting users off from their accounts or cluttering your database with fake addresses you’ll have no use for. Luckily, there are several fairly obvious approaches to validating emails in Python.

Why bother, though, one might ask. There’s plenty of significant reasons behind having proper validation in place:

### Sending emails to fake/no-longer-existent addresses will hurt your deliverability.

When you’re, for example, offering access to free Wi-Fi or an online resource in exchange for someone’s email address, some (many) users will provide fake addresses. Some others will use a disposable, 10-minute-mail account that will be gone by the time you finish your morning coffee. Each message resulting in a [hard bounce,](/blog/soft-vs-hard-bounce/) will increase the chance of emails sent to legitimate addresses going to spam or bouncing as well. 

In all honesty, nearly always I leave a wsbfre@fwejfb.com-type of email address when forced to sign in to airport Wi-Fi. And I’m sure most fellow travelers do the same. Whoever tries to utilize this database without any validation must be enjoying some pretty dramatic delivery rates.

### Mistyping an email address will block users from confirming their account or resetting a password.

There will always be typos and large databases will be flooded with the kind of “gmial.com” or “outlook.con” addresses if no validation is in place. If your app accepts that kind of addresses without a blink of the (virtual) eye, users might be effectively locked out of their account before they even access it for the first time. Your [confirmation emails](https://mailtrap.io/blog/confirmation-emails/) will bounce too, further hurting your deliverability.

### It lets you stay in touch with users 

Having a valid email address lets you reach them on any occasion. You can chase them when they abandon their card or a payment fails or just keep them in the loop about features and tips. If an email address is all they provide at registration, you don’t want to have an invalid one on your records.

## Python options to validate an email address

It’s important to note that there’s no 100% error-proof method of validating emails other than just emailing a user. And for the top reason stated above, you shouldn’t do it. But the methods we’re going to present are quite effective and have saved thousands of Python devs from collecting useless addresses.

### Validating emails with a regex

The first approach is to use a regex in Python. It will check inserted addresses for certain conditions and return a “valid” or “invalid” response.

**Example 1: **

This regex checks if an email address has a proper format. It also verifies if the top-level domain length is between two and four characters. You might want to raise the final number to a higher value to include top-level domains such as .travel, but that might also lead to some false positives.
```
^[w-.]+@([w-]+.)+[w-]{2,4}$
```
This script is not any good for catching typos or fake email addresses such as !32d!3@dfsjn@dwef.com, but it will do for a very basic check.


**Example 2:**







Let’s make it more sophisticated and assume we want the following criteria to be met for an account@domain email address:







* Both consist of case-insensitive alphanumeric characters. Dashes, periods, hyphens or underscores are also allowed
* Both can only start and end with alphanumeric characters
* Both contain no white spaces
* _account_ has at least one character and domain has at least two
* _domain_ includes at least one period
* And of course, there’s an ‘@’ symbol between them







```
^[a-z]([w-]*[a-z]|[w-.]*[a-z]{2,}|[a-z])*@[a-z]([w-]*[a-z]|[w-.]*[a-z]{2,}|[a-z]){4,}?.[a-z]{2,}$
```

This is also a basic regex, and it will still capture some fake addresses. Although .com, .org or .net domains need to be two or more characters long, many other top-level domains will allow just one character to be present. For example, Google’s Chinese domain, g.cn, would fail this test, but emails sent to big_brother@g.cn may just reach the target.
Above all, this regex completely ignores 99.9% of typos, making it ineffective as a standalone solution.

**Example 3:**
Since the other two examples did almost nothing about typos, you can also include another condition for popular email providers, such as Gmail:

```python
import re
example = "example@gmial.com"
if re.search("@gm(ia|a|i)l.com$", example):
print("Maybe you meant @gmail.com?")
```

If the domain name is gmial.com, gmal.com or gmil.com (very very likely indicating a Gmail account) then we can show a warning to the user.
Of course, to validate all possible typos, more sophisticated methods should be used, but listing the most common typos might just do the job.
Be aware that however sophisticated regex you write, it will eventually fail for some legitimate email. Read more about the possible trade-offs [here](https://www.regular-expressions.info/email.html). If you don’t require perfect accuracy, a script will do for your needs.
### Validating emails with Python libraries
Another way of running sophisticated checks is with ready-to-use packages, and there are plenty to choose from. Here are several popular options:

[email-validator 1.0.5](https://pypi.org/project/email-validator/)
This library focuses strictly on the domain part of an email address, and checks if it’s in an x@y.com format. 
As a bonus, the library also comes with a validation tool. It checks if the domain name can be resolved, thus giving you a good idea about its validity.


[pylsEmail 1.3.2](https://pypi.org/project/pyIsEmail/#description)
This Python program to [validate email addresses](https://mailtrap.io/blog/verify-email-address-without-sending/) can also be used to validate both a domain and an email address with just one call. If a given address can’t be validated, the script will inform you of the most likely reasons.

[py3-validate-email](https://pypi.org/project/py3-validate-email/)
This comprehensive library checks an email address for a proper structure, but it doesn’t just stop there.
It also verifies if the domain’s MX records exist (as in, is able to send/receive emails), whether a particular address on this domain exists, and also if it’s not blacklisted. This way, you avoid emailing blacklisted accounts, which would affect deliverability.
### Validating emails with an external API
Finally, there’re also a number of APIs you can use with your Python app. Here are some popular choices:

[Mailboxlayer](https://mailboxlayer.com/)
This REST API verifies the format of each email. Like the libraries we just talked about, it also verifies if MX records exist and if an address is disposable. It offers a score for each email address checked.
Mailboxlayer is free to use with up to 250 requests per month. If you need more than that, the plans start from $9.99 per month with additional functionality available.

[Isitrealemail](https://isitarealemail.com/)
This simple API checks for SMTP servers on the domain provided. It then verifies if an email address exists in this domain.
100 requests/day are offered for free. You then pay $3 for every 5,000 requests, with no subscription plan.

[Sendgrid’s Email Validation API](https://sendgrid.com/solutions/email-validation-api/)
This sophisticated API runs a number of checks to determine a score for each email address. It checks, as predecessors on this list, for MX records, and also looks for A records. SendGrid will also easily track down disposable and role addresses (admin@, support@ etc.)
SendGrid claims to use machine learning to determine the likelihood of a bounce, and with the amount of data they have at their disposal, these might prove to be pretty accurate predictions.
Sendgrid’s Email Validation API is only available to its customers on paid plans. For detailed pricing and a calculator, consult their page.

### Other methods for validating emails
Many ESPs will incorporate their own techniques for validating emails. They may be more sophisticated than the scripts we listed above, but won’t be bullet-proof (until an email is sent).
If you’ve already accumulated a list of email addresses and want to validate them in bulk, there are a number of free tools, such as [ValidateEmailAddress.org](https://validateemailaddress.org/) or [emailvalidator.co.](http://www.emailvalidator.co/) You upload your list of contacts and, for each, they will return either of the following results:
* **Valid** – the address exists and is very likely to accept your emails
* **Risky** – the address exists, but there are factors that could still lead messages to bounce
* **Invalid** – the address is invalid, as it contains errors, whether it is in syntax, DNS or a mailbox.
## Other considerations
Validating emails is just one aspect of [successful email campaigns in Python](/blog/sending-emails-in-python-tutorial-with-code-examples/). Another is testing if emails are sent out as expected. This is something that Mailtrap can help you with.
[Mailtrap](https://mailtrap.io) is an environment for pre-production email testing. You route your test emails to your Mailtrap inbox so you inspect them, check them against spam filters and improve them before they’re sent to real users.
[Try Mailtrap for Free](/register/signup)

You can also choose to **bcc Mailtrap on real emails** so you can get a copy of each in your fake inbox. This way, you’ll immediately spot when something is wrong and will be able to react before more damage is done.

