+++
title = 'One of those cool course projects'
date = 2024-08-05T17:33:06+08:00
draft = false
+++

I'm writing this after my last paper for my second semester of my second year. Recently, just a week ago on Friday we submitted our course project for EFB2073 - Microprocessor and Computer Architecture. It was a fun course although I'm not sure how well I did on the tests. Semester results would be out a month from now. Anyways it was one of those courses that really did push me to learn and discover more.

I like to compare myself to others (but stop when it becomes negative to growth[^remark]). From what I've seen so many opted for a non-IoT project. The few that did used Arduino, which was explicitly disallowed. Turns out one group did figure out actual (Inter)net of Things with pure ESP IDF, something I couldn't figure out because I was severely tunneled-vision. I didn't do enough research because we wanted to rush it in three days. We spent ~1.75 days being stuck trying to use ESP Rainmaker. In the midst of that tunnel vision we overlooked the simple fact that the basic ESP IDF [components](https://github.com/espressif/esp-idf/blob/master/components/esp_http_client/test_apps/main/test_http_client.c "Title") already handle HTTP requests with few overhead, (I recall seeing the examples folder in the ESP IDF repo but ignored them!).

We swallowed the copium pill by slightly twisting the 'I' in IoT. How about **Intra**net of Things instead? And that was how we ended up using the ESP-NOW protocol instead. What's funny was that there wasn't an example project for ESP-NOW that fit nicely to what we wanted to do. And what we wanted to do was simple (just check out the source code). So we ended up spending even more time on what would otherwise be something trivial.

The person who figured out IoT with ESP IDF admittedly still worked on it a few hours before the submission deadline, so even if we went down that path we would've risked a late submission. But what this taught me was it would have helped to stop being so locked in for 20 minutes to half an hour, just to look at the problem at hand calmly with no distress.

On the second day I had a terrible sinus experience. The entire day my nose was just leaking fluid nonstop, so that was probably what led us into picking ESP-NOW instead.

[^remark]: Comparing yourself to others is one of the easiest ways to challenge and push yourself. Use with caution however, because you would tend to do the same even when there's nothing you can do about it anymore when you lose the imaginary contest you've set up in your head. The antidote here is humility.

### Links

- [Our project report](https://andergisomon.github.io/efb2073_report "Title")
- [IMO the group with the best submission](https://sites.google.com/view/scpro/home "Title")