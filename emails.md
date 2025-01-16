# Emails

## Emails with luring keywords

The email subject has a number of keywords that are meant to lure the user in opening the email

```
EmailEvents
| where Subject has_any('trial', 'free', 'demo', 'membership', 'premium', 'gold', 'notification', 'notice', 'claim', 'order', 'license', 'licenses')
| summarize count() by Subject
| sort by count_ asc
```
