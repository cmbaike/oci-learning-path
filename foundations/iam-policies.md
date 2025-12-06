# OCI IAM - Policies and Identity Model

OCI IAM is built on simple, human-readable policies that define *who* can do *what* in *which* compartment.

## Key Constructs

- **Users** → belong to groups.
- **Groups** → assigned policies.
- **Compartments** → logical resource boundaries.
- **Policies** → permissions written in plain language.
- **Dynamic Groups** → machine identities for compute/OKE resources.

## Example Policies

Allow group dev-team to manage instance-family in compartment dev
Allow dynamic-group oke-nodes to read buckets in compartment dev

## Mental Model

People → Groups → Policies → Resources
Machines → Dynamic Groups → Policies → Resources
