---
layout: post
title: "APIs!!!! The Advantage of Code Over Text-Based Prompts"
date: 2026-07-15
---
July 15, 2026 Entry

Following up on the last post — everything so far has been me reading papers by hand, one at a time, with an LLM as an assistant running on specific commands. However, we don't know what the LLM is thinking (I quote my mentor here). We can never completely entrust our work to the LLM, as in the end, we can't be sure if what comes out works. Furthermore, from my experience of hand mining 44 papers, the time and effort consumed was much more than I had expected and the end results still had to be verified by hand in the case of a mistake. 

What if there was a way to skip this manual process? If there was a machine that could automatically feed these research papers and mine their data at a extremely fast rate? This holds promise for projects like ours where going over 300+ papers to mine data pertaining to critical conditions is common. Luckily, it's called an API (application programming interface). Essentially, it is just a defined way for one piece of software to talk to another directly, without a human clicking through a UI in between (what I was doing for the past weeks). Instead of me typing into a chat window, my code sends a request straight to Claude's servers — the paper's text plus instructions on what to extract. If we were to put it in simple words, I am the ferryman, making round trips to and across the river at set times, while the API is the Golden Gate Bridge that allows passage any time of the day at great convenience (at great initial cost, however). Anyways, I digress. The same script can run on one PDF or a hundred, on a schedule, unattended, and produce the same kind of output every time. You know exactly what is going on because you know the entire script and can edit it whenever and to whatever, produces transparent results that can easily be verified by other researchers, and is convenient to troubleshoot and debug whenever something goes wrong with the process. 

**Setting up the actual API**
I'll keep it short since the actual process has to do with API design and actually extracting that data. Essentially, the 2 core components of this process are Anaconda Powershell and Microsoft Visual Code, as well as your computer's file system. Powershell is basically window's terminal function, and it can access files and manipulate them with code. This is where we will perform the actual API call and the test. Microsoft Visual Code is for opening, editing, and nesting files. If something is wrong with the code, I edit it here. If I need to update the code (eg adding a new .py file or something), I can create it easily in visual code and nest it under the right file. Exact steps on my github repo. 

**Update on the data mining by hand process**
The by hand mining is finished. We intend to compare these results with that of the results obtained from continually updating API call (eg we will continuously update code to attain best effects). This is to test the effectiveness of commercial LLMs in research projects like this. Short post today. Just another progress update.

