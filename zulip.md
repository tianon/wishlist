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
  - implementation in https://github.com/zulip/zulip/pull/34962, but excludes mobile (grayed out in the settings screenshot) 😭 -- hopefully that's just because mobile lives in a separate castle and it "just" needs to be implemented over there too (mobile doesn't even have the "reactions" view yet though 😭)

- poll response notifications

- more customizable left sidebar

- when "press Enter to send" is turned on, typing markdown like \`\`\` that's clearly supposed to start a code block and then Enter should _not_ send but should newline until the accompanying closing sentinel
  - similarly, it would be nice to be able to tweak this setting when typing polls and todo lists to prevent premature sending (and because there, pressing "Enter" is literally how you add new items so it makes sense that sending should be an explicit separate action, not an "oops, I forgot Shift this time, guess it's done")

- better markdown support (for example, \_underlines\_ are supposed to be _italic_)

- forcing certain user settings across the org, such as the emoji theme (https://github.com/zulip/zulip/issues/18150)

- when moving messages, we can either move "just this message" or "this and all following" but it'd be cleaner if we could have a third option to multi-select a few messages to move at once, especially if several conversations are happening at the same time (like in "general chat")

- bigger emoji when they're solo (https://github.com/zulip/zulip/issues/15390)
- I guess this also implies "custom emoji with a native size bigger than 64x64"
- showing a bigger version of every emoji on hover would be nice, even if it's only slightly bigger
- if an emoji has multiple names, show them all on hover
- the ability to update/replace a custom emoji directly (esp. for adding a higher quality copy, for example, or for later when we can upload bigger than 64x64 😇)
  - > Failed: A custom emoji with this name already exists.
- a way to change the name of an emoji (especially if we get multiple names for a single custom emoji)

- more padding on settings pages when the website is viewed on mobile (things get cut off for me - I'm usually loading the website on mobile because of the mobile app missing so many features)

- when uploading for the organization image or personal avatar, pan/zoom should be offered to cut it appropriately (for the organization image, it just chopped my image for me, cut off the animation from the GIF, and none of that in a very flattering way)

- for some channels, it would be nice to *always* show the topic list in the sidebar, not just when the channel is selected (to reduce the time needed to jump in and start communicating, especially with frequent context switches)
  - maybe a way to pin _topics_ too, not just channels?  and then only show the pinned topics persistently?

- "Include content of direct messages in desktop notifications" should either _also_ apply to private/limited channels, or there should be a separate (perhaps per-channel?) setting for it, because they're similarly private/privileged comms

- easier ways to run regular backups, especially from Zulip Cloud
  - ~~for now, I've set up a bot to regularly run (and download) exports from Jenkins~~
  - welp, scratch that, now getting "Export failed: Exceeded rate limit." (but with a 400 status code, not 429) -- I can't find any documented limits but it must be five exports? (that's how many I have now)
  - no documentation, but I found it in the code: https://github.com/zulip/zulip/blob/5ee9ae7eab3e9d8e87c04842c94d6255540ce2c5/zerver/views/realm_export.py#L44-L62 (maximum 5 exports in a 7 day rolling window, and still counts "deleted" exports, which is why deleting some didn't let me complete a new one)
  - looking further down in that code, it's clear that if we ever reach 250,000 messages *or* 4 of us completely max out our 5GiB then we'll start getting failures we can't overcome -- I guess it'd be nice to have some way to control that, like a way to do an incremental backup?  maybe some way to easily recombine yesterday's and today's into a "complete" backup?
  - for now, I've updated my Jenkins job to use `H H H/2 * *` (backup every other day) which should start succeeding as soon as tomorrow - this will get a little jank at the end of the month (because it's hard to express "every other day" in a cron expression), but for the purposes of a periodic backup it's probably fine (and better than having to do something like once a week)
- related, it would be nice if the `/api/v1/export/realm` endpoint included some kind of checksum (sha256, etc) for verifying the export integrity after download

- better multi-window support (opening a conversation/topic/channel in a new tab/window without multiplying notifications / having a whole new "full" view)
  - relatedly, "settings" being so modal is irritating when I'm getting messages while changing settings and want to read them but not lose what I'm working on
  - a common occurrence for me is reading one thread (especially my note-to-self DMs) and needing to pull up another thread to reply to something without losing my spot and better multi-window support would make that a lot more ergonomic

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

- bug: images in a topic zoom larger with a carousel of *all images* at the bottom - this is great, *except* when some of those images appear inside spoiler tags and should probably be "spoiler blocked" inside the carousel too 😅

- when I click on a topic in the sidebar and then start typing, it should either already have focused the messagebox or immediately focus the messagebox (ie, it should only take one click to get into a topic and start typing a message)

- the web interface seems to prefer to leave half the visible space of the screen blank (when the thread is scrolled all the way down, the bottom of the most recent message is roughly mid-screen), which is a weird use of space (especially when the expanded messagebox below it that it seems like it might've been saving space for is collapsed and even small by default when expanded)

- if my default channel view is set to "topics list" and I click into a topic and then press <kbd>Esc</kbd>, it should take me "back" to the topics list

- some way to subscribe a group to a channel in a way that subscribes future members of that group automatically too

- a way for administrators to modify the avatar of users

- custom emoji in topic titles (and/or an emoji keyboard for topic titles on web where emoji keyboards are less commonly available from the OS)

- "Default user settings" should allow configuring custom per-channel defaults too (especially for "everyone joins this channel" channels)

- pinned channels should (optionally?) stay inside their folder and just be at the top / obviously pinned (pin icon?)

- a way to reorder the "VIEWS" sidebar list, especially since it shows tiny icons of the first few when it gets collapsed (so I'd love to choose *which* tiny icons show up since I don't use/even want several of those)

- bug: if "Organization description" includes emoji, they show up in plain text (`:eyes:` instead of 👀) on the login page
  - ideally this would support full markdown with a better edit box than just a textarea and perhaps even the organization's custom emoji

- dark mode for the login page
- dark mode for the API documentation

- "forward this message" - like quoting, but across channels/topics
  - the way Slack handles this is really clean - it shows a warning if the message you're forwarding is private, and then it only shows a link / the source of the forwarded message if the recipient has access to it also

- the "reactions" view/list should include not only messages I sent, but messages that mention me (or my notification words)

- easier/more reliable preview of link "unfurling" / expanding
  - maybe a way to force it to try again if it fails to find an unfurl?
- a way to avoid the unfurl behavior completely for a single message
  - additionally, a way to retroactively remove the unfurl from a prior message

- recognize URLs to this instance (https://xxx.zulipchat.com/#foo/bar) and display them in the cuter way (`<link to message from @_**person** in #**foo>bar**>` for example)
- relatedly, intelligent "unfurling" for links to other content I have access to; if I see a link to a message, (optionally?) show a preview of it if I can access the original, maybe like the expandable spoilers?

- a way for administrators to change settings on behalf of users
  - for example, their notification settings
  - perhaps opt-in from the users like the export privacy setting?
- alternatively, a way for a user to easily and quickly reset their settings back to the "org defaults" or actively stay set on the org defaults (so the administrator can change the defaults and opted-in users will automatically follow)
- relatedly, a way to see where the org defaults differ from zulip defaults *and* where personal settings differ from the org defaults

- a way to (temporarily) hide my own reactions from the "reactions" view
  - especially self-reactions in self-DMs (which I use to track whether I've moved those notes somewhere more useful/persistent)

- bug: reminders are a DM from the Notification Bot (sure, that's fine), but the text is `You requested a reminder for #channel>@NNNNN` with an inscrutable number instead of a topic name; not sure what that's about and why it isn't a real `#**channel>topic**` reference 😅
  - I'm also not sure where to see/manage reminders once they're set?  maybe that doesn't exist?

- "moved messages" notices should be small (not just special bot messages), and then they'd be generally a lot less disruptive to allow to post
- similarly, renaming a topic should create a small/unobtrusive "event" message inside the topic at the point of the rename
  - this would be similar to how a lot of IRC clients show something like "channel topic changed from 'foo' to 'bar'"

- when adding a custom emoji, the "name" should default to the filename (possibly pre-sanitized of invalid characters)
- relatedly, the "name" field should warn about invalid characters _before_ we've clicked save (simple built-in browser field validation, perhaps?)

- bot API keys should probably be hidden or obscured by default, and should probably include confirmation on the regenerate action (because it's otherwise really disruptive)

- search is "stiff" (I'm not sure exactly how else to describe it); the "narrow" options are all very strict
  - for example, searching for text that's in part of a URL doesn't seem to match
  - I don't think there's a way to search for messages in any topic that contains certain words (ie, searching by words in a topic title, not by words in the message -- `topic:` is strictly exact match)
  - oof, and we can't search by a date range? 😬
  - doesn't search inside links embedded in markdown either 😔

- I see the API knows which Zulip client sent a given message; it'd be neat to optionally expose that in the UI somehow/somewhere

- for APIs like "Update user group members", it would be great to have a parameter to explicitly set the full list of group members (not just add and remove)
- the ability to specify usernames or emails in "group membership" APIs

- optional long-form "descriptions" for topics, so that long-running ones can be more approachable to new participants
  - if this supported full markdown, it would also be a handy place to shove things like persistent links for a topic, such as issue tracker links (making them more discoverable for topic participants)
  - this would get a little complicated if merging topics / topics go away, since that description would need to go *somewhere* (or stick around even if the topic becomes empty), so maybe only channel admins can create/edit descriptions?  and get warnings if they're going to perform an action that would make a non-empty description go away like moving all the messages in the topic elsewhere?

## DMs

- topics in DMs (https://github.com/zulip/zulip/issues/1555)
  - would be a great way to organize "notes to self" inside self-DMs 👀

- moving messages to/from DMs (https://github.com/zulip/zulip/issues/20501)

- the ability to pin DMs too, especially "note to self" self-DMs

- a way to "archive" or "close" DM conversation so they no longer appear in the sidebar (but such that history is preserved and they can be reopened and reappear)

- a way to "leave" a group DM (or otherwise manage my participation in it)

- a way to "delete" a DM entirely (possibly admin-only?)

(in our testing, we're currently working around the DM limitations by using private 1:1 or 1:n channels instead, which brings quirks of its own like having to come up with cute names that mean something to *all* participants, like "parents" for the 1:1 with my spouse)

## [Android](https://github.com/zulip/zulip-flutter)

- most of the desktop functionality 😭 (why is the mobile experience practically a totally different tool??)
  - something that looks more like the "left sidebar" of the desktop UI -- that sidebar could literally be the app landing page
  - the desktop emoji picker for reactions; mobile has a hyper long list that's hard to browse
    - > Reaction emoji options to be more grid-like like in the message box because I don't know what they are called or what keywords to search for so my options are limited since it doesn't endlessly scroll either
    - it also needs to ignore whitespace (when I swipe something on my keyboard, it often adds a space, which then doesn't match the emoji I'm searching for)
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
  - support for `/me` 😔
  - profile editing, especially the avatar (you know, on my phone, where my photos of myself likely are 😂)
  - edit history

- double-tap for 👍 (https://github.com/zulip/zulip-flutter/issues/969), maybe even customizable? (double tap for :heart:, :ack:, etc - could be different per channel but that makes the experience less predictable)

- message preview, especially for complex markdown, code blocks, or "math"/LaTeX expressions (https://github.com/zulip/zulip-flutter/issues/178)
  - (see also above - would love the "full" message experience)

- easier navigation into topics / control over whether clicking a channel drops straight into a topic, the channel feed, or the topics list
  - topics on the channels page: https://github.com/zulip/zulip-flutter/issues/412 (also touches on the "new topic" noted above from 1385)
  - it takes no less than *six* clicks to get into a specific topic to start chatting (click on the Zulip app, click on the channels icon, click on the channel, click on the topic list, click on the topic, click on the message box), meanwhile *all* the channel topics flash on my screen for a minute, some of which might be more sensitive than others (shoulder surfers)
  - most chat apps on Android support long-clicking the application icon to "deep link" directly to into a recent conversation, and even dragging that out into a separate shortcut for a persistent conversation -- this would be really neat for "pinning" common topics to my home screen for instant access
  - (as above) a way to default some or all channels to dropping straight into "general chat" (or maybe a customizable "default topic" per channel) when they're selected
  - hold-clicking on a channel to go into the topic list instead of straight into the full channel feed (avoiding shoulder surfing) brings up a menu, but if there are unread messages it has a "mark all as read" option that's *dangerously* close to the "topic list" option 😬

- per-conversation customizable notifications
  - > Does it have the option of different ring tones for different channels?
  - in most chat apps, the notifications for a given conversation allow long-clicking in the notification area and setting custom sounds, etc specific to that conversation
  - ideally this could be per-topic so that really important conversations can have a unique sound, but per-channel would be really reasonable too ("important" conversations can be split off into a separate channel pretty reasonably, even though topics feel cleaner and like a little sub-channel)

- "mark as read" (and/or "reply") quick action directly from notifications

- better "share to" functionality
  - showing potential share targets in the "share" dialog
  - when sharing to a channel, it pulls up the channel, drops the shared content in the chat box, and defaults to "general chat" but shows the channel feed - if I click on a topic above, it opens that topic but my sharing content is gone, so it would be useful if the top half of that "share" dialog could be a topic *list* instead (and then clicking one could just seed the "topic" box in the message below)
  - related to some of the above feedback, perhaps implementing more of that type of thing would naturally surface topics or at least channels here?

- the ability to download/save or directly (re)share an image from the image view

- when clicking a link to a message, especially from one of the auto-generated quoted blocks, the message being linked to should be highlighted somehow (like how it gets the focus on the website)

- some way to disable or force confirmation for the bulk "Mark as Read" buttons that show up everywhere
  - especially when they're near places I *need* to click, like the bottom toolbar or in menus
  - (seriously, why so aggressive with "mark all as read" ??? it's an extremely destructive operation that can be very hard to "undo")

## Dockerization

Before I gave up and decided to use Zulip Cloud, I tried very hard to run Zulip locally using Docker containers (something I happen to know a thing or two about), and boy howdy this application is **designed** to run inside a hand-maintained virtual machine.  Given the age of the software, I can't really blame them for it, but it sure made running my own instance a pain because the upstream-published image just mimics a VM and I'm "weird" about my containers so that's DOA for me.  I did manage to get something running in my own containers, but every single inch of progress was an uphill battle.  For comparison, most competing solutions (those that are open source, that is) I was able to make my own container images from source successfully in a day or two's work (because they're designed to be separate from the database, etc from the start).

With all that being said, I'm clearly still using the product because as I noted above, they have some _really_ killer functionality that sets them apart from every other tool, even if they're missing a lot of the shine and polish of their competitors, to the point where I gave up running it myself completely but did still want to use it. 🤷

### Zulip Cloud

- ~~not thrilled about the free tier message limit or the pricing for "home" usage, but perhaps that's what I get for considering an enterprisey solution~~
  - ~~maybe we qualify for a "community plan" ? "Communities and personal organizations (clubs, groups of friends, volunteer groups, etc.)"~~
  - confirmed, am now "sponsored" by Zulip! 😊
  - > If you could list Zulip as a sponsor on your website, we would really appreciate it!
  - [![round Zulip logo, as requested](https://github.com/zulip/zulip/blob/5ee9ae7eab3e9d8e87c04842c94d6255540ce2c5/static/images/logo/zulip-icon-128x128.png?raw=true)](https://zulip.com/)  
    > Zulip is an organized team chat app designed for efficient communication.

- the 5GB of storage has me _really_ worried because for personal family chat, we're likely to be sharing a lot of images over time and the storage for those is really going to add up fast
  - it would be neat if I could bring my own (image) storage, somehow?  like provide a Backblaze B2/AWS S3 bucket, or similar
  - with "Standard" it goes up to 5GB/user, but that's still really small and makes me nervous 😅

- organization-level audit logs (which IPs are accessing, etc)
  - this helps with the peace-of-mind for how private my household chats are, because many of them will be really sensitive

- warrant/federal access policy?
  - employee/IT access policy?

(ideally I'd really self-host which would make both of these moot, but that's also why this section is nested under Dockerization -- self-hosting also has rough implications for the household-acceptance-factor because it becomes my problem to provide remote access to it and secure it appropriately, but that's tenable)

## Bot Ideas

- "Reactions": to work around the lack of reaction notifications, a bot that could (for public channels or private channels it gets invited to) notify message senders of reactions to their messages via private DM
  - would need some amount of debounce so it doesn't immediately send a message and a separate message for every single reaction
  - would also need to decide what to do about removed reactions  
    (with debounce, maybe that doesn't matter as much since quick removals wouldn't be notified anyhow)

- ✅ https://github.com/tianon/zulip-bots/tree/main/adsb "ADS-B": what airplane is currently flying over our house (within some small geofence/distance)
  - since I run `readsb` and scrape the data myself, this is "just" reading `aircraft.json` and doing the geo math then piping that into Zulip's API to a specific channel/topic via a Bot token
  - the complicated bit is making sure it only sends the message once per event (maybe it queries the target topic's recent messages?)
  - if it queries for the most recent message, then when there _is_ a recent one, it can update/edit instead of posting anew! (so changing metadata like speed/height, etc can update while it flies over)

- "Unread": to work around the lack of visible unread status, could use emoji reactions on messages to display whether messages have been read by everyone in the channel
  - this probably needs to "settle" in such a way that the end-state is no reactions, so it's more of a "someone hasn't read this message" than "this message has been read" status
  - then the state reconcile when there are event steam glitches is easier too; it can search for messages it has reacted to, check their "read receipts", and remove its reaction
  - needs to somehow account for people who've disabled read receipts *and* people muting topics (because they're basically "never" going to read the messages and the reaction needs to go away eventually)
  - ... which might actually be the deal-breaker with this idea, because whether someone disabled read receipts *or* muted a topic is probably considered "private" data and something we can't query (maybe administrator privileges?)

- a dice-rolling bot (built-in command? `/roll 2d6 1d8`)
