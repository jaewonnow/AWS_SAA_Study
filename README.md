# Week 1: AWS Global Infrastructure & IAM

## 🎯 Goal
Understand the physical layout of AWS and master the permission system.
"If you don't know this, everything else will be confusing."

## 📚 Topics

### 1. AWS Global Infrastructure
- **Region**: Independent geographic areas.
- **Availability Zone (AZ)**: Isolated locations within a Region.
- **Edge Location**: Endpoints for AWS which are used for caching content (CloudFront).

### 2. IAM (Identity and Access Management)
- **User**: An entity that you create in AWS to represent the person or application that uses it to interact with AWS.
- **Group**: A collection of IAM users.
- **Role**: An identity with permission policies that determine what the identity can and cannot do in AWS.
- **Policy (JSON)**: A document that defines one or more permissions.
- **AssumeRole**: A way to grant temporary access to users or services.

### 3. Shared Responsibility Model
- **Security OF the Cloud**: AWS responsibility (Hardware, Global Infrastructure).
- **Security IN the Cloud**: Customer responsibility (Data, Configuration, IAM).

## 💡 Key Point
Every service problem has a potential "Permission/IAM" solution hidden in it.
