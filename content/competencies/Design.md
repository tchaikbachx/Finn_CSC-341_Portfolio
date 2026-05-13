+++
date = '2026-04-08T08:19:13-05:00'
draft = false
title = 'Design'
+++
## Needfinding
The needfinding preocess began with Collin's personal experiences working with the music checkout system; this then lead to an observation session I had with him while he was working with the current system. This produced some notes, which can be found [here](https://github.com/tchaikbachx/Needfinding-and-Ideation/blob/main/Needfinding%20and%20Ideation.odt) under "Observation #2 (Finn observing Collin)", which is shown below:
>       Observation #2 (Finn observing Collin):
>     • I want a sax
>     • goes to saxophone page (lives somewhere in the filesystem (system -> music checkout -> instruments -> brass & woodwinds -> woodwind saxes.excel)
>     • all of the ones with names are being borrowed, so look for the first one without a name
>     • does that instrument actually exist (check locker physically)
>     • is it in good quality
>     • once I give green light on chosen instrument...
>         ◦ fill out current date, due date, and student email
>         ◦ fill out checkout list on paper (kinda useless nowadays)
>         ◦ student gets email (someone manually emails them)
>         ◦ student is told the locker and combo numbers in the email
>         ◦ student can reply to email if they need additional assistance
>         ◦ double-check that all data was actually populated (old-ass excel formulas handle all of that and sometimes they break)

These observation notes then served as a basis for what needed to be addressed by the prototyping phase. In particular, a reoccurring theme was how manual the entire system was, requiring the user to perform several easily-automatable tasks such as emailing borrowers which could be (and were, by Collin's memory) just as easy for the human user to forget to do.

## Ideation
After my observation of Collin, I did some [text ideation](https://github.com/tchaikbachx/Needfinding-and-Ideation/blob/main/Prototyping.odt), shown below:
>     • 2-pane view
>         ◦ one pane has all of the instruments (with search bar)
>             ▪ clicking on instrument blows up details on it
>         ◦ other pane has actions
>             ▪ checkout
>             ▪ add
>             ▪ remove
>             ▪ other stuff idk
>     • python + sql + docker for back-end
>     • whatever web stuff for front-end
>     • 2 branches?
>         ◦ inventory system and checkout system separate
>             ▪ would be nice for profs to be able to just see the inventory without needing to edit things
>             ▪ what would profs want to do?
>                 • search for instruments
>                 • some kind of export system for paper or excel formats
>                 • add/remove entries
>         ◦ some inventory thing -> checkout system front-end
>     • data fields
>         ◦ family (brass, woodwind, etc)
>             ▪ type (trumpet, flute, etc)
>                 • name + id (sequential ids)
>     • locker class
>         ◦ contained instruments list
>     • instrument class
>         ◦ what am I
>         ◦ where am I
>         ◦ who owns me

I spoke with Collin about these points while writing them, and we bounced ideas off each other. We did some basic testing where we said out-loud what which button-presses and similar actions could be saved by doing these things. The 2-pane view concept arose from the desire to see all of the relevant data in one place, as switching between several excel tabs and files was very taxing for the user both in terms of time and effort. 

Consequently, we decided that one of the things the final product would need to have is a filtering system to aid with the planned master instrument list, and we would also like to have everything easily *visible* at a glance, as poor accessibility was one of the issues with the old system.

## Prototyping
Extending from needfinding, we got to work on a [paper prototype](https://github.com/tchaikbachx/Prototyping/blob/main/prototype.jpeg). In particular, I made the pane at bottom-left of the image.
![image](./prototype.jpeg)

These prototypes built off of the complaints raised during the needfinding process. In particular, we identified that the instruments should exist in a unified view where all of their info can be seen simultaneously, as the current system uses several tabs in an excel sheet, requiring a lot of looking around for stuff. Likewise, we put all of the relevant table actions ("checkout", "add", "remove", as noted above) alongside the info pane for easy access. Our prototypes then went to Erik Jarvis for review, and he responded favorably.

## Evaluation
I got a friend who isn't familiar with the Music Checkout Department to try engaging with the system as a student and operator, and had him give his thoughts on how straightforward everything was to navigate and understand. He liked the UI and thought it was pretty simple to use the filters to find instruments, but thought that the admin access was a little weirdly positioned on the page and that it should have more information on the Music Checkout Department in general.

Our average user will be more familiar with the department than him, so this wasn't a major concern but we decided to include plenty of information on it in the final product anyway just in case. We also added another admin login button lower on the page to make it easier to reach when reading the policies on the main page.
