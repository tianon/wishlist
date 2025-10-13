# [Zulip](https://zulip.com/)

For context, I've started (as of 2025-10) using Zulip for family chat, and the primary selling point is literally the ability to move messages (which no competitor seems to have figured out is critically important for a chat tool like this).

A consequence of using this for _family_ chat is that 90% of the usage of the instance will be from mobile, with most users never touching the web interface, so the mobile experience being so ... limited ... is a _real_ downer for everyone.

## General

- frequently used reaction emoji or customizable "popular emoji" (https://github.com/zulip/zulip/issues/21841)

- reaction notifications (https://github.com/zulip/zulip/issues/27327)

- more customizable left sidebar

- when "press Enter to send" is turned on, typing markdown like \`\`\` that's clearly supposed to start a code block and then Enter should _not_ send but should newline until the accompanying closing sentinel

- better markdown support (for example, \_underlines\_ are supposed to be _italic_)

- forcing certain user settings across the org, such as the emoji theme (https://github.com/zulip/zulip/issues/18150)

- when moving messages, we can either move "just this message" or "this and all following" but it'd be cleaner if we could have a third option to multi-select a few messages to move at once, especially if several conversations are happening at the same time (like in "general chat")

- bigger emoji when they're solo (https://github.com/zulip/zulip/issues/15390)

- more padding on settings pages when the website is viewed on mobile (things get cut off for me - I'm usually loading the website on mobile because of the mobile app missing so many features)

- when uploading for the organization image or personal avatar, pan/zoom should be offered to cut it appropriately (for the organization image, it just chopped my image for me, cut off the animation from the GIF, and none of that in a very flattering way)

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
