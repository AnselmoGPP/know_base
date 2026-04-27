# Moodle

## Table of Contents

+ [References](#references)
+ [Introduction](#introduction)

## References

- [Moodle.org](https://moodle.org/)
- [Installation guide for Ubuntu](https://docs.moodle.org/501/en/Step-by-step_Installation_Guide_for_Ubuntu)

## Introduction

**Moodle** is a LMS (Learning Management System) that is open-source, PHP-based, and very customizable.

**Hosting**: Moodle is resource-intensive because it handles many concurrent database requests. If you need control over the environment and the ability to scale, don't use shared hosting. There're three main paths:

- **MoodleCloud**: A SaaS solution hosted by Moodle. Great for small schools; no technical setup required, but limited customization.
- **Self-Hosted** (Recommended for Institutions): You install Moodle on your own server (AWS, Google Cloud, or a dedicated VPS). This gives you full control over plugins and user limits.
- **Moodle partners**: Certified service providers who handle the technical heavy lifting for you.

**Stacks**: Combinations of software components for building applications. A Moodle server requires:

- **Linux**: Free OS.
- **Web server**: Such as Apache, Nginx, Litespeed, or IIS.
- **Database server**: Such as PostgreSQL, MySQL, MariaDB, Aurora MySQL or Microsoft SQL Server.
- **PHP**: Scripting language in which Moodle is developed. It's integrated with the web server, which detects php pages (by their extension) and sends them to PHP for execution.

Popular stacks:

- **LAMP**: Linux + Apache + MySQL/MariaDB + PHP/Python/Perl. A traditional, mature stack ideal for dynamic websites.
- **LEMP** (recommended): Linux + Nginx + MySQL/MariaDB + PHP/Python/Perl. A high-performance variant of LAMP. Nginx (lightweight, event-driven) handles concurrent connections more efficiently (ideal for high-traffic sites and static content delivery).

**Infrastructure** recommendation:

- **Environment**: Ubuntu 24.04 or 26.04 LTS.
- **Stack**: LEMP (Linux, Nginx, MariaDB/PostgreSQL, PHP 8.3+). Nginx is generally preferred over Apache for Moodle’s high concurrency needs.
- **Hosting**: AWS (EC2 + RDS) or DigitalOcean. Start with at least 4GB RAM and 2 vCPUs. Moodle is a memory-heavy application.
- **Storage**: Use S3 or an external block storage for the moodledata directory, as this will house all student uploads and videos.

Install Moodle using **Git** so you can easily pull security patches and upgrades.

```
cd /var/www/html
git clone -b MOODLE_405_STABLE git://git.moodle.org/moodle.git  # Use the latest stable (e.g., 4.5 in 2026)
```

**Configure** Moodle to make it look interesting. Options:

- **Boost** default.
- **Moove**: Modern, clean, "SaaS-like" look.
- **Edwiser RemUI**: Professional dashboard interface.
- **Adaptable**: Highly customizable.

**Plugins**: There're many interesting ones:

- **CodeRunner: Essential**: Create quiz questions where students write actual code (Python, C++, Java…) which is then executed and graded in a sandbox.
- **VPL (Virtual Programming Lab)**: Provides a full IDE inside Moodle with a private execution server.
- **Configurable reports**: Get data on student progress.
- **H5P**: For interactive video lectures and "branching" scenarios.

**Hierarchy**: Moodle has a specific one. You should map it out like this:

- **Site home**: Campus landing page
- **Categories**: Faculties (engineering school, data science school…)
- **Sub-categories**: Programs (Cybersecurity track…)
- **Courses**: Individual modules (Intro to distributed systems)

**Automation & Integration**: Don't manually enroll students.

- **Auth**: Connect Moodle to **Keycloak** or **Auth0** for professional SSO (Single Sign-On).
- **Enrollment**: Use the **Stripe Payment Plugin** so that once a student pays, they are automatically enrolled in the course.
- **API**: Use Moodle's Web Services (REST API) to sync student data with your marketing site or a custom-built dashboard.

**Security & Compliance**:

- **Cron Job**: Moodle requires a cron job to run every minute to send emails and process grades.
- **Privacy (GDPR/CCPA)**: Moodle has built-in Privacy API tools. Ensure these are configured before you accept your first student.
- **Backups**: Set up automated Course Backups to an external S3 bucket (you cannot afford losing student grades).

**Quick setup**: Using **Tutor** you can avoid configuring PHP extensions and file permissions for hours. It's a Docker-based deployment tool originally for Open edX, but there're similar Docker-compose setups for Moodle that will spin up your DB, Redis (for caching), and Web Server in one command.

## Moodle in WSL 2

Install Docker Desktop in Windows and setup for WSL 2.



