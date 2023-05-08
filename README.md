# Daml Fundamentals Certificate Sample App

✨ Welcome to the Daml Fundamentals Certification Sample App! ✨

As part of the certification process, you will be required to complete a backend-only capstone project that demonstrates your understanding of the material covered throughout the Daml Fundamentals Certification Path. You have the freedom to choose the topic of your project as long as it fulfills the criteria specified below. 

**The project must include the following components that are fully operational:**

+ A signatory with the authority to create and archive contracts
+ A controller with the authority to exercise choices on contracts
+ An observer with the authority to view contracts
+ Test scripts that verify the functionalities of the above mentioned parties

**Bonus points will be awarded if you implement the following features:**

+ Use the propose / accept design pattern
+ Use the try / catch block for error handling

**We will score all required and bonus features (6 in total) by the following:**

+ The feature is free of bugs
+ Only authorized users have access to the feature
+ The feature can be tested appropriately
+ TX is not unexpectedly aborted 

🚨 **IMPORTANT NOTE** 🚨
+ **The evaluation of your project requires a README that adheres to the format provided in the README of the sample project below.**

+ Your README should document the purpose and functionalities of the project, as well as any important details about how it works. The README file should also include instructions on how to run the project, how to run the tests, and any dependencies required to do so. This documentation will help others understand your project and how to use it, and will also demonstrate your ability to clearly communicate about your work.

To help you prepare for your capstone project, we provide this sample app as a guide for the kind of app you should aim to build. The sample app has been designed to showcase the key concepts and skills that you will need to apply in your own project.

We recommend that you examine this app closely, paying attention to the code structure, functionality, and the test script. We believe that this sample app will be an invaluable resource for you as you work towards your certification. Happy coding!

---

# DamlForge App
Daml templates designed for a platform for proposing project ideas to get rejected/approved.

### I. Overview 
This project was created by using the `empty-skeleton` template. The project adopts and exemplifies the `proposal-accept` design pattern. A signatory can create a ProjectIdea contract. Then they can exercise the Propose choice as a controller to get the project proposal either approved or rejected by their manager. If the manager, a controller, exercises Reject choice on the proposed contract, the employee can exercise Revise choice on it to re-propose the project with updated details. Upon manager exercising the Accept choice, a Project contract is created.

### II. Workflow
1. An employee creates a ProjectIdea contract. Both colleague and manager are invited as obeservers, but manager, as a controller, is authorized to exercise either Reject or Accept choices.
2. Upon the controller exercising Reject, a new contract is created.
3. Revise choice can be exercised on the newly generated contract from above.
4. Accept choice is exercised to finalize the project idea and generate a new Project contract.

[![Demo](./Demo.png)](https://share.vidyard.com/watch/xbDuZMbNUbgfHmPnqzt72N?)

### III. Challenge(s)
* `controller ... can` syntax causes warning in Daml 2.0+. The code itself does not cause any issues/errors in 2.5.0 but according to the warning, the syntax will be deprecated in the future versions of Daml. More information [here](https://docs.daml.com/daml/reference/choices.html#daml-ref-controller-can-deprecation).
* The new controller syntax requires a controller to be an observer first before they can exercise a choice, otherwise it'll throw an error: "Attempt to fetch or exercise a contract not visible to the committer." For more information, check out [this post](https://discuss.daml.com/t/error-attempt-to-fetch-or-exercise-a-contract-not-visible-to-the-committer/1304/1) on the Daml Forum.
* The project was created by using `empty-skeleton` and the following was removed from `daml.yaml`:
```
sandbox-options:
   - --wall-clock-time
```
and replaced with the following:

```
exposed-modules:
  - Main
navigator-options:
 - --feature-user-management=false
```
For more info, check out [this post](https://discuss.daml.com/t/sandbox-options-wall-clock-time/5692/16?u=cathy_jung) on Daml Forum and [Daml Doc](https://docs.daml.com/tools/navigator/index.html?&_ga=2.48248804.337210607.1673989679-241632404.1672853064&_gac=1.17025355.1673455980.CjwKCAiA2fmdBhBpEiwA4CcHzfI2w1_D95zAr3_d6QTypOMXGTpUxtS06c55inucNwZvUZn4AebsJxoCZEgQAvD_BwE&_gl=1*elem6v*_ga*MjQxNjMyNDA0LjE2NzI4NTMwNjQ.*_ga_GVK9ZHZSMR*MTY3Mzk5NDQzOS4zMS4xLjE2NzM5OTQ3MDcuMC4wLjA.#logging-in-as-a-party).


### IV. Compiling & Testing
To compile and test, run the pre-written script in the `Test.daml` under /daml OR run:
```
$ daml start
```
