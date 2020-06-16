# A $10000 BTC Bounty for an open source tool to export your Twitter followers

![Twitter export to email](./img/twitter-to-email.png)

The community has crowdfunded a [$10000 bounty](#bounty-commits),
payable in BTC, for an open source tool that helps people export their
followers from Twitter to [Substack][], [Ghost][], [Locals][], or
other user-controlled platforms.

 - **Submit your bounty entry [here][issue]**
 - Read on for detailed problem description and possible solutions

The goal is to take a Twitter account with N followers and produce a
list of N emails (or phone numbers) for those followers _with their
explicit consent_ to contact them on another platform, and without
bothering them very much or at all. The ideal solution shouldn't
take too much time or money on anyone's part.

There are many possible approaches to this problem, and the best one
will win the first $10k [committed](#bounty-commits). With any
remaining monies, we'll fund testing and/or second and third place
prizes.

We care more about the results than the method. We are not going to be
prescriptive about the best approach to take, though we do suggest two
possible ideas below, the "[mass DM](#the-mass-dm-approach)" and
"[affiliate link](#the-affiliate-link-approach)" approaches.

How do we determine the "best" approach? We are thinking about
[scoring](#bounty-scoring) the different approaches by allowing
different accounts to try out the top submissions on a subset of 1000
followers, and then rating them by conversion percentage,
cost-per-conversion, ease-of-use, and happiness-of-converted-user.

Because a tool like this is desired by many people, a good solution to
this bounty could become a product or even a startup. You'd want to
first get it to work robustly for Twitter influencers, probably via
white glove service for the first 100 or so accounts. And then make it
work for other social platforms. Companies like [Buffer][] have done
surprisingly well ($20M+ ARR!) with similar seemingly simple products
that fill a hole in the social networking landscape.

# Problem: exporting followers from Twitter

Twitter is an incredible platform for learning and finding people of
like mind. I admire much of what Jack Dorsey and his team have
accomplished.

However, it has several downsides for users with large follower bases,
as it lacks tools for:

  - **distribution**: you can't contact all of your followers without permission from Twitter
  - **customization**: you can't customize the experience for your followers or offer them added benefits
  - **monetization**: you don't make money as a Twitter influencer, and don't get a storefront to sell things
  - **moderation**: you can't maintain a civil tone among your community
  - **information**: you don't have individual-level search and analytics on your follower base
  - **prioritization**: you can't up- or down-regulate what appears in your feed or that of your followers
  - **brand management**: you don't control your own brand or domain name, as it's twitter.com/example rather than example.com

For these reasons and more, many people are moving to platforms like
[Substack][], [Ghost][], [Locals][], or the like. In these platforms,
an influencer has full root privileges over their community and can
give a richer experience. You don't need to buy Twitter ads to reach
your followers, or trust Twitter to deliver your content to your
followers' feeds.

The issue, however, is that it's not trivial to export a large
follower base from Twitter!

Note that the problem here is _not_ the export of one's own profile
data. That is relatively easy and [Twitter][twitter-export] already
supports that. The issue is not the _access_ to your own data, the
issue is the ability to _contact_ your followers (eg via email or
phone) without Twitter's additional consent.

# Solution

As noted above, the ideal is for an account with N followers to get a
list of N emails (or phone numbers) for those followers _with their
explicit consent_ to contact them on another platform, and without
bothering them very much or at all. In practice, you won't get all N,
but you may get a subset. Also, the ideal solution shouldn't take too
much time or money on anyone's part.

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
9. Generate a per-user affiliate referral link, and pay follower to refer others

None of these are perfect. You might want to use several of them at
the same time. But let's discuss the last two in some detail.

## The Mass DM Approach
The concept here is to send a private DM to each of your followers
with a link (and possibly some incentive) to sign up for a new
platform, like Substack.

The simplest way to implement the mass DM approach might be a command
line app that takes as input a Twitter API key and a message to send
each user. It would give you a preview of all of your followers,
addsome options to rank them by importance, and let you try it out by
sending test messages to a few accounts before opening it up to
message 1000 accounts per day. It stores state so you know who you
messaged in the past, such that you don't inadvertently recontact
them.

You can imagine a fancier local Mac App that puts a nice GUI on top of
the command line engine described above. Or an even fancier hosted
version with individually attributable conversion links, so you know
which usernames converted to which emails. The hosted version would
also allow you to keep running the 1000 DMs per day in the background,
so it could be a SaaS service.

## The Affiliate Link Approach

This is a very different approach. The idea here is to make export
from social networks as organically viral as the original import was.

One way of doing that is to generate an affiliate link for each
follower, such that the one who refers the most/best users to your
site each day receives $100 in crypto.

Why "most/best"? Because you want some measure of quality, not just N spam emails.
Why crypto? Because it's easy to automate small, fast, international payouts.

A major advantage of this approach is that it can generalize to other
social networks. It's also much harder to shut down than mass DM, and
it aligns the crowd with you economically.

Here's one possible flow, in which all emails are recorded at a single
site that tracks everything and then re-exported into Substack, Ghost,
Locals, Mailchimp, or other applications. Note that this will work for
_free_ email lists, but the upsell to paid subscriptions as per
Substack would then have to be done separately as this implementation
doesn't also include a checkout flow.

Feel free to modify this.

### Phase 1: Set up referral URL
Suppose we define three parties: the developer, the influencer who
wants to export their followers, and each follower themselves.

- The developer sets up a site at (say) `socialexporter.com`
- It says EXPORT YOUR FOLLOWERS
- An influencer lands on this page and logs in with their Twitter account
- The influencer gets a public page generated for them at `socialexporter.com/username`
- The influencer can admin this page at `socialexporter.com/username/settings`
- This public page has some copy asking a user to sign up and explaining where their email will be used (eg Substack, Mailchimp, etc)
- It also has a small form where a follower can enter their email address
- After this email address is entered, a second small form is displayed where a follower can optionally generate an affiliate URL (more on that below)
- And a link appears to `socialexporter.com/username/leaderboard`, which shows a leaderboard of which followers referred which emails (all zero at the start)
- Separately, when logged in, the influencer sees a different private page with all their followers (kind of like [Social Blade][social-blade-jack])
- The private page also has a Bitcoin address to deposit funds
- The influencer sends (say) $1000 to that address to fill up the referral budget
- And the influencer sets a daily budget of (say) $100 for payouts, and can edit the copy on the private page

At this point the influencer has written copy encouraging users to
sign up with their email, as well as allocated a budget to incentivize
this action.

### Phase 2: Post referral URL

Now the influencer incentivizes their audience to refer people.

- The influencer tweets out `socialexporter.com/username` along with a message
- "Hey, I'm setting up my mailing list. You can sign up here and get paid to refer others: socialexporter.com/username"
- A Twitter user sees this tweet and visits `socialexporter.com/username`
- At first they just see copy encouraging them to sign up to the `username` email list and where it will be used (eg Substack, Mailchimp, etc)
- After they enter their email, they then see a second small form where they can optionally generate an affiliate URL
- The site may require them to be a follower of `twitter.com/username` for this affiliate link to work, not just a random user
- It's a [bit.ly-like](https://bit.ly) URL generator where they can type in their Twitter username to generate an affiliate link
- So a follower named `foobar` would get an affiliate URL like `socialexporter.com/username?referer=foobar`
- A user who landed on the site through this affiliate URL and then entered in a quality email would give `foobar` credit on the socialexporter.com leaderboard
- Anyone can view this leaderboard at `socialexporter.com/username/leaderboard` to see themselves alongside the top referers for the day for this username, ranked by the number of quality emails they've referred, similar to [pioneer.app](https://pioneer.app/leaderboard#global)
- Quality can be determined by something like [kickbox.com][] or something more sophisticated, to filter out fake signups

### Phase 3: Payment
Every 24 hours, the socialexporter.com site issues payments to the top referers.

- First, all emails are analyzed for quality using a tool like [kickbox.com][] or more sophisticated custom code
- You might require an email validation, for example, or similar criteria to consider an email to be "high quality"
- Once you have the number of quality emails referred by each user over the last 24 hours, payouts are calculated
- In one model, 50% of the payouts are proportional and 50% are a prize to the best referrer
- So if there were three referers who referred 30, 20, and 10 quality emails respectively, along with a daily prize of $100, the first referer would get $50 + (30/60)($50), the second would get (20/60)($50), and the third would get (10/60)($50).
- These payouts would be sent to the Bitcoin addresses on file every 24 hours
- If transaction fees are too high, payments can be batched, sent via an off-chain method like Coinbase, or sent via another cryptocurrency
- In this fashion one can make fast, international, automated, small payments to users for decentralized work

### Phase 4: Tokenization

Note that the affiliate link approach, unlike the mass DM approach,
is more general (as it works across social networks) and doesn't make
use of the Twitter API. However, it does cost some money to operate. A
variation of this method would allow the influencer to compensate
users in a new cryptocurrency issued for the purpose (such as Reuben's
Bramanathan's [personal token][]).

Note that this whole user story is just a sketch of an incentivized
social referral model for viral export. It can be modified in many
ways.

# Bounty: $10000 bounty for open source Twitter export tool

Here are threads with context on the bounty:

- [Initial thread][initial-thread]
- [First followup][followup1], with increased bounty
- [Second followup][followup2], with affiliate link approach
- [Third followup][followup3], with updated writeup and scoring method

Please follow [@balajis][] for future updates.

## Bounty Scoring
As noted above, we are thinking about scoring the different approaches
by doing two passes.

**First pass**: identify promising submissions versus those which are
obviously buggy by looking at the code, polish, visuals, etc.

**Second pass**: work with volunteer accounts to try out the top
submissions on a subset of ~1000 followers and rate each submission by
conversion percentage, cost-per-conversion, ease-of-use, and
happiness-of-converted-users.

Let's define these terms.

 - conversion percentage: out of N followers, the percentage that submit their emails (eg 10%)
 - cost-per-conversion: the amount of money paid to convert emails divided by the total number of emails collected by the end of the campaign
 - ease-of-use: self-reported subjective measure by the influencer who set up the campaign
 - happiness-of-converted-users: self-reported subjective measure by the users who were pinged to submit their emails

Assume that the only emails that count are those that are above a
quality bar, as measured by [kickbox.com][] or a similar set of
quality filters. It goes without saying (but we're saying it) that all
users must consent to submitting their emails, ideally via email
verification or some other form of demonstrated consent (such as
clicking a link and manually submitting their email).

We're open to feedback on this scoring system, but it appears to
capture the spirit of "export Twitter followers to an email list"
without being prescriptive on the exact method.

## Bounty Commits
Enough other people were interested in this that the total bounty
funds are now >$10000 as of Monday June 15, 2020.

As more money comes in beyond $10,000, we will allocate the first
$10,000 to the winner. We'll then allocate remaining monies to folks
who test out the app and/or possibly to second and third place
submissions.

- [$1000 from @balajis](https://twitter.com/balajis/status/1271945241881268224)
- [$1000 from @ameensol](https://twitter.com/SpankChain/status/1271949898548514816)
- [$1000 from @shervin](https://twitter.com/shervin/status/1272166171924557824)
- [$1000 from @maxua](https://twitter.com/maxua/status/1272040978816339968)
- [$500 from @seanlinehan](https://twitter.com/seanlinehan/status/1271951229602590720)
- [$500 from @stevecarrera](https://twitter.com/stevecarrera/status/1272167907447861249)
- [$200 from @kiko_himself](https://twitter.com/kiko_himself/status/1271972879337435138)
- [$150 from @deconstructized](https://twitter.com/deconstructized/status/1271949110271021056)
- [$2000 from @richardheartwin](https://twitter.com/RichardHeartWin/status/1272195436766474242)
- [$100 from @allenday](https://twitter.com/allenday/status/1272192331458867202)
- [$150 from @paulyacoubian](https://twitter.com/PaulYacoubian/status/1272193951273975809)
- [$250 from @zosegal](https://twitter.com/zosegal/status/1272261575416492032)
- $1000 from anon1
- $1000 from anon2
- $500 from anon3
- $1000 from anon4
- $1000 from anon5

## Bounty Logistics

In terms of mechanics, I (@balajis) will decide on the winner by June
28, 2020, and then the BTC address of the winner will be provided to
the various people who have publicly supported the bounty.

It will be incumbent upon each of these people to pay what they have
committed to the winner. They can optionally publicly post an on-chain
confirmation.

# FAQ

## How to submit an entry for the bounty?
Go to this [issue][] and make a comment with a link to
your project. Ideally it should have a gif or something that shows
how it works.

## What about other approaches?
As noted above, the ideal is that if you have N followers, you get a list of
N emails (or phone numbers) for those followers _with their explicit
consent_ to contact them on another platform, and without bothering
them very much or at all, or requiring too much time or money on the part
of the influencer.

If you can achieve this goal another way besides the mass DM or
affiliate link approach, that's fine. We'll score them as per the
[bounty scoring](#bounty-scoring) section by running them on a subset
of followers.

## What about Twitter API and DM limits?
These are a critical constraint. If you have a solution that works in theory, but that
breaks on accounts with many followers, or gets an account banned or shadowbanned for spam,
or has some other serious negative side effect, then you don't have a solution.

## What about existing tools?
Here are a few that are relevant:

- Example of using Python API to extract followers: [get_followers_bios.py][]
- Example of getting followers _without_ official API: [Twint][]
- Command line tool for interacting with Twitter: [t][]

There are tons of open source tools for working with Twitter out there
on GitHub and the broader internet. Feel free to use them rather than
reinventing the wheel.

## Mass DM specific questions
As noted, there are multiple possible approaches to this problem
including the "[mass DM](#the-mass-dm-approach)" and
"[affiliate link](#the-affiliate-link-approach)" approaches, as well
as something creative you might come up with. If you take the mass DM
approach, here are some answers to FAQs.

### If I do the mass DM approach, can it be command line only?
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

### Why would ranking followers be important for the mass DM approach?
Because you can only send 1000 DMs per day, you will want to
prioritize your followers such that you export the most important ones
first. These might be the ones who have the most followers themselves,
or who have some attribute in their bio (like a #Bitcoin hashtag), or
that have some other criteria. In practice this means that you'll
likely want a _follower table_, where the first column is the Twitter
username and subsequent columns are metadata on that username (along
with a timestamp for when that metadata was last collected, as it can
become stale as people update their profiles).

### Can the mass DM tool run for multiple days?
Yes, Twitter's default API has a [1000-daily-DM limit][dm-limits]. So
your tool might need to run for multiple days.

The open source version would run locally and have some state, like a
SQLite database or a flatfile. It would use that state to record what
people it had DM’d and when, along with what was said and whether they
responded. You should also allow re-running of the tool periodically
as new followers arise, without requiring the influencer to think
about whether they are inadvertently messaging people they already
messaged.

### Can the mass DM tool require something above the basic API?
Maybe, so long as that API access isn't too expensive or time
consuming to get for the typical Twitter influencer with (say) 10,000
followers.

The [DM API][dm-api] for customer service seems like it might be quite relevant.

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

Please note that Twitter and company will be fine and won't go away any time soon.
This is a [cave-and-commons][] approach. The large global social networks
will likely persist for some time as "commons" where you recruit
members, but these "caves" off to the side with individual influencer-led communities
will thrive.

Finally, as noted above, companies like Buffer that solve seemingly simple problems 
like this have gotten to $20M+ in ARR. If you can build and maintain a tool that reliably exports
a large percentage of follower emails from Twitter and other social networks, with the consent of the users and at a reasonable price, you have something that a large number of influencers will likely pay for.


[Substack]: https://substack.com
[Ghost]: https://ghost.org
[Locals]: https://locals.com
[twitter-export]: https://help.twitter.com/en/managing-your-account/how-to-download-your-twitter-archive
[bounty]: https://twitter.com/balajis/status/1271945241881268224
[mention]: https://help.twitter.com/en/using-twitter/mentions-and-replies
[initial-thread]: https://twitter.com/balajis/status/1271945241881268224
[issue]: https://github.com/balajis/twitter-export/issues/1
[bounty-increase]: https://twitter.com/balajis/status/1271975948846415872
[get_followers_bios.py]: https://gist.github.com/raulgarreta/64b4daaf5295b5a95dd09718ac7512f7
[Twint]: https://github.com/twintproject/twint
[t]: https://github.com/sferik/t
[welcome message]: https://developer.twitter.com/en/docs/direct-messages/welcome-messages/guides/setting-default-welcome-message
[dm-api]: https://developer.twitter.com/en/products/direct-messages
[Buffer]: https://buffer.com/press/buffer-expands-brand-building
[cave-and-commons]: https://hbr.org/2013/03/give-workers-the-power-to-choose-cave
[dm-limits]: https://developer.twitter.com/en/docs/basics/rate-limits
[10kbounty]: https://twitter.com/balajis/status/1272199847324471298
[social-blade-jack]: https://socialblade.com/twitter/user/jack
[keybase-proof]: https://book.keybase.io/guides/proof-integration-guide
[personal token]: https://medium.com/@bramanathan/what-i-learned-from-tokenizing-myself-bb222da07906
[kickbox.com]: https://kickbox.com/
[@balajis]: https://twitter.com/balajis
[followup1]: https://twitter.com/balajis/status/1272199847324471298
[followup2]: https://twitter.com/balajis/status/1272431222485106688
[followup3]: https://twitter.com/balajis
