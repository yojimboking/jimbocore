---
published: true
subtitle:
date: 2022-09-21
tags: projects
---

# Exocore Feedback
Don't show "interlinked pages" if none exist.

Support for footnotes (extended markdown syntax) doesn't seem to be working. Odd because its included in Jekyll's default markdown parser, kramdown

Attaching videos isn't working. Should be able to just detect a .mp4 etc file and convert `![[attachment.mp4]]` to `<video width="400px" height="400px" controls><source src="[attachment.mp4]" type"video/[.mp4]">Your browser does not support this video tag.</video>`

Remove `see this post in context` in the Latest post feed, the tile already takes you there

Make latest posts go where Home is in the navigation side bar. Home doesnt need a link, the pfp/account name suffices.

Ignore first Header when showing the preview in an index

All themes should differentiate between internal and external links.

Notes folder should be changed to "Wiki"

We should add "Scrapbook" for excerpted content taken from the web

Articles should have a Drafts folder that automatically is ignored for publishing. If its not in drafts, its automatically treated as publishing: true unless the YAML specifies otherwise.

Date should also include Last Modified date.

Obsidian currently not working for generating wiki titles as hex codes; this should be possible with its Templater plugin though

If possible, edith's theme should separate H2's into their own boxes

Anchor tags shouldn't show up on the nav bar Articles, Journals etc

Summaries only show up on the index cards if there is body text on the next line immediately after h1; even if its an empty line or any other header before body text it'll be blank or just show the h1.

Jekyll appears to be rendering each internally linked article in lowercase regardless of the original title.

Re add tag view

Images included within a table show `<p></p>` for some reason

Need a `figcaption` markdown syntax

--- 

Template docs need the dates updated for consistent format

Instructions could be made clearer

Need instructions for how to synchronize new updates from primary repo

Need to add Obsidian instructions to exocore