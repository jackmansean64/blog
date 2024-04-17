---
title: "How To Retrieve Correct Highlights From An Amazon Kindle"
date: 2024-04-17
draft: false
---
# Background
eBook highlights are selections of text from the ebooks that you want to save and access later. Passages containing things like quotes, stories, interesting information, key points, etc. are all common reasons to highlight. Ebooks from different manufacturers each have their own means of handling highlights. This article is focused on the Amazon Kindle eReader.
# Problem
After we finish highlighting our books we need to export the highlights so that we can access them on a more convenient device like a computer. This is easy for eBooks purchased through Amazon's Kindle Store, however the task of (accurately) exporting the desired highlights for personal ebooks (ie. ebooks not obtained via the Kindle Store) from a modern Kindle proves surprisingly difficult. 
# Clippings.txt ❌
The standard solution to this problem is the clippings.txt file. On the surface, the clippings.txt file seems like a great solution. All highlights from all books are stored on the same text file so it's a simple matter to export the file and upload it into one of the various solutions that exist for managing ebook highlights such as Readwise or Evernote. However, the clippings.txt file quickly proves problematic if you happen to compare the highlights stored in clippings.txt with the ones you see in your ebook.

If you happen to make a mistake while highlighting your book (ie. highlighting the wrong word or section of text, changing your mind, etc.) the clippings.txt file will diverge from what you see on your screen. **Every single highlight that you have ever made is stored in the clippings.txt file, including the ones that you've undone and deleted.**

This issue is compounded by the difficulty posed in highlighting using e ink displays. While they've certainly come a long way in 2023, the screens still suffer from slow responsiveness relative to typical device displays making dynamic actions difficult. To highlight a section of text from an ebook, you must hold your finger on a word, pause until it selects the txt, drag your finger to the last word of the section, pausing to wait for the screen to catch up to verify you've stopped on the right word, and then letting go. If you miss the word, you can continue dragging the highlight around until you get the right spot. Obviously, this process is error prone and results in having to delete and undo a lot of highlights.

So, if you attempt to use the highlights retrieved from clippings.txt directly, you will have to wade through your history of mistakes resulting in duplicates and overlapping highlights. 

While I disagree with the approach Amazon took here I can see some sense in it. By storing everything, you have a full history of all of your highlights and will never have to worry about highlights getting lost or overwritten through the usage of the device. The downside is (merely) that you have no way of seeing the highlights you actually want to see... That is, the final state of your highlights.
# Duplicate Detection ❌
To attempt to get around this issue, services have implemented solutions like Readwise's "advanced duplicate detection" which attempts to delete the unwanted highlights. While this also seemed promising initially, it doesn't quite get it right either. For example while it often correctly identifies overlapping highlights and deletes them, it also tends to overcorrect and delete intended highlights that are close together. It also has no way of identifying highlights that the reader changed their mind about and deleted - those all remain.

To be fair to Readwise, I don't really see how any service could get this 100% right since it's impossible to know exactly which highlights the reader intends to keep based solely on a record of all the highlights they made so it will always just be a best guess. In my experience, roughly 5-10% of the highlights differed between Readwise's end result and the actual highlights on my Kindle which is an unacceptable error rate in my opinion (though this rate would surely decrease if you avoided highlighting passages close to each other and made fewer mistakes or adjustments).
# Native Kindle Highlights ❌
Okay so clippings.txt is practically unusable. The next obvious questions is: How does the Kindle natively store the correct state of the highlights and can we use it? 

The Kindle stores its highlights alongside each ebook in a separate file (for 11th gen Kindles using a ".azw3r" file, though different file formats have been used for past Kindle versions). Unfortunately, this is a proprietary, non human-readable format that as of this time, doesn't have any well known programs for parsing it. I was able to dig up some scripts that various programmers have written over the years to parse this file, however they're very difficult to use (even for a developer). While I was able to successfully parse the .azw3r file using a c code script I found on mobileread.com, it turned out that was only the first step because **the .azw3r file doesn't actually store the highlights, just the start and end locations of them**. To make matters worse, each ebook file type has (unsurprisingly) slightly different text locations in their files so not only is the second step of matching extracting the highlights from the ebook using the start and end locations required, but it must also be handle multiple different ebook formats. While there was a perl script linked at the same location that purported to achieve this, I was unable to get it working after a couple hours of trying. 

So, while it's theoretically possible to extract correct highlights in this way, it's currently completely inaccessible to anyone but an experienced developer with the time and patience to make the existing hacked together scripts work or build a more robust solution themselves. Perhaps I'll take this on as a personal project at some point... 
# Send to Kindle ✔
My last ditch effort was to attempt to leverage the Kindle cloud ebook service which I had originally assumed was only usable with ebooks purchase from the store. However, I discovered that Amazon currently offers a service called [Send to Kindle](https://www.amazon.com/sendtokindle)  which allows you to upload ebooks (epub, mobi, pdf, etc.) to your Amazon account. Highlights from these books are then synced across your devices via the Kindle apps.

So, the highlights for these uploaded books seem to work the same way they do for the native Kindle Store purchased ebooks! From the Windows desktop Kindle App, you can export your highlights as html. You can then either view them in the Kindle App or in a web browser, or import them into a service like Readwise which then provides convenient access to them via their app and excellent selection of export capabilities.
## Drawbacks
One concern I have with this method is if Amazon has a policy for ebooks obtained outside the proper channels and are actively searching for signs of them in uploaded ebooks. So far I haven't noticed an issue so I think it's unlikely to be a problem, but it could be an issue if they did start looking and potentially removing any problematic ebooks they find or worse case ban you from the service (which might be a stretch).

In addition, it's a little inconvenient because you now need to worry about an additional method of uploading and managing ebooks rather than being able to rely entirely on an ebook management program like Calibre. It also doesn't seem to be possible to see from the Kindle which ebooks are synced from your Amazon account vs uploaded manually, so if you mix and match you need to make sure you aren't highlighting your Calibre ebooks inadvertently.

Finally, this method relies on Amazon continuing to support it. At any point, Amazon could decide to remove this service or render it incompatible with the strategy outlined above and we're back to square one.

