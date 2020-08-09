---
layout: single
title:  "Regression Testing: Drawing Lines in the Sand"
date:  2020-08-03
tags: testing
excerpt: Every time my team touched the code, we ran the risk of changing important output results -- without even knowing it.
---

I had a legacy project at work that I took over a few years ago, stepping in for a co-worker whose role was expanding and she needed to hand off the software development of the project. It was a great opportunity for me to join a new research project and a great opportunity to jump into that regime of scientific code that I love best: time-stepping simulations.

But, there was a challenge. This was legacy code that was well respected and had a public history of results. The code and results had been used for published papers and also to build the case with research sponsors for why the research should continue. The code and it's results were considered correct, trustworthy, and reliable. This was code that Eric Winsburg would call "XXX".

**My Challenge** As the new software lead, I had no part of that code history. I had no idea which revision of the software had been used for those trusted, published results. Fortunately, the code that I received was configuration managed at a basic level (yay!), but not rigorously. There were no tags, no issue management, no obvious branching methodology, no continuity of a development team. And we had development work to do -- changes to get working on. Every time my development team touched the code to introduce a new research feature, we ran the risk of changing historically accepted output results -- without even knowing it. :(

Taking over that project felt like walking through an unlit room full of furniture. We needed shin guards! We had to get some control over the situation before one of our "bug fixes" or "new features" made the code untrustworthy.

**Enter Regression Testing** Regression testing is like drawing lines in the sand. It connects code revisions to input files and output results and makes them a semi-gelatinous thing. For scientific code, the results are not necessarily "truth", just currently accepted results. They are a baseline of results that can be used to help identify changing results.

Did you catch my wording there? Two important adjectives: `currently` and `accepted`.

_Currently_. The honest truth is that scientific code results do change. Ok, maybe not the trivial ones, but certainly the complex results that we care about. The ones that we were searching for, that force us to write research software in the first place. We need to expect changes to results and plan for it.

_Accepted_. Sometimes we don't know if our research software is giving us the "correct" answer. It's research, for crying out loud! We may not really even know what the "correct" answer is. But, our scientific intuition can be trusted in these cases to identify obviously wrong results and results that are reasonably plausible. For regression results, we define acceptable results as those that we trust from a scientific and research perspective, even if we don't know if they are absolutely correct.

So how do "currently accepted results" help? Well, via results comparison activities, of course! For each important change to the research software, a new result set can be generated. These are then compared to the old results set. If the comparison shows that the results haven't changed -- great! If a change has occurred, then an investigation needs to be done to determine why the change and if the new results set should be considered the new "currently accepted". Each set of "currently accepted results" is a new line in the sand.

It's important to remember that the new results are not necessarily wrong -- just new. It's up to the folks with scientific and software expertise to decide which results set should be the "currently accepted" one. Maybe you fixed a bug and the new results are better. Maybe you accidently introduced a bug and the old results are more trustworthy. The investigation is the process through which that discovery is made.

In the case of my project, everything became healthier once we had baseline regression results in place. And once we forced ourselves to pay attention to them. We could change the code and feel fairly comfortable that we would know if we did something subtly bad. And doing these investigations became a really good mechanism to learn the code and all it's legacy nuances (can you say "skeletons in the closet"?). And it gave us a data-based context for our discussion about what changes were good ones. Regression testing saved us.

Of course, we did have to constantly generate new regression results for each code change. That was a good opportunity for some continuous integration automation! And we did need regression results that covered the full input spectrum. But, that's a different topic.
