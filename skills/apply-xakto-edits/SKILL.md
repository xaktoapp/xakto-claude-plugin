---
name: apply-xakto-edits
description: Writes the edits the user made to a live page in Xakto, the Chrome extension, into the project's source code. Use when the user says "Apply my Xakto edits", with or without ids such as "3, k2", or asks to put their Xakto changes in the code.
---

# Apply the user's Xakto edits

The user changed a live page in Xakto: its styles, words, attributes or layout. Those edits live only in the browser until you write them in the source.

1. Call `get_pending_edits`. When the user names ids, as in "Apply my Xakto edits 3, k2", pass them as `ids`; otherwise call it without. If it says an id is no longer pending, ask the user which edits they meant.
2. Find each element in the source by its words, its classes and its selector, and write exactly the change listed:
   - On a Tailwind page, swap the classes named rather than adding inline styles.
   - When an element is one of several alike, ask whether the user meant that one or all of them.
   - A moved element says where it landed, such as "now first, before …" or "now 2nd of 3, between …": put it there.
   - An edit said to be handed over before and not yet written: look in the source first, and if it is there already, don't write it again.
3. Call `mark_edits_applied` with the ids you wrote, or with none when you wrote them all. Xakto then lists them under In the code and takes its previews off the page once the page shows your code.
4. Say what you changed, file by file.

If Xakto isn't connected, tell the user to open Xakto's menu › Coding agent in Chrome. Meanwhile they can use Copy as prompt in Xakto's Changes and paste the edits here.

When the user asks for a visual change to the page and doesn't say where, ask whether they want it in the browser, with `edit_element` or `edit_page` as a preview they can undo, in the code, or both.
