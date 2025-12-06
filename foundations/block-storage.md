# OCI Storage Fundamentals - Block, Object, Archive

OCI offers several storage options optimized for different use cases and cost models.

## Block Storage

- High performance disks for compute instances or OKE worker nodes.
- Suitable for stateful apps, databases, and OS boot volumes.

## Object Storage

- Durable, scalable storage for logs, files, artifacts, backups.
- Similar to AWS S3.

## Archive Storage

- Lowest cost tier for long-term, infrequently accessed data.
- Ideal for compliance backups and archival datasets.

## Cost Optimization Principle

Move data based on lifecycle:
Block → Object → Archive
