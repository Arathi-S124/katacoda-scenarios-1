In this, we'll apply a policy to prohibit unauthorized host paths.

## Reason
This is important because, from a compromised pod, an attacker will be able to access sensitive files through the host path unless authorized host paths have been whitelisted.

We have to apply the ConstraintTemplate and the Constraint.

## ConstraintTemplate
The ConstraintTemplate has to be applied first.
First, we have to open the file and uncomment the rego policy lines that have been commented out after going through the policy. 

We can do this by removing the "**#**" before the start of each line.

For example, 

`#input.review.object.kind == "Pod"` becomes `input.review.object.kind == "Pod"`

Now we can apply the template.

`kubectl apply -f template.yaml`{{execute}}

## What the Rego policy does
- Checks if the kind is "Pod".
- Stores the host path in a variable.
- Finally checks if the host path used is in the allowed paths list passed as a parameter.
 
## Constraint
Take a look at the constraint.yaml file and then apply the constraint.

`kubectl apply -f constraint.yaml`{{execute}}

**NOTE:** If "no matches for kind" error comes when applying the Constraint file, try the following fixes:
- Make sure all the rego policy lines have been uncommented. 
- Apply the template.yaml and the constraint.yaml again.
- If the error still persists, try applying the constraint.yaml again after a couple of minutes.

