# [Zulip](https://zulip.com/)

For context, I've started (as of 2025-10) using Zulip for family chat, and the primary selling point is literally the ability to move messages (which no competitor seems to have figured out is critically important for a chat tool like this).

A consequence of using this for _family_ chat is that 90% of the usage of the instance will be from mobile, with most users never touching the web interface, so the mobile experience being so ... limited ... is a _real_ downer for everyone.

This list focuses mostly on the bad/downsides, because that's who I am (sorry!) -- in my opinion, the good mostly speaks for itself.  If you want to know what I mean, you can fall in love with Zulip before you ever try it by following the exact same steps I did:
- open https://zulip.com/help/
- scroll the sidebar reading topic titles
- click on and read anything that sounds even remotely interesting
- every. single. feature. is. a. banger.
  - explicit topics per channel (no more chaos threads)
  - moving messages between topics, channels
  - "full" markdown support (lists, sublists, TYPED code blocks, etc)
  - spoiler tags
  - collaborative TODO lists
  - polls
  - more than one emoji reaction per person (looking straight at you, Signal)
  - "global times" (post a date/time, everyone can see it as if you typed their local - no more date math)
  - LaTeX for embedded math
  - tables
  - trivial/clean bot support (including trivial per-user bots) + straightforward APIs (the "Jenkins" item I note in the lists below took me all of an hour at most to set up completely)

## General

- frequently used reaction emoji or customizable "popular emoji" (https://github.com/zulip/zulip/issues/21841)

- reaction notifications (https://github.com/zulip/zulip/issues/27327)

- poll response notifications

- more customizable left sidebar

- when "press Enter to send" is turned on, typing markdown like \`\`\` that's clearly supposed to start a code block and then Enter should _not_ send but should newline until the accompanying closing sentinel
  - similarly, it would be nice to be able to tweak this setting when typing polls and todo lists to prevent premature sending (and because there, pressing "Enter" is literally how you add new items so it makes sense that sending should be an explicit separate action, not an "oops, I forgot Shift this time, guess it's done")

- better markdown support (for example, \_underlines\_ are supposed to be _italic_)

- forcing certain user settings across the org, such as the emoji theme (https://github.com/zulip/zulip/issues/18150)

- when moving messages, we can either move "just this message" or "this and all following" but it'd be cleaner if we could have a third option to multi-select a few messages to move at once, especially if several conversations are happening at the same time (like in "general chat")

- bigger emoji when they're solo (https://github.com/zulip/zulip/issues/15390)

- more padding on settings pages when the website is viewed on mobile (things get cut off for me - I'm usually loading the website on mobile because of the mobile app missing so many features)

- when uploading for the organization image or personal avatar, pan/zoom should be offered to cut it appropriately (for the organization image, it just chopped my image for me, cut off the animation from the GIF, and none of that in a very flattering way)

- for some channels, it would be nice to *always* show the topic list in the sidebar, not just when the channel is selected (to reduce the time needed to jump in and start communicating, especially with frequent context switches)
  - maybe a way to pin _topics_ too, not just channels?

- "Include content of direct messages in desktop notifications" should either _also_ apply to private/limited channels, or there should be a separate (perhaps per-channel?) setting for it, because they're similarly private/privileged comms

- easier ways to run regular backups, especially from Zulip Cloud
  - for now, I've set up a bot to regularly run (and download) exports from Jenkins

- better multi-window support (opening a conversation/topic/channel in a new tab/window without multiplying notifications / having a whole new "full" view)

- "Drafts are not synced to other devices and browsers." is really sad and they *should* be sync'd, especially to/from mobile (start typing a comment, want to preview it or type it on a bigger device, etc)
  - > Doh lost my message by switching screens ... I somehow got back to this screen and there was my message partially typed

- multiple names for a single custom emoji (just like many of the built-in emoji have)

- a way to default some or all channels to defaulting straight into "general chat" (or maybe choosing any specific topic as default) when they're selected

- pressing "enter" in the "new task" or "description" field on a task list should add the task and focus the field for adding another

- polls with an enforced and well-advertised time limit (possibly "re-openable" ?)

- optionally (per-channel?) actively *show* read-receipts on messages (maybe similar to reactions? or even as a "special" reaction so it has the same name-showing behavior?)

- bot descriptions (custom profile fields for bots?), so their purpose can be written down somewhere discoverable by other users who might be off-put by "bots" (especially less technical users whose exposure to the term "bots" in 2025 is now mostly AI slop 😭)

- the option for bigger gif preview in the "giphy" search (they're all so tiny on my 4k screen 😅)

- alt text for images (`![alt text](image URL)`, in most markdown syntax)

- images in a topic zoom larger with a carousel of *all images* at the bottom - this is great, *except* when some of those images appear inside spoiler tags and should probably be "spoiler blocked" inside the carousel too 😅

## DMs

- topics in DMs (https://github.com/zulip/zulip/issues/1555)

- moving messages to/from DMs (https://github.com/zulip/zulip/issues/20501)

(in our testing, we're currently working around the DM limitations by using private 1:1 or 1:n channels instead, which brings quirks of its own like having to come up with cute names that mean something to *all* participants, like "parents" for the 1:1 with my spouse)

## [Android](https://github.com/zulip/zulip-flutter)

- most of the desktop functionality 😭 (why is the mobile experience practically a totally different tool??)
  - something that looks more like the "left sidebar" of the desktop UI -- that sidebar could literally be the app landing page
  - the desktop emoji picker for reactions; mobile has a hyper long list that's hard to browse
    - > Reaction emoji options to be more grid-like like in the message box because I don't know what they are called or what keywords to search for so my options are limited since it doesn't endlessly scroll either
  - moving messages (https://github.com/zulip/zulip-flutter/issues/1438, https://github.com/zulip/zulip-flutter/issues/530)
  - easier editing/creating topics (like from the topic list)
    - creating topics: https://github.com/zulip/zulip-flutter/issues/1385
    - > Topic title editing on mobile!
  - show channel folders (https://github.com/zulip/zulip-flutter/issues/1765)
  - at least the _option_ for the "full" message editing experience (all the helpful buttons, the message formatting quick-reference, etc)
  - when _typing_ emoji (not reacting), most mobile keyboards have easy access to the Unicode-approved set of emoji, so an emoji picker that emphasizes custom emoji ahead of "standard" emoji would be nice
    - bonus points if it can also emphasize emoji that the current phone's operating system doesn't support yet, but Zulip does 👀
    - (basically, making it easy to type emoji that exist in a Zulip instance but aren't easy to type on a phone keyboard)
  - ... support for todo lists at all (but at the very least, added items should show up somehow??  maybe strikethrough for checked off things??  ideally the actual list)
  - the same LaTeX rendering engine the web UI uses (things like `\frac{a}{b}` works great on web but not on mobile and unless you know that, you wouldn't know your audience is seeing raw LaTeX instead of a cute formula)

- double-tap for 👍 (https://github.com/zulip/zulip-flutter/issues/969), maybe even customizable? (double tap for :heart:, :ack:, etc - could be different per channel but that makes the experience less predictable)

- message preview, especially for complex markdown, code blocks, or "math"/LaTeX expressions (https://github.com/zulip/zulip-flutter/issues/178)
  - (see also above - would love the "full" message experience)

- easier navigation into topics / control over whether clicking a channel drops straight into a topic, the channel feed, or the topics list
  - topics on the channels page: https://github.com/zulip/zulip-flutter/issues/412 (also touches on the "new topic" noted above from 1385)
  - it takes no less than *six* clicks to get into a specific topic to start chatting (click on the Zulip app, click on the channels icon, click on the channel, click on the topic list, click on the topic, click on the message box), meanwhile *all* the channel topics flash on my screen for a minute, some of which might be more sensitive than others (shoulder surfers)
  - most chat apps on Android support long-clicking the application icon to "deep link" directly to into a recent conversation, and even dragging that out into a separate shortcut for a persistent conversation -- this would be really neat for "pinning" common topics to my home screen for instant access
  - (as above) a way to default some or all channels to dropping straight into "general chat" (or maybe a customizable "default topic" per channel) when they're selected

- per-conversation customizable notifications
  - > Does it have the option of different ring tones for different channels?
  - in most chat apps, the notifications for a given conversation allow long-clicking in the notification area and setting custom sounds, etc specific to that conversation
  - ideally this could be per-topic so that really important conversations can have a unique sound, but per-channel would be really reasonable too ("important" conversations can be split off into a separate channel pretty reasonably, even though topics feel cleaner and like a little sub-channel)

- "mark as read" (and/or "reply") quick action directly from notifications

- better "share to" functionality
  - showing potential share targets in the "share" dialog
  - when sharing to a channel, it pulls up the channel, drops the shared content in the chat box, and defaults to "general chat" but shows the channel feed - if I click on a topic above, it opens that topic but my sharing content is gone, so it would be useful if the top half of that "share" dialog could be a topic *list* instead (and then clicking one could just seed the "topic" box in the message below)
  - related to some of the above feedback, perhaps implementing more of that type of thing would naturally surface topics or at least channels here?

## Dockerization

Before I gave up and decided to use Zulip Cloud, I tried very hard to run Zulip locally using Docker containers (something I happen to know a thing or two about), and boy howdy this application is **designed** to run inside a hand-maintained virtual machine.  Given the age of the software, I can't really blame them for it, but it sure made running my own instance a pain because the upstream-published image just mimics a VM and I'm "weird" about my containers so that's DOA for me.  I did manage to get something running in my own containers, but every single inch of progress was an uphill battle.  For comparison, most competing solutions (those that are open source, that is) I was able to make my own container images from source successfully in a day or two's work (because they're designed to be separate from the database, etc from the start).

With all that being said, I'm clearly still using the product because as I noted above, they have some _really_ killer functionality that sets them apart from every other tool, even if they're missing a lot of the shine and polish of their competitors, to the point where I gave up running it myself completely but did still want to use it. 🤷

### Zulip Cloud

- not thrilled about the free tier message limit or the pricing for "home" usage, but perhaps that's what I get for considering an enterprisey solution
  - maybe we qualify for a "community plan" ? "Communities and personal organizations (clubs, groups of friends, volunteer groups, etc.)"

- the 5GB of storage has me _really_ worried because for personal family chat, we're likely to be sharing a lot of images over time and the storage for those is really going to add up fast
  - it would be neat if I could bring my own (image) storage, somehow?  like provide a Backblaze B2/AWS S3 bucket, or similar

- organization-level audit logs (which IPs are accessing, etc)
  - this helps with the peace-of-mind for how private my household chats are, because many of them will be really sensitive

- warrant/federal access policy?
  - employee/IT access policy?

(ideally I'd really self-host which would make both of these moot, but that's also why this section is nested under Dockerization -- self-hosting also has rough implications for the household-acceptance-factor because it becomes my problem to provide remote access to it and secure it appropriately, but that's tenable)
