---
title: "PickleballBot - Devlog 1"
description: "Building PickleballBot"
pubDate: "Jan 08 2024"
heroImage: "/pickleball-bot-1.png"
---

As anyone who has scheduled anything would know, finding a time when everyone is available to do something is notoriously difficult. The more people you add, the more difficult it gets. That's why I decided to build a simple Discord bot to help with scheduling my Pickleball group's weekly meetup.

## What it needed to do?
This part was simple - our existing process for scheduling was pretty bad. Someone would send out a message to the group along the lines of *"Pickleball this weekend?"* and a couple of people would respond with their availability: *"Yeah sure, I'm free 4-6 Saturday, 3-4 Sunday"*. A few follow-ups later and we'd have everyone's availability or non-availability. When you multiply this by 5 people you can see how it becomes pretty annoying to find a common time - add in a doubling in size and it becomes pretty much impossible to do.

So, at the start of every week this bot needed to:
- Present a choice of times for Saturday and Sunday
- Make it easy and simple to vote
- Make it even easier to say you're not available

## How does it do this?
At this point we needed a way to merge the whole back and forth process of finding when to book a court into a single message - I reasoned that the easiest way to prototype a solution would be a Discord bot. I began by looking at existing scheduling bots, but a key thing stood out: all the available solutions had no way to find a common time, instead they were all for creating an event and RSVPing. There were plenty of bots that could be used for voting on event times, but none of them had any way to send at a scheduled repeating time each week.

After a little playing around I decided that it might be worth just combining an event scheduling bot with an automated messaging bot. Unfortunately things weren't going to be that simple and I quickly ran into Discord's [limitation of bots not responding to other bots](https://stackoverflow.com/questions/56799778/discord-bot-to-trigger-other-bots-actions) - an entirely reasonable limitation, but frustrating nonetheless.

Finally, I decided to just roll my own bot. Pros: the functionality is exactly what we need. Cons: more hassle to maintain and host. After a few iterations I ended up with the following:

1. Each Monday at 10am, send a message to the Discord channel "#availability"
2. The message should ask for availability for that Saturday and Sunday
3. Voting should be done through reactions, so the bot should react to each availability message with times in the form of numbers

Or, if you'd like to see it in action:
![PickleballBot in action](/pickleball-bot-1.png)

To start with, I hosted the bot on my own Raspberry Pi 4. This became an issue when I would restart the RPi4 (both accidentally and on purpose), so soon after I moved it to a US$5 Linode VPS where it's still running.

## What are the results?
This is the big question and we've found that it certainly helped a lot eventhough we still need to book a time manually. Anecdotally, people are more likely to vote and there's far less following-up needed.

An issue that has come up is that whoever is booking has to go chase down a weather forecast before they decide exactly what time, so perhaps that could be a future expansion.
