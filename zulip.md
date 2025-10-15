# [Zulip](https://zulip.com/)

For context, I've started (as of 2025-10) using Zulip for family chat, and the primary selling point is literally the ability to move messages (which no competitor seems to have figured out is critically important for a chat tool like this).

A consequence of using this for _family_ chat is that 90% of the usage of the instance will be from mobile, with most users never touching the web interface, so the mobile experience being so ... limited ... is a _real_ downer for everyone.

## General

- frequently used reaction emoji or customizable "popular emoji" (https://github.com/zulip/zulip/issues/21841)

- reaction notifications (https://github.com/zulip/zulip/issues/27327)

- poll response notifications

- more customizable left sidebar

- when "press Enter to send" is turned on, typing markdown like \`\`\` that's clearly supposed to start a code block and then Enter should _not_ send but should newline until the accompanying closing sentinel

- better markdown support (for example, \_underlines\_ are supposed to be _italic_)

- forcing certain user settings across the org, such as the emoji theme (https://github.com/zulip/zulip/issues/18150)

- when moving messages, we can either move "just this message" or "this and all following" but it'd be cleaner if we could have a third option to multi-select a few messages to move at once, especially if several conversations are happening at the same time (like in "general chat")

- bigger emoji when they're solo (https://github.com/zulip/zulip/issues/15390)

- more padding on settings pages when the website is viewed on mobile (things get cut off for me - I'm usually loading the website on mobile because of the mobile app missing so many features)

- when uploading for the organization image or personal avatar, pan/zoom should be offered to cut it appropriately (for the organization image, it just chopped my image for me, cut off the animation from the GIF, and none of that in a very flattering way)

- for some channels, it would be nice to *always* show the topic list in the sidebar, not just when the channel is selected (to reduce the time needed to jump in and start communicating, especially with frequent context switches)

- "Include content of direct messages in desktop notifications" should either _also_ apply to private/limited channels, or there should be a separate (perhaps per-channel?) setting for it, because they're similarly private/privileged comms

- easier ways to run regular backups, especially from Zulip Cloud
  - for now, I've set up a bot to regularly run (and download) exports from Jenkins

- better multi-window support (opening a conversation/topic/channel in a new tab/window without multiplying notifications)

- "Drafts are not synced to other devices and browsers." is rubbish and they *should* be sync'd, especially to/from mobile (typing a comment, want to preview it or type it on a bigger device, etc)

- multiple names for a single custom emoji (just like many of the built-in emoji have)

## DMs

- topics in DMs (https://github.com/zulip/zulip/issues/1555)

- moving messages to/from DMs (https://github.com/zulip/zulip/issues/20501)

## [Android](https://github.com/zulip/zulip-flutter)

- most of the desktop functionality 😭 (why is the mobile experience practically a totally different tool??)
  - the desktop emoji picker for reactions; mobile has a hyper long list that's hard to browse
  - moving messages (https://github.com/zulip/zulip-flutter/issues/1438, https://github.com/zulip/zulip-flutter/issues/530)
  - easier editing/creating topics (like from the topic list)
    - creating topics: https://github.com/zulip/zulip-flutter/issues/1385
  - something that looks more like the "left sidebar" of the desktop UI
  - show channel folders (https://github.com/zulip/zulip-flutter/issues/1765)

- double-tap for 👍 (https://github.com/zulip/zulip-flutter/issues/969)

- message preview, especially for complex markdown, code blocks, or "math"/LaTeX expressions (https://github.com/zulip/zulip-flutter/issues/178)

- easier navigation into topics / control over whether clicking a channel drops straight into a topic, the channel feed, or the topics list
  - topics on the channels page: https://github.com/zulip/zulip-flutter/issues/412 (also touches on the "new topic" noted above from 1385)
  - it takes no less than *six* clicks to get into a specific topic to start chatting (click on the Zulip app, click on the channels icon, click on the channel, click on the topic list, click on the topic, click on the message box), meanwhile *all* the channel topics flash on my screen for a minute, some of which might be more sensitive than others (shoulder surfers)
  - most chat apps on Android support long-clicking the application icon to "deep link" directly to into a recent conversation, and even dragging that out into a separate shortcut for a persistent conversation

- per-conversation customizable notifications
  - in most chat apps, the notifications for a given conversation allow long-clicking in the notification area and setting custom sounds, etc specific to that conversation

- "mark as read" and "reply" directly from notifications

- better "share to" functionality
  - showing potential share targets in the "share" dialog
  - when sharing to a channel, it pulls up the channel, drops the shared content in the chat box, and defaults to "general chat" but shows the channel feed - if I click on a topic above, it opens that topic but my sharing content is gone, so it would be useful if the top half of that "share" dialog could be a topic *list* instead (and then clicking one could just seed the "topic" box in the message below)

## Dockerization

Before I gave up and decided to use Zulip Cloud, I tried very hard to run Zulip locally using Docker containers (something I happen to know a thing or two about), and boy howdy this application is **designed** to run inside a hand-maintained virtual machine.  Given the age of the software, I can't really blame them for it, but it sure made running my own instance a pain because the upstream-published image just mimics a VM and I'm "weird" about my containers to that's DOA for me.  I did manage to get something running in my own containers, but every single inch of progress was an uphill battle.  For comparison, most competing solutions (those that are open source, that is) I was able to make my own container images from source successfully in a day or two's work.

With all that being said, I'm clearly still using the product because as I noted above, they have some _really_ killer functionality that sets them apart from every other tool, even if they're missing a lot of the shine and polish of their competitors, to the point where I gave up running it myself completely. 🤷
