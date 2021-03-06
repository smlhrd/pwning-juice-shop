# Weak security mechanisms

## Challenges covered in this chapter

| Challenge                                                                                                                          | Difficulty |
|:-----------------------------------------------------------------------------------------------------------------------------------|:-----------|
| Log in with the administrator's user credentials without previously changing them or applying SQL Injection.                       | 2 of 5     |
| Log in with Bjoern's user account without previously changing his password, applying SQL Injection, or hacking his Google account. | 3 of 5     |
| Inform the shop about a JWT issue. (Mention the exact secret used for the signature in the JWT in your comment.)                   | 3 of 5     |
| Exploit OAuth 2.0 to log in with the Chief Information Security Officer's user account.                                            | 4 of 5     |
| Wherever you go, there you are.                                                                                                    | 4 of 5     |
| Log in with the support team's original user credentials without applying SQL Injection or any other bypass.                       | 5 of 5     |

### Log in with the administrator's user credentials without previously changing them or applying SQL Injection

You might have already solved this challenge along with
[Log in with the administrator's user account](sqli.md#log-in-with-the-administrators-user-account)
if you chose not to use SQL Injection. This challenge can only be solved
if you use the original password of the administrator. If you
_accidentally_ changed the password, do not despair: The original
password will _always_ be accepted to make sure you can solve this
challenge.

#### Hints

* Guessing might work just fine.
* If you harvested the admin's password hash, you can try to attack
  that.
* In case you use some hacker tool, you can also go for a _brute force
  attack_ using a generic _password list_

### Log in with Bjoern's user account

The author of the OWASP Juice Shop (and of this book) was bold enough to
link his Google account to the application. His account even ended up in
the initial user records that are shipped with the Juice Shop for your
hacking pleasure!

> If you do not see the _Log in with Google_ button, do not despair! The
> hostname your Juice Shop is running on is simply not configured in the
> OAuth integration with Google. The OAuth-related challenges are still
> solvable! It might just take a little bit more detective work to find
> out how an OAuth login is handled.

#### Hints

* There are essentially two ways to light up this challenge in green on
  the score board:
  * In case you, dear reader, happen to be Bjoern Kimminich, just log in
    with your Google account to automatically solve this challenge!
    Congratulations!
  * Everybody else might want to take detailed look into how the OAuth
    login with Google is implemented.
* It could bring you some insight to register with your own Google
  account and analyze closely what happens behind the scenes.
* The security flaw behind this challenge is 100% Juice Shop's fault and
  0% Google's.

> The unremarkable side note _**without** hacking his Google account_ in
> the challenge description is _not a joke_. Please do not try to break
> into Bjoern's (or anyone else's) Google account. This would be a
> criminal act.

### Inform the shop about a JWT issue

> JSON Web Token (JWT) is a compact, URL-safe means of representing
> claims to be transferred between two parties. The claims in a JWT are
> encoded as a JSON object that is used as the payload of a JSON Web
> Signature (JWS) structure or as the plaintext of a JSON Web Encryption
> (JWE) structure, enabling the claims to be digitally signed or
> integrity protected with a Message Authentication Code (MAC) and/or
> encrypted.[^1]

OWASP Juice Shop uses JWT in order to identify its users and authorize
them for the more sensitive functions of the shop. Unfortunately when an
appropriate security mechanism is used or implemented improperly, all
its security benefits might be null and void.

#### Hints

* As the challenge description suggests, you need to somehow retrieve
  the secret that is used by the application when tokens are produced.
* For this challenge a brute force attack might be more effective than
  manual attacks or searching for specific exploits.
* The site https://jwt.io proved to be a pretty useful resource

### Exploit OAuth 2.0 to log in with the CISO's user account

You should expect a Chief Information Security Officer to know
everything there is to know about password policies and best practices.
The Juice Shop CISO took it even one step further and chose an
incredibly long random password with all kinds of regular and special
characters. Good luck brute forcing that!

#### Hints

* The challenge description already suggests that the flaw is to be
  found somewhere in the OAuth 2.0 login process.
* While it is also possible to use SQL Injection to log in as the CISO,
  this will not solve the challenge.
* Try to utilize a broken convenience feature in your attack.

### Wherever you go, there you are

This challenge is undoubtedly the one with the most ominous description.
It is actually a quote from the computer game
[Diablo](http://us.blizzard.com/en-us/games/legacy/), which is shown on
screen when the player activates a
[Holy Shrine](http://diablo.gamepedia.com/Shrines_%28Diablo_I%29). The
shrine casts the spell
[Phasing](http://diablo.gamepedia.com/Phasing_%28Diablo_I%29) on the
player, which results in _teleportation_ to a random location.

By now you probably made the connection: This challenge is about
_redirecting_ to a different location.

#### Hints

* You can find several places where redirects happen in the OWASP Juice
  Shop
* The application will only allow you to redirect to _whitelisted_ URLs
* Tampering with the redirect mechanism might give you some valuable
  information about how it works under to hood

> White list validation involves defining exactly what _is_ authorized,
> and by definition, everything else is not authorized.[^2]

### Log in with the support team's original user credentials

This is another _follow-the-breadcrumbs_ challenge of the tougher sort.
As a little background story, imagine that the OWASP Juice Shop was
developed in the _classic style_: The development team wrote the code
and then threw it over the fence to an operations and support team to
run and troubleshoot the application. Not the slightest sign of
[DevOps](https://en.wikipedia.org/wiki/DevOps) culture here.

#### Hints

* The support team is located in some low-cost country and the team
  structure fluctuates a lot due to people leaving for jobs with even
  just slightly better wages.
* To prevent abuse the password for the support team account is very
  strong.
* To allow easy access during an incident, the support team utilizes a
  3rd party tool which every support engineer can access to get the
  current account password from.
* While it is also possible to use SQL Injection to log in as the
  support team, this will not solve the challenge.

[^1]: https://tools.ietf.org/html/rfc7519
[^2]: https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet#White_List_Input_Validation
