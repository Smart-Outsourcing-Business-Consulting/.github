# How to customize modules 101 (summarized)

## Branch selection for fork/cloning
Determine which branch to use as base for copying. You can use the compare feature of github to determine which branch has the latest change. For example, if the home page of the github repo 
is [https://github.com/odoo/odoo](https://github.com/odoo/odoo), append /compare to it like this [https://github.com/odoo/odoo/compare](https://github.com/odoo/odoo/compare). 
From there you can choose 2 branches to compare e.g. production and staging. Below are several articles on Github that explain its use.
- [Comparing Commits and Branches](docs.github.com/en/pull-requests/committing-changes-to-your-project/viewing-and-comparing-commits/comparing-commits)
- [Three-dot and two-dot Git diff comparisons](docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-comparing-branches-in-pull-requests#three-dot-and-two-dot-git-diff-comparisons)
  
> [!TIP]
> In a well-managed github repo, this should be straightforward. If you are not sure which to use, **ASK**.

## Include and initialize git submodules
If you are going to work locally, use the ready-made git command in the Odoo.sh project to make sure you download and initialize any submodules that may be present. Do note that you **WILL** need to change the branch name.

![image](https://github.com/user-attachments/assets/66d72ad3-0064-4110-954b-9c85ccbb8daa)

## Name dev branch properly
All DEV branches should start with 'DEV-' in capital-case, followed by the (custom) module being modified, dash, followed by a description of the change/fix/upgrade in [imperative form](https://www.scribbr.com/verbs/imperative-mood/). 
### Example:
If I am fixing a pom calculation issue in bi_product_dimension in Dragon, the branch name would be DEV-bi_product_dimension-fix-pom-calculation-issue.

## Check for whitespace errors
Check for whitespace errors before you commit by using ```git diff --check``` on unstaged changes and ```git diff --cached --check``` for staged changes. 
See [git-diff documentation](https://git-scm.com/docs/git-diff) for more information.

## Commit according to guidelines
Follow the guidelines for committing explained in [README.md document](README.md)

## Update local branch with latest remote branch changes
Update the branch you are developing each day with the latest changes. You do that by merging the branch you copied from into the branch that you are working on. Use git pull --rebase locally
the update from the branch and keep a linear history. If there are merge conflicts, ASK how to resolve them. 
### Example: 
you copied the production branch on github/odoo.sh and called the new branch A, you clone the project on your pc. You need to merge remote production into local branch A so you run
 ```git pull --rebase origin production``` if those locals commits have not been pushed to the remote branch with other developers working on it or else git pull origin production.

## Test before you push to remote branch
Test the newly commited code using its dependencies' tests be it either the tests of another custom module, odoo standard modules' tests and/or the module's tests. 
In settings page of the remote branch on Odoo.sh, make sure the option ' Validate the test suite on new builds. ' is turned on and fill in the module dependencies prepended by '/'.
PRs for which tests have not been correctly configured and executed will not be accepted. See Odoo [documentation](https://www.odoo.com/documentation/18.0/developer/reference/backend/testing.html#test-selection) on selecting tests.
### Example:
If your module 'A' depends on 'stock_landed_cost', 'sale_management','account',and 'industry_fsm' then you should write in that field
>/stock_landed_cost,/sale_management,/account,/industry_fsm,/A

## Make PULL request according to guidelines
Follow the guidelines for making Pull Requests explained in 📄 Git with Stephen feedback

> [!CAUTION]
> Do not delete the remote branch until it has been merged with production branch. It would be done by one of the repository admins.
    
