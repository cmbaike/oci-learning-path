# OCI IAM - Identity Domains, Policies, and Access Model

OCI Identity and Access Management (IAM) provides the framework for authentication (who you are) and authorization (what you can do). It combines identity domains, users, groups, policies, and compartments into a clear, hierarchical access model.

---

## 1. Identity Domains

An **identity domain** is a boundary for managing users, groups, authentication methods, and IAM configuration.

Every tenancy starts with a default identity domain, and additional domains can be created for isolation or federation needs.

Inside an identity domain, you create:

- **Users**
- **Groups**
- **Dynamic groups**
- **Federation rules**
- **Authentication policies**

Identity domains manage *identity*, but **do not define authorization** — that is done through policies.

---

## 2. Users and Groups

### Users

Represent people (human identities).
They sign in to OCI through an identity domain.

### Groups

Collections of users.
Groups are used to **assign authorization via policies**.

> OCI best practice:
> **Never assign permissions to individual users. Always assign to groups.**

---

## 3. Compartments

A **compartment** is a logical container used to organise and isolate resources.

Examples of resources inside compartments:

- Compute instances
- VCNs
- Buckets
- OKE clusters
- Load balancers

Policies typically reference compartments when defining what groups can do.

---

## 4. Policies (Authorization)

A **policy** grants a group or dynamic group permission to interact with OCI resources.

Policies are written in plain English:

Allow `<subject>` to `<verb>` `<resource-type>` in `<location>`

### Syntax Example

Allow group dev-team to use instance-family in compartment dev

### Where Policies Live

Policies can be created at:

- **Tenancy level (root)** → affects the whole organization  
- **Compartment level** → affects only the target compartment  

### Important Clarification

Policies **do not live inside identity domains**.  
Policies define *authorization*, not authentication.

---

## 5. Dynamic Groups

Dynamic groups provide identities for **non-human principals**:

- Compute instances
- OKE worker nodes
- Functions
- Other OCI services

Membership is rule-based.

Example rule:
Any instance in compartment dev-comp where instance.name = 'web-server'

Policy referencing a dynamic group:
Allow dynamic-group web-servers to read buckets in compartment dev

Dynamic groups are essential for:

- OKE
- Automation
- CI/CD pipelines
- Headless services

---

## 6. Putting It All Together (Correct IAM Flow)

1. Identity domain is created.
2. Users and groups are defined inside the identity domain.
3. Compartments are created for resource organization.
4. Resources are launched inside compartments.
5. Policies are created at tenancy or compartment level.
6. Policies reference groups or dynamic groups, granting them permissions on resources.

---

## 7. Canonical OCI Policies Examples

### Read-only access to a compartment

Allow group auditors to read all-resources in compartment prod

### Admin rights for a platform team

Allow group platform-admins to manage all-resources in tenancy

### Allow OKE nodes to pull from Object Storage

Allow dynamic-group oke-nodes to read buckets in compartment dev

### Allow DevOps team to manage compute

Allow group dev-team to manage instance-family in compartment dev

---

## Mental Model Summary

- **Identity domain** → where users & groups live
- **Groups** → who gets permissions
- **Policies** → what they can do
- **Compartments** → where they can do it
- **Resources** → what they access
- **Dynamic groups** → machine identities

Mastering this structure is essential for OCI architecture, security, DevOps, and OKE deployments.
