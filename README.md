# apic-gitops

The objective of this operator is to provide a gitops based approached to publishing APIs in IBM's API Connect.


This is designed around a githubs repo that contains all apis/products for a catalog/space/channel where the following branches exist.
1. agnostic - where the developer checks in the environment agnosti code
2. SIT - Where the API is tested formally
3. NFT Test  - Long Running test
4. Prod  - Prod

# CR
Each CR will have three key variables
1. Current Environment
2. Repo
3. Branch
4. Last publish time
5. Which is the next environment in the flow.

Each CR will watch the github repo and branch to see if there is a change.
If there is a change the following flow is done.
1. Products and apis cloned from the repo-branch
2. Compare the products name and version to those already deployed in APIC
3.  If there is a product that is in the repo but not in apic  check to see if there is a product with an earlier minor version but the same major version,
4. If there is a product with the same major version but an earlier major version, replace the existing the product with this one,
5. if not (to any of the ifs) just publish this without replacing what is there
6. If there is a product that is in APIC but not in git then retire+delete the api.


How do we handle Rollback??
How do we handle Build??
