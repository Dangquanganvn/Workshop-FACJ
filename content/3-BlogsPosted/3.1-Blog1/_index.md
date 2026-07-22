---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Multi-AZ or Read Replica? I used to get them mixed up too!

When I first started learning about Amazon RDS, I used to confuse **Multi-AZ** with **Read Replicas**—a common mix-up for many newcomers to AWS. While both features create database copies, they serve completely different purposes. In this article, I will summarize the key differences to make them easier to remember.

Key points to know:

* Multi-AZ
    * Goal: High Availability (HA).
    * Synchronous data replication.
    * Includes a standby database in a different Availability Zone (AZ).
    * Automatic failover if the primary instance fails.
    * Does not handle read queries; does not improve performance.

* Read Replica
    * Goal: Read Scaling.
    * Asynchronous data replication.
    * Handles SELECT queries to offload the primary instance.
    * Replication lag may occur.
    * No automatic failover if the primary instance fails.
* Quick Summary
    *  Multi-AZ = System resilience (HA).
    *  Read Replica = Increased read capacity (Read Scaling).
    *  In production systems, these two features are often combined to ensure both high availability and improved performance. 

![Your BlogsPosted picture](/images/3-BlogsPosted/Blog1.png)

[...Link...](https://www.facebook.com/groups/660548818043427/user/100022580752820)

