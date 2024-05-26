# New server setup and config (decisions involved in selecting server type and power).

## Server Configuration Documentation

## Server Details

- **Server Name:** Web Server
- **Server OS:** Ubuntu 24.04 LTS (Canonical, Ubuntu, amd64 noble image build on 2024-04-23)
- **Architecture:** 64-bit (x86)
- **AMI ID:** ami-04b70fa74e45c3917
- **Instance Type:** t2.small (Family: t2)
- **Volume:** 8 GiB SSD (gp3)

## Reasoning for Server Selection

### Instance Type (t2.small)
- **Purpose:** Chosen for balanced resources and cost-effectiveness.
- **Resources:** Offers 1 vCPU and 2 GiB Memory, suitable for hosting ASP.NET and Next.js applications.
- **Hourly Cost:** USD 0.0464, balancing performance and affordability.

### Suitability for ASP.NET and Next.js Applications
- Both ASP.NET and Next.js applications typically have modest resource requirements, making t2.small adequate.
- 1 vCPU and 2 GiB Memory can support expected workloads without unnecessary overhead.

### Cost Considerations
- t2.small instance helps manage costs effectively, balancing performance and affordability.
- Hourly rate of USD 0.0464 is reasonable for the resources provided.

### Ubuntu OS (24.04 LTS)
- Ensures compatibility with various software packages and libraries commonly used in web development.
- Known for stability, security, and ease of administration, suitable for hosting web applications.

### 8 GiB SSD Volume (gp3)
- Provides sufficient storage capacity for application files, databases, and other resources.
- gp3 volume type ensures reliable performance and flexibility in storage performance adjustments.

## Conclusion
The selected server configuration is well-suited for hosting both ASP.NET and Next.js applications, offering a balance between performance, cost-effectiveness, and scalability.
