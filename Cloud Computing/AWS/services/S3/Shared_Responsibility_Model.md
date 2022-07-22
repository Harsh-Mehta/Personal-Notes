# Amazon Simple Storage Service (S3)

## Shared Responsibility Model
+-------------------------------------------------------------------------------------------------+----------------------------------+
| AWS                                                                                             | User                             |
+=================================================================================================+==================================+
| * Infrastructure (global security, durability, availability, sustain concurrent loss of data in | * S3 Versioning                  |
| two facilities)                                                                                 | * S3 Bucket Policies             |
| * Configuration and vulnerability analysis                                                      | * S3 Replication Setup           |
| * Compliance validation                                                                         | * Logging and Monitoring         |
|                                                                                                 | * S3 Storage Classes             |
|                                                                                                 | * Data encryption at rest and in |
|                                                                                                 | transit                          |
+-------------------------------------------------------------------------------------------------+----------------------------------+