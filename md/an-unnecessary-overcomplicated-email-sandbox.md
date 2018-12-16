# An Unnecessary, Overcomplicated Email Sandbox

_Tristan Goodell on Project, Email | 05 Oct 2018_

The title is pretty self explanatory: this setup is unnecessary and way more complicated than it really needs to be to have proper online security. I would not suggest a replication of this email sandbox strategy simply due to how much of a headache it was to develop and how it (probably) does not actually contribute much to online security.

## The Events Prior to This

On Friday, January 18, 2018 at 7:24 PM, an IP address in Dnipro, Dnipropetrovsk Oblast, Ukraine attempted to break into my primary Google Account. This was not good.

I was using [Lastpass](https://www.lastpass.com/) as my password manager at the time. The password for the almost-compromised Google account was a randomized 64 characters long with both capital and lowercase letters, numbers, and various symbols.

According to [howsecureismypassword.net](https://blog.tgoodell.com/an-unnecessary-overcomplicated-email-sandbox/howsecureismypassword.net), it would take a computer 4 trestrigintillion years to crack the password. That begs the question: how did these hackers get my password? I don't think that they had 4 trestrigintillion to brute force it and I don't know how they could have intercepted it.

And the hackers did have my password; from the testing that I have done, Google only notifies you of a potential login only if a hacker logs into your account from a fishy location or is blocked by two factor authentication.  

Following this event, I performed a self-done security audit: changed passwords, ensured that no other accounts were compromised, double checked that 2FA was enabled on all platforms that offered it (it was), and looked for potential security flaws that could have caused this whole ordeal. There were none. Weird.

This was not the last instance of weird happenings with email accounts, however.

Last Spring, I left the country for about a week. I was without internet during that time period (which was probably a mistake). When I returned, I noticed something odd: I was receiving an error message for the email account that I use for various online accounts. I use [K-9 Mail](https://k9mail.github.io/) as my mobile email client. Connection errors are not unheard of in my experience, so I thought nothing of it at the time. Furthermore, I use [Disroot](https://disroot.org/en) as my email provider which also sometimes has outages (unsure if they are just on my side or theirs).

When I returned home and attempted to diagnose this issue, I was met with unexpected results.

This wasn't good: nearly all of my accounts were tied to this one email account.

When I attempted to reset my password using the [Self Service Password Center](https://user.disroot.org/pwm/private/login), I was greeted with another error.

Not good. When I attempted to send an email to the locked email account, I was given the error `550 5.1.1 : Recipient address rejected: User unknown in virtual mailbox table`. Weird.

I assumed that either (a) someone broke into my presumably secure email account and deleted it or (b) Disroot messed up and removed it for some unknown reason.

Regardless, I wanted a solution that would prevent an account from being compromised, and, at the very least, let me know what happened and why.

## The Plan

Sandboxing with redundancy. Simple as that.

The plan is to use separate email accounts for different purposes and have several mirrors and archives to help ensure that I know what is going on with an email account, even if I do not have access to it.

The design can be separated into three main areas:

1.) Communicative - Personal, school, and work emails ; emails that you expect to need to respond to.

2.) Utility - Online Accounts, Newsletters, and more ; emails that are just there for account confirmation and the receiving of emails. No responses.

3.) Mirrors - Security, Archiving, and simplifying the number of email accounts that you need to keep track of.

---

## Execution

Three dozen accounts are implemented in this design. They are from various providers including Google, Disroot, Tutanota, Zoho, and several others. Each has 2FA enabled and strong passwords. Here is how they roughly pan out:

- 3 Security Accounts - any and all emails that relate to security are passed to these three accounts. For extra redundancy, each account receives security notifications to ensure that I know what occurred in the event of a breach.
- 2 Archive Accounts - all emails are passed through to these accounts as a backup archive.
- 3 School Accounts - these all feed into a mirror to ensure that I receive emails from all three. No, I am not enrolled in three schools; school IT departments just don't delete student emails (even though they no longer have access to domain in the case of one of these).
- 4 Personal Emails - for conversing with the family and friends.
- 13 Miscellaneous Accounts - for newsletters, updates, account notifications, and more. Most of these feed into a pass-through account for simplicity.
- 7 Work Emails - all for the website for different purposes.
- 2 Pass-through accounts - to simplify the Misc accounts.

Grand Total = 36 Email Accounts

---

## Conclusion

At the end of the day, this is an unnecessary, bloated approach to online security. The hassle is most definitely more than it is worth and it offers, at best, minimal security advantages over a simpler approach.

Even though our email account is the key to our entire online existence, 36 emails are overkill. If I were to implement this today, I would have three accounts: (1) Personal to interact with, (2) one for newletters and online accounts, and (3) an archive/security passthrough to ensure that you have a record of any fishy activity with your email accounts.

Some tips:

- Only use your personal account for personal interactions. Don't hand it out to online entities: they will potentially sell your email to advertisers (which opens up the door to spam).
- Make sure to configure automatic forwarding to your security/archive account so that you have a record of what is going on in the event of a security breach.
- Use POP3 for the archive/security account. Depending on the email provider, you can have anywhere between 500MB and 15GB of storage. This can be exhausted quickly if you are not careful. I would suggest that you use a Raspberry Pi or any other computer to use as an email archive machine. The Post Office Protocol Version 3 (POP3) works by downloading your emails to your computer and then deleting them from the server. This means that you can have an offline backup of all of your emails almost instantaneously without having to worry about someone else modifying the contents.  

And of course:

- Use a strong, random password with capital and lowercase letters, digits, and symbols. My go to length is 64 characters, although I do suggest that you use the maximum length if you can.
- Use a password manager like KeepassX, Lastpass, or Bitwarden. I have used all three before. It is really all about preference.
- Use two factor authentication. I use FreeOTP+ on Android. Any 2FA solution would work however.

Good luck!
