# Exodus

People have crowdfunded a [$5000+ bounty][bounty] for an open source
tool that helps influencers export their followers from Twitter to
[Substack][], [Ghost][], [Locals][], or other user-controlled
platforms.

Read on for the problem description and possible solutions. Submit
your example code [here][issue].

Because this is desired by many people, a good solution to this bounty
could become a product or even a startup. You'd want to first get it
to work robustly for Twitter influencers, probably via white glove
service for the first 100 or so accounts. And then make it work for
other social platforms. Companies like [Buffer][] have done
surprisingly well with similar seemingly simple products.

# Problem: exporting followers from Twitter

Twitter is an incredible platform for learning and finding people of
like mind. I admire much of what Jack Dorsey and his team have
accomplished.

However, it has several downsides for users with large follower bases,
as it lacks tools for:

  - distribution: you can't contact all of your followers without permission from Twitter
  - customization: you can't customize the experience for your followers or offer them added benefits
  - monetization: you don't make money as a Twitter influencer, and don't get a storefront to sell things
  - moderation: you can't maintain a civil tone among your community
  - information: you don't have individual-level search and analytics on your follower base
  - prioritization: you can't up- or down-regulate what appears in your feed or that of your followers
  - brand management: you don't control your own brand or domain name, as it's twitter.com/example rather than example.com

For these reasons and more, many people are moving to platforms like
[Substack][], [Ghost][], [Locals][], or the like. In these platforms,
an influencer has full root privileges over their community and can
give a richer experience. You don't need to pay Twitter ads to reach
your followers, or trust that they will deliver your content to their
feed.

The issue, however, is that it's not trivial to export a large
follower base from Twitter!

Note that the problem here is _not_ the export of one's own profile
data. That is relatively easy and [Twitter][twitter-export] already
supports that. The issue is not the _access_ to your own data, the
issue is the ability to _contact_ your followers (eg via email or
phone) without Twitter's additional consent.

# Solution: mass DM with subscribe link?

Here's the ideal: if you have N followers, you get a list of N emails
(or phone numbers) for those followers _with their explicit consent_
to contact them on another platform, and without bothering them very
much or at all. Also, the solution shouldn't take too much time on the
part of the influencer to run and maintain a script.

In theory, Twitter could add a feature where users could opt in to
allowing their emails to be viewed by a few, some, or all of the
accounts they followed, perhaps in return for a micropayment of some
kind. For example, an account could pay $X for the verified email of
each follower with an account age over 3 months and >100 real
followers themselves.

But in the absence of a built-in feature like this, there are several
overlapping ways to export your userbase to example.com/subscribe.

1. Put example.com/subscribe in your name, bio, photo, and profile
2. Create a pinned tweet directing your followers to example.com/subscribe
3. Regularly post a tweet with example.com/subscribe
4. [Publicly tweet][mention] to each follower with example.com/subscribe
5. Set up a separate new account that does #1-4, to keep the public mentions out of your timeline
6. Parse the bios of each follower account for public contact info (eg if they have their email in their bio), and email them out-of-band with example.com/subscribe
7. Set up a [welcome message][] with example.com/subscribe for each new follower
8. Privately DM each follower _once_ with example.com/subscribe

None of these are perfect. But the last one seems like it has the
right balance of being reasonable (a single DM to someone who has
chosen to follow you is not unreasonable) and in theory relatively easy to
automate.

In particular, Twitter has a bunch of tools for corporations to do
customer service [via DM][dm-api] that might be repurposed for this use case.

## Bounty: $5000 bounty for open source mass DM tool

Here is a [thread][first-thread] with context on the initial
bounty.

### Bounty logistics
Enough other people were interested in this that the bounty
rose to [$4350][bounty-increase] and then above $5000 quickly.

In terms of mechanics, I (@balajis) will decide on the winner by June
21, 2020, and then the BTC address of the winner will be provided to
the various people who have publicly supported the bounty.

It will be incumbent upon each of these people to pay what they have
committed to the winner. They can optionally publicly post an on-chain
confirmation.

# FAQ

## How to submit an entry for the bounty?
Go to this [issue][] and make a comment with a link to
your project. Ideally it should have a gif or something that shows
that it works.

## What about other approaches?
As noted above, the ideal is that if you have N followers, you get a list of
N emails (or phone numbers) for those followers _with their explicit
consent_ to contact them on another platform, and without bothering
them very much or at all, or requiring too much time on the part
of the influencer to run or maintain a script

If you can achieve this goal another way, that's fine.

## What about Twitter API and DM limits?
These are a critical constraint. If you have a solution that works in theory, but that
breaks on accounts with many followers, or gets an account banned or shadowbanned for spam,
or has some other serious negative side effect, then you don't have a solution.

## Can the tool run for multiple days?
Yes, Twitter's default API has a 1000-daily-DM limit. So your tool might need to run
for multiple days.

The open source version would run locally and have some state, like a
SQLite database or a flatfile. It would use that state to record what
people it had DM’d and when, along with what was said and whether they
responded. You should also allow re-running of the tool periodically
as new followers arise, without requiring the influencer to think
about whether they are inadvertently messaging people they already
messaged.

## Can the tool require something above the basic API?
Maybe, so long as that API access isn't too expensive or time
consuming to get for the typical Twitter influencer with (say) 10,000
followers.

The [DM API][dm-api] for customer service seems like it might be quite relevant.

## Can the tool be command line only?
That's the simplest version, but ideally there should be a simple Mac
app and a hosted version as well.

 - The command line version would be for developers.

 - The Mac app would be for folks who aren't developers, but don't
   want to give their Twitter credentials out to a new website. They'd
   prefer to paste in an API key locally.

 - The hosted version will probably be the most widely used, where
 someone logs in with Twitter OAuth and sets up this mass DM to
 run in the background, with analytics on who has been contacted,
 who signed up, and so on.

However, because there are many fly-by-night Twitter apps, and because
of the nature of what this app is doing (mass DM of followers), the
influencer will want to carefully babysit it and the presence of the
open source versions will increase trust in the hosted version.

## What about existing tools?
Here are a few that are relevant:

- Example of using Python API to extract followers: [get_followers_bios.py][]
- Example of getting followers _without_ official API: [Twint][]
- Command line tool for interacting with Twitter: [t][]

There are tons of open source tools for working with Twitter out there
on GitHub and the broader internet. Feel free to use them rather than
reinventing the wheel.

# Next steps
The problem of exporting your following applies to all social media,
and has been discussed for the better part of a decade, but it now
feels like it's gotten to a boil. There is a critical mass of people
who are moving to platforms like Substack, Ghost, and Locals that
offer greater control over your audience (and, with it, monetization
for the influencer and benefits for the audience).

If we can solve it for Twitter, we can probably generalize this to
work for _partial_ exodus of influencers from other platforms like
Facebook and Instagram.

Please note that Twitter and company won't go away any time soon.
This is a [cave-and-commons][] setup. The large global social networks
will likely persist for some time as "commons" where you recruit
members, but these "caves" off to the side with individual communities
will thrive.



# References
[Substack]: https://substack.com
[Ghost]: https://ghost.org
[Locals]: https://locals.com
[twitter-export]: https://help.twitter.com/en/managing-your-account/how-to-download-your-twitter-archive
[bounty]: https://twitter.com/balajis/status/1271945241881268224
[mention]: https://help.twitter.com/en/using-twitter/mentions-and-replies
[first-thread]: https://twitter.com/balajis/status/1271945241881268224
[issue]: https://github.com/balajis/twitter-export/issues/1
[bounty-increase]: https://twitter.com/balajis/status/1271975948846415872
[get_followers_bios.py]: https://gist.github.com/raulgarreta/64b4daaf5295b5a95dd09718ac7512f7
[Twint]: https://github.com/twintproject/twint
[t]: https://github.com/sferik/t
[welcome message]: https://developer.twitter.com/en/docs/direct-messages/welcome-messages/guides/setting-default-welcome-message
[dm-api]: https://developer.twitter.com/en/products/direct-messages
[Buffer]: https://buffer.com/press/buffer-expands-brand-building
[cave-and-commons]: https://hbr.org/2013/03/give-workers-the-power-to-choose-cave
