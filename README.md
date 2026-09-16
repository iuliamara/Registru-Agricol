# Registru-Agricol
A full-stack, multi-tenant agricultural register platform designed to digitize and streamline agricultural administration.

This project was developed collaboratively as part of a team project.

The application provides a centralized environment for managing agricultural holdings, land parcels, citizens, administrative units, documents, and tenant-specific workflows. It supports multiple user roles, including citizens, tenant administrators, and super administrators, while maintaining secure data separation between tenants.

Features
Multi-tenant architecture with tenant-specific data isolation
Role-based access control for citizens, tenant admins, and super admins
Agricultural holding and land parcel management
UAT (Unitate Administrativ Teritorială) management
Citizen portal and account-based interactions
JWT-based authentication and authorization
Document and contract management
Audit logging and data change tracking
Administrative dashboards
Public and tenant-specific database schemas
REST API architecture
Kafka-based messaging and integration support

Tech Stack

Backend

Java
Spring Boot
Spring Security
JPA / Hibernate
Maven

Frontend

Angular
npm

Database

PostgreSQL

Infrastructure & Integration

Docker
Docker Compose
Apache Kafka
JWT Authentication
Git


Purpose

The goal of the project is to reduce paperwork and improve the management of agricultural records by providing a secure and structured digital platform for public administration institutions, local agricultural offices, citizens, and platform administrators.

The system focuses on data separation, traceability, transparency, and centralized management across multiple administrative tenants.
