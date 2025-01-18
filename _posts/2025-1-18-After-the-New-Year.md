---
layout: post
title: After the New Year
---

It's been 3 and half weeks since my past post. I went on a week trip to Japan, and it's already been the third week of Janurary. Today, the weather is amazing, Vancouver is on a streak of dry air from the south, so we have a lack of rain for the next little bit. 

I went crabbing today to take advantage of the nice weather, but it was super cold. I caught a dungeoness crab, and will cook it in a bit. 

I've been quite slow on working on the trips app. It's a bit more difficult to parse iteneary emails that I thought it would be. I tried to use a LLM model to try to parse the text, but because the text is ill-formatted, its a bit more difficult than I thought.

My current idea is that because emails are usually HTML, and HTML is a tree format. We can look for specific keywords, like *Check-in* or *Arrival Time* and look for a related string of similar format. A date for checkin, and a time for arrival time. and try to find the relative closest element to the keywords. Assuming that the keywords and the related information are gonna reside relatively close in the rendered UI. 

This is potentially an actual usecase of the leetcode's tree traversal algorithms so I'm pretty excited to put it to use. But I'm debating if I need to rewrite the tree node object or use the builtin one in golang. Hopefully I can spend more time on it next week, and be able to update it here. =)


