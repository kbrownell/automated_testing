# Automated Testing
Lessons learned automating Drupal 7 tests with Behat and TravisCI

[Stanford Behat Tests](https://drupalcamp.stanford.edu/lessons-learned-2-years-using-behat)

[Stanford TravisCI Scripts](https://github.com/SU-SWS/stanford_travisci_scripts)

Why we chose to automate the running of our tests
---
1. [Is It Worth the Time?](https://xkcd.com/1205/) It was, we were at about 6hrs/week (and it took about 2 months of billiable time).
2. We had a growing team.
3. Impressive suite of behat tests (first phase of automating tests; before my time).
4. Increasing nervousness over the potential for problems and opportunities for human error.
5. Clients ready to pay for tests to become part of their definition of done.
6. We had resources for training (I was new) and infrastructure.

Constraints
---
### Had to:

1. Be free and we didn't want to host the CI application.
2. Integrate with GitHub.
4. Build our products.
5. Work with existing tests.

### Testing priorities from clients:

1. Site looks professional.
2. Data is accurate and complete.
3. Layout and organization are as planned.
4. Site functions (for admins and editors) as expected.

### Priorities from our team:

1. Reduce the time between development (or security announcement) and deployment.
2. Reduce the amount of code changes tested at once, so that we can find and fix bugs more quickly.
3. Reduce the amount of time we spent running tests manually.
4. Include test results as part of our code review process, without the added burden of manually running tests per pull request.

Current Toolchain
---
**Module Development:** Local > GitHub Pull Request > CodeClimate > Travis/Behat

**Profile Version Upgrades:** [Update Profiles](https://github.com/SU-SWS/stanford_upgrade_scripts/tree/master/upgrade_modules) > GitHub Pull Request > CodeClimate > Travis/Behat

**Production Code Upgrades:** [Copy over code from Profile Builds](https://github.com/SU-SWS/stanford_upgrade_scripts/blob/master/upgrade_modules/includes/upgrade_functions.inc#L136) > Manually Deploy to UAT > Manually Test with Behat > Manually Deploy to Production > Manually Test with Behat

### Why we like Behat:

1. Because Behat tests emulate keyboard navigation, they help us test for the accessibilty of our sites.
2. Widespread adoption by the Drupal community.

### Why I liked TravisCI:

1. Sensible defaults, ie. never had to adjust MySQL max_packet_size, came with Firefox, etc.
2. Prints out container defaults.
3. Free for open source projects; if we had to pay, not based on disk space (which is harder to control).
4. Allows secure environment variables for public repositories, so we don't have to store credentials in code.
5. Their favicon indicates build status, which won my heart.  They get that these processes should and will be running in the background of our browser.
6. Able to get a local copy up and running pretty quickly.
7. I was able to find many public repositories using TravisCI with Drupal and Behat, as well as lots of good documentation.

### Novice mistakes:

1. Not testing the origination branch of a pull request.
2. Not running all tests for a module or product.  It still passes, but isn't testing all that we wanted it to test.
3. Not setting up a local copy of the CI tool right away.  If you're troubleshooting runserver or file paths, no point in waiting for an entire site to build each time you want to try something new.
4. If you're running tests within a script, so not straight from a command in the .yml file, then be sure you force a failing exit code if at least one test fails ([example](https://github.com/SU-SWS/stanford_travisci_scripts/blob/behat-7.x-1.x/bin/script.sh#L20-L27)).

If we did less, we'd have
---
1. Written fewer Behat tests.
2. Added TravisCI to fewer repositories.
3. Exclude Javascripts tests entirely, which means we wouldn't have needed to setup Selenium and xvfb.

If we did more, or when we start working on D8
---
1. If we had a pattern library or style guide, try shoov for visual regression testing.
2. Automate tests for individual, custom client sites, ie. not just our modules and products.
3. Automatically update product make files when new module release is tagged (that would be really nice!).
4. Rewrite a number of our tests, so that they perform functionality not just check if fields and text can be found.
5. Reorganize tests, so that they travel with their related code, instead of being housed in a single test repository.
6. Automate deployment of changes to UAT sites.

If you're just getting started
---
I'd recommend watching Lynda.com's [DevOps Fundamentals Course](https://www.lynda.com/Operating-Systems-tutorials/DevOps-Fundamentals/508618-2.html).
