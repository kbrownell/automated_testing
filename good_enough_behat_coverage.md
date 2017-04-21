~50 min cap

General Best Practices:
---
* Clean up after yourself.
  * Write non-destructive tests. Something that leaves permanent change.
  * Don’t leave artifacts.
* All test should pass.
* Only test for seeded content. Do not assume content from other places.
* Write genericized tests as much as possible in order to span as many “life-spans” as possible.
* Do not deprecate bug tests.
  * Regression testing is super valuable. No need to remove after a period of time.
* Try to avoid @javascript when possible (slow).
* Do not use “wait N seconds” steps (use I wait for ajax to finish) it is smarter.
* Use git-crypt when storing authentication credentials. (actually, we're still figuring this one out.)
* Keep tests maintained and up to date with change.
* Test to ensure things work under normal situations. Don’t go heavy on edge case.
  * Example: Test to submit a field with good value input vs garbage.
* Works on local and remote (sometimes tests that work on Sites will fail on local because local is too fast and you need to add a “And I wait for AJAX…” or “And I wait for the batch…”
* Use the goutte driver testing over selenium as it is better for accessibility.
* You do not need to test for aesthetics or visual placement. Test for existence of items.
  * Unless it is for usability.

Module Specific:
---
* Create tests for any user stories that are available.
  * Process driven and sometimes in Jira.
* Anything the client has deemed high value in their business needs/goals needs to be tested.
  * Ask team members / clients what is important?
* Read the module’s code and test for all major components.
  * Should test for all sub modules included in parent module.
  * If module has a content type or entity please test for entity creation.
  * Beans / Blocks / Views / Contexts
  * All fields exist and display or are hidden.
  * hook_menu, form_alters, entity_alters, preprocess_hooks work.
  * Display modes (entities)
  * Installed settings
  * Integrations (3rd party) Feeds, Apis, etc.
  * Pages / urls exist and display
  * Any accessibility improvements or fixes are tested
* Separate your feature files per module and sub module
  * Granularity is good
* Test for previously experienced bugs (regression testing)
* Test for the three A’s (Anon, Auth, and Admin)
* Actually authenticate to any external services
* Test in the lowest common denominator build (Stanford Sites) when possible

Product Specific:
---
* Create tests for any user stories that are available
* Should test for any specific configuration of a shared component.
  * IE: If you change settings on the stanford_news module you alter the tests that are run for this product.
  * Sometimes product tests will need their own override or copy of the shared set
* Previously experienced bugs (regression testing)
* Check for specific roles included and bundled in the product level
* Testing for existence of default content is ok here (careful)

Site Specific:
---
* Anything the client has deemed high value in their business needs/goals
  * Ask team members / clients what is important?
* It is the site owner / development team’s responsibility to maintain tests after the site has been changed.
