## CMPUT 301 - Lab 8: Continuous Integration and Test-driven Development

## 1. Walkthrough
1. <ins>Set up</ins>
- Fork this repository
  - Double-check that your forked repository is **public**
- Clone this repository and open the `lab8` folder in Android Studio
  - The starter code provided would feel familiar, as it is the walkthrough code for Lab 6

2. <ins>Confirm continuous integration (CI) is working</ins>
- Make a small change locally (i.e., add a comment, add a newline, etc.)
- Add, commit, and push your small change
- Go to your forked repository and click on the `Actions` tab
  - You should see that your workflow is running automatically after you made the push (notice the yellow icon)
  - It will take a couple of minutes, but while you wait, you can check out the `ci.yml` file in the folder `.github/workflows` from the root directory to see how the CI workflow using GitHub Actions was implemented
- Eventually, you will see that Gradle was able to build and pass the existing tests

3. <ins>Write tests for a method not properly implemented yet </ins>
- We want to implement a new method, `restoreMana()`, but let's do it the test-driven development (TDD) way
- In `Wizard.kt`, write the skeleton for `restoreMana()`:
```kotlin
fun restoreMana(amount: Int) { }
```
- In `WizardTest.kt`, let's write two tests to capture the expected behavior of the method:
```kotlin
@Test
fun restoreMana_amountAddedExceedsOneHundred_manaSetToOneHundred() {
    evilWizard.restoreMana(80) // 30 + 80 = 110, so mana should be set to 100

    assertEquals(100, evilWizard.mana)
}

@Test
fun restoreMana_amountAddedDoesNotExceedOneHundred_manaIncreasesCorrectly() {
    evilWizard.restoreMana(40) // 30 + 40 = 70, so mana should be set to 70

    assertEquals(70, evilWizard.mana)
}
```

4. <ins>Run tests (should fail)</ins>
- Now, add, commit, and push your changes
- Go to your forked repository and click on the `Actions` tab
  - You'll see your workflow running, but since we did not fully implement `restoreMana()`, you will eventually see that it fails

5. <ins>Implement `restoreMana()`</ins>
- In `Wizard.kt`, write the logic for `restoreMana()`:
```kotlin
fun restoreMana(amount: Int) {
    mana = minOf(100, mana + amount)
}
```

6. <ins>Run tests (should pass)</ins>
- Now, add, commit, and push your changes
- Go to your forked repository and click on the `Actions` tab
  - You'll see your workflow running, but since we finally implemented `restoreMana()`, you will eventually see that it passes!

## 2. Lab 8 Participation Exercise
Your turn! We want our wizards to become infinitely more powerful, so let's implement a `train()` method using TDD.
> Specifications for `train()`:
> - No parameters are passed into the method
> - If we have at least 5 `mana`, we increase `spellPower` by 1 and decrease `mana` by 5
> - Otherwise, nothing happens as we don't have sufficient `mana` to train and increase `spellPower`
  
1. Write the skeleton for `train`
2. Write 2 test methods for `train()`
- One test should test if we have enough mana
- The other test should test if we don't have enough mana
3. Add, commit, and push your changes, and see that your workflow FAILS
4. Implement `train()`
5. Add, commit, and push your changes, and see that your workflow PASSES

> [!NOTE]
> - Ensure that you write clear, concise, and informative commit messages!
> - Not following TDD will result in an "incomplete"
>   - You must write the tests first and have the workflow fail at least once before implementing `train()`

## 3. Submission Specifications
1. Update the `README.md` file with your details and references/collaborators
2. Update the `LICENSE.md` file with your full name
3. Submit the link to your GitHub repository on Canvas

> [!IMPORTANT]
> - This lab is graded on a complete/incomplete basis. You will receive a “complete” if you finish the walkthrough, complete the participation exercise, and follow ALL submission requirements. You will receive an “incomplete” if any of these requirements are not met, such as an inaccessible (non-public) repository, missing participation exercise, or an incorrect submission.
> - **There will be no exceptions, partial marks, or late submissions allowed.**
