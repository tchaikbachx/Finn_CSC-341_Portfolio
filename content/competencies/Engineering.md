+++
date = '2026-04-08T08:19:13-05:00'
draft = false
title = 'Engineering'
+++
# Infrastructure
I used VSCode with the Git extension as well as Konsole running as both a standalone terminal and through VSCode. This allowed for quick Git actions (other than making PRs, which had to be done through GitHub via browser) and VSCode itself gave nice formatting for the Python code I was writing.

There was a point where the filesystem was a bit messy and this resulted in packages not being located when they needed to be called; VSCode let me know which packages were causing problems so that [I could adjust their filepaths](https://github.com/tchaikbachx/image/pull/10).

# Self-learning
I learned how to create and populate a SQL table in the tech tutorial using Python, which ended up being pretty useful in my project since we were using Python with SQLite for the back-end, so knowing how to do SQL queries via Python helped a lot.

In the future I would like everyone to be more aware of the `connection` aspect of Python's SQLite library since it's much more managable and less prone to error to have one connection get passed between methods rather than creating a new connection for each method.

# Process
We utilized a Kanban board on GitHub in order to organize what we needed to do on a weekly basis and assign people to those tasks, which could then be checked off as needed. We followed the Kanban board pretty well for the first few weeks of using it, but around the time that our MVP was made, we mostly fell off of using it in favor of using our in-person meetings for planning.

We generally got the most work done during our weekly meetings and not a lot of work done during solo time, so the Kanban board just ended up being somewhat vestigial later on. Despite this, we did maintain a mostly consistent concept of what needed to be done and when, so the work always managed to get done regardless of the somewhat disorganized nature of the board.

# Collaboration
1. There was a bug where some functions were updating the wrong tables, so a [pull request](https://github.com/tchaikbachx/image/pull/12) was created by Sarah to fix this bug. The PR was then reviewed by Collin, who patched up a slight error Sarah made in fixing the bug, and the PR was then sent to me for review. I reviewed the changes from Sarah and Collin and eventually merged them into main after verifying that there wasn't anything else to fix between the two's code.

2. There was a bug where file paths were a bit janky and lead to issues trying to deploy the website on Reclaim Cloud, so I made some adjustments so that the back-end would use relative filepaths instead of absolute ones and created a [pull request](https://github.com/tchaikbachx/image/pull/10) for the changes. These new filepaths have since seen minor edits as needed after talking over them with the rest of the group and testing on Reclaim's end done by Grace.

3. We [needed a testing suite](https://github.com/tchaikbachx/image/issues/7) since at the time we had no testing for any functionality front-end or back-end (there was a note on the Kanban board that had been there for quite some time), so I put together a rudimentary testing file and made a PR for it. This testing file needed assistance from Collin (to write additional tests) and Sarah (to fix problems caused by Flask due to directly calling some back-end functions outside of the front-end). Sarah also wrote tests on the front-end, but I was not involved in their creation.

4. There was some back-and-forth between Sarah and I on the usage of `jsonify()` in making back-end calls, represented by [this issue](https://github.com/tchaikbachx/image/issues/2) on the Kanban board. More specifically, Sarah needed the data from the table to be in JSON format in order to display them on the webpage, but the initial back-end functions just directly took the arguments from the system call, leading to issues. A later version written by Sarah instead used passed arguments in JSON format and then disentangled them in the back-end functions. We discussed to what extent the JSON was needed on the back-end, and this eventually resulted in the current version where the back-end arguments are passed directly while the front-end only uses JSON for `GET` instructions in order to display table information.