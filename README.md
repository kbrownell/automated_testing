# Automated Testing
Lessons learned automating Drupal 7 tests with Behat and TravisCI

[Stanford Behat Tests](https://drupalcamp.stanford.edu/lessons-learned-2-years-using-behat)

[Stanford TravisCI Scripts](https://github.com/SU-SWS/stanford_travisci_scripts)

Why we chose to automate our tests
---
1. [Is It Worth the Time?](https://xkcd.com/1205/) It was, we were at about 6hrs/week.
2. We had a growing team.
3. Impressive suite of behat tests.
4. Increasing nervousness over the potential for problems and opportunities for human error.
5. Clients ready to pay for tests to become part of their definition of done.
6. We had resources for training (I was new) and infrastructure.

Constraints
---
Had to:

1. Be free and we didn't want to host the CI application.
2. Integrate with GitHub.
4. Build our products.
5. Work with existing tests.

Testing priorities from clients:

1. Site looks professional.
2. Data is accurate and complete.
3. Layout and organization are as planned.
4. Site functions (for admins and editors) as expected.

Priorities from our team:

1. Reduce the time between development (or security announcement) and deployment.
2. Reduce the amount of code changes tested at once, so that we can find and fix bugs more quickly.
3. Include test results as part of our code review process, without the added burden of manually running tests per pull request.

Current Toolchain
---
Module Development: Local > GitHub Pull Request > CodeClimate > Travis/Behat

Profile Version Upgrades: [Update Profiles](https://github.com/SU-SWS/stanford_upgrade_scripts/tree/master/upgrade_modules) > GitHub Pull Request > CodeClimate > Travis/Behat

Production Code Upgrades: [Copy over code from Profile Builds](https://github.com/SU-SWS/stanford_upgrade_scripts/blob/master/upgrade_modules/includes/upgrade_functions.inc#L136) > Manually Deploy to UAT > Manually Test with Behat > Manually Deploy to Production > Manually Test with Behat

Why we like Behat:

1. Accesibility
2. Functionality is mostly what we care about

We I liked TravisCI

1. Sensible defaults
2. Prints out defaults
3. Free for open source projects

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
