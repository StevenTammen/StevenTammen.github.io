---
permalink: /about/
layout: layout
title: About
---

<h1 class="center"> About The Site </h1>

## Author

My name is Steven Tammen and I am an undergraduate student at the University of Georgia studying Latin, Greek, Hebrew, and Classical culture. I am also interested in philology, the ancient Near East, and ancient history in general.

My other pursuits cluster around the theme of practical efficiency -- optimizing objects and processes through systematic study and continuous improvement to make them the best they can be according to the constraints inherent to reality.

### Purpose

This site exists to

- Give me a centralized internet presence
- Give me a platform to spread my thoughts on a wide variety of otherwise unrelated topics
- Contribute to free and open knowledge

This site does not exist to

- "Market myself"
- Make money by locking content behind exclusive mailing lists, paid eBooks, monthly subscriptions, or other things of the sort
- Make money through advertising or affiliate marketing

## Backend

Please have a look at the readme in [this site's Github repository](https://github.com/StevenTammen/steventammen.github.io) for a concise technical summary of how everything works.

## Stucture

The "Home" page of this site gives a brief overview of what has been published recently, and will also have other items as the need arises (requests for help with projects, announcements, etc.). The "Contact" and "CV" pages are exactly what they sound like -- there are links to my publications/writings in the CV.

The "Pages" page contains all the pages that have been completed, organized into alphabetically-sorted categories. If you know what you are looking for, you can use Ctrl+F (or your hotkey equivalent) to rapidly navigate to it. The "In Progress" page is organized in exactly the same manner, but contains pages that are not yet completed. These pages may range from barely started (a collection of research links and bullet points with preliminary thoughts), to almost finished (complete expositions waiting for proofreading and polishing).

The "Search" page contains an embedded Google custom search object. You may search using the same syntax as normal (e.g., enclosing things in quotes, prepending things with dashes, etc.), but results will show up on the page rather than in another window, and will be limited to results on this site.

The "Settings" page will eventually contain various customization options for the site, such as adjusting font size, line spacing, background color, and so forth. Please check back later -- I will try to implement customization as soons as I can.

The "Contribute" page explains how you can help contribute to the content, design, and focus of this site.

## Open Sourcing Websites And Workflows

### Transparency From Square One

I am strong believer in publishing content before it is finished completely. This is so for two reasons: 1) waiting until pages are "finished" before publishing means that they aren't useful to anyone else until the very end of the research and writing process, and 2) I am far from a perfect writer (and my knowledge in many areas is less than complete), so giving people opportunities for feedback and constructive criticism from the very beginning of the process will help improve the content more than waiting until some arbitrary point of "good enough for others to see". To use an anology, open source code projects don't wait until their code is "good enough" to push to GitHub, it starts open source from the get go, and is better for it. Obviously prose is not code, but the same general logic applies: 

1. multiple people working on the same thing will yield better results than a single individual
2. this is true at all stages of the creation process, not just for edits of an already-finished work
3. Therefore (*modus ponens*), enabling multiple people to contribute at all stages of the process will yield better results
4. better results are a desirable thing that should be pursued
5. Therefore (*modus ponens*), policies enabling multiple people to contribute at all stages of the process should be pursued

If it wasn't obvious from that chain of propositions, open sourcing stuff is something that I think is important. Code has been opensourced for a while now, and hardware is beginning to get there (see: crowdsourced tech startups), but, to my knowledge, there has not been much of a push to open source *websites themselves* and *the processes for creating meaningful content*. I find this somewhat puzzling, since open projects offer so many advantages and so few disadvantages. Below I have layed out my implementation of a completely opensource website and workflow.

### Workflow

Kanban-like boards have been utilized by agile software development teams for years, and they have made the leap into business organization as well. I am fully convinced that they are the best solution to organizing cross-functional teams of people in parallel, especially when there is no heirarchichal leadership structure. They are a perfect match for managing the workflows of open source projects that are organized horizontally.

There are many proprietary options to choose from (such as [Jira](https://www.atlassian.com/software/jira), [LeanKit](https://leankit.com/), [KanbanTool](http://kanbantool.com/), [KanbanFlow](https://kanbanflow.com/), etc.), but I wanted to choose something that was open source at its core, so the project managment from this ste is done through [Waffle.io](https://waffle.io/).

You can see the Waffle.io board for this site here. If you wish to contribute, you're going to have to get added as a contributor by me, so shoot me an email at <a href="mailto:workflow@steventammen.com">workflow@steventammen.com</a>, or message me on GitHub, and I'll get you direct access to the board. If you don't want to play such an active role, you can always just let me know your thoughts and opinions about what should be covered in what order by emailing that same address.

### Content

At the top of every page I have included two buttons that link to its [markdown](https://daringfireball.net/projects/markdown/) source: one links to the page's location in the site's [GitHub Repository](https://github.com/StevenTammen/steventammen.github.io) and the other links to the page's location on [Prose.io](http://prose.io/), an online markdown editor for GitHub.

You can help improve the site's content by submitting pull requests with editorial changes on Github, or by editing the pages on Prose.io and then pressing "Save" --> "Submit Change Request", which will automatically create the pull request for you. Prose.io is great if you don't have a lot of experience with Git and GitHub -- even though you need a GitHub account to propose changes through Prose.io, you need no other knowledge, so once you [set up a GitHub account](https://github.com/join), you can contribute freely without having to know all the complicated programmer stuff. If you aren't comfortable contributing through GitHub or Prose.io, you can also just email improvements to <a href="mailto:content@steventammen.com">content@steventammen.com</a>.

At the present time, I am not aware of any easy way for me to make content editable in a rich text environment, so if you want to contribute through GitHub or Prose.io, you are going to have to learn the basics of [markdown syntax](https://daringfireball.net/projects/markdown/syntax). You won't have to know anywhere near the whole specification to help -- if you skim the sections related to paragraphs, links, lists, and emphasis and you should have a good working knowledge in just a few minutes.

Example Content Improvements:

- Eliminating typos
- Eliminating unecessary verbosity or denseness of prose
- Improving phrasing, flow, or pacing
- Replacing technical jargon and unecessarily large words with more universally understood synonyms
- Splitting up unecessarily long sentences into forms easier to follow, i.e., simplifying syntax as appropriate
- Adding visual aids, such as diagrams, to enhance comprehension
- Anything else you think could make the content better

### Design

You can help improve the site itself by submitting pull requests with design improvements. If you are comfortable with web development languages but not GitHub pull requests, you can send implementations to <a href="mailto:design@steventammen.com">design@steventammen.com</a> and I'll incorporate them into the repository myself. If you aren't comfortable with web development languages or GitHub pull requests, your ideas are still valuable, and you can send them to that same address.

Example Design Improvements:

- Improving the desktop UX
- Improving the mobile UX
- Improving accessibility
- Anything else you think could make the site better

For pull requests requiring significant amounts of work, it would be a good idea to check with me early on to make sure I approve of the changes or enhancements being considered. I don't want to put you in a situation where you put a lot of work into something that I wouldn't ultimately use.

## Copyright and Terms of Use

The contents of this site are licensed under the <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>. Any code associated with subprojects is licensed under the <a rel="license" href="http://www.gnu.org/licenses/gpl.html">GNU General Public License v3</a>.

In short, you may use these materials in any way you see fit so long as you give attribution where it is due and share any derivative works under the same license(s). Both of these licenses are examples of what is commonly termed "copyleft" -- instead of depriving people of freedom, copyleft maximizes the freedom people have to distribute and modify materials while ensuring that this freedom is preserved. To achieve this, copyleft imposes one and only one restriction (in essence): the limitation of further restriction.

You may find information on best practices for the attribution of Creative Commons works [here](https://wiki.creativecommons.org/wiki/Best_practices_for_attribution).
