+++
date = '2026-04-08T08:19:13-05:00'
draft = false
title = 'Verification'
+++
# Testing Strategies
Since I wrote most of the back-end, I was also responsible for running some tests on it. In particular, I needed to test the functionality of adding, deleting, and changing entries in any given table. In order to test these, I made some dummy instruments and used them to manipulate a test database which was both initialized and deleted as part of the testing process, running unit tests to make sure that bad data couldn't be added to the tables. Examples of these can be found below:
```Python
# try to delete entry with ID = 0
try:
    man.delete('instrument', "0")
    print("PASS test: deleted entry 0")
except Exception as e:
    print("FAIL test: failed to delete entry 0 (" + str(e) + ")")

# try to add a dummy instrument back into table at ID = 0
try:
    man.add('instrument', jsonify(dummy))
    print("PASS test: added dummy instrument to table at ID = 0 after deletion")
except Exception as e:
    print("FAIL test: failed to add dummy instrument to table at ID = 0 after deletion (" + str(e) + ")")

# try to edit entry that doesn't exist
try:
    man.update('missing', "3", jsonify(dummy))
    print("FAIL test: did not throw exception trying to edit null entry")
except Exception as e:
    print("PASS test: threw exception trying to edit null entry (" + str(e) + ")")
```
These tests do not cover every table, instead focusing on the `instrument` table. That table is the most important one and all of the other tables reuse code from it, so while other tables may silently break, they would be much easier to fix compared to the `instrument` table and likely not indicate any larger problems with the codebase.

# Testing Infrastructure
When the server is spun up, it runs `testing.py` so that if any errors crop up in the actual running of the server, the tests will already have been run and printed in the console. Unfortunately this cannot cover for issues on Reclaim Cloud's end, but nothing can really be done about that.

These tests let us know that the update functions were broken before we put those changes up on Reclaim Cloud, which is great since updating the server on Reclaim's end is usually pretty slow.