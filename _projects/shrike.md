---
layout: page
title: "Shrike Security Auditing Tool"
subtitle: "A modular security auditing tool that consolidates findings from established security scanners into a unified reporting workflow."
date: 2026-11-16
thumbnail: "/assets/images/shrike_thumbnail.png"
github_link: "https://gitlab.com/tristanswanson98/shrike"
---

### The Challenge

As a developer working on personal software projects, I wanted a practical way to regularly assess the security of my own repositories. Existing security tools offer powerful individual capabilities, but using several independently can mean managing different workflows, interpreting inconsistent outputs, and manually keeping track of findings.

I started developing Shrike to address this problem: a tool I could use to audit my own projects while building something that could also be useful to other developers and security practitioners.

Modern software projects rely on multiple security analysis tools to identify vulnerabilities, exposed credentials, and insecure configurations. However, these tools operate independently and produce results in different formats, making it difficult to consolidate findings, track security issues over time, and maintain a consistent view of a repository's security posture.

Shrike aims to address this fragmentation by providing a unified security auditing workflow. Rather than attempting to independently implement every type of vulnerability detection, the project integrates established security scanners and normalizes their output into a common data model.

The initial focus is on auditing GitHub and local Git repositories, with an architecture designed to accommodate additional repository providers and scanning tools in the future.

### Process

I am developing Shrike as a modular Python application, with an emphasis on maintainability, extensibility, and reliable handling of security findings.

* **Architecture & Data Modeling:** I designed a normalized finding model using Pydantic to establish a consistent representation of security issues across different scanning tools. This provides a common foundation for storing, comparing, filtering, and reporting findings regardless of their original source.

* **Security Tool Integration:** Rather than reinventing existing security analysis capabilities, Shrike is designed to orchestrate established tools:
    * **Gitleaks:** Detects exposed credentials and secrets in repositories and Git history.
    * **Semgrep:** Identifies potentially insecure programming patterns through static application security testing (SAST).
    * **Checkov:** Detects security misconfigurations in infrastructure-as-code files.

* **Finding Normalization:** I am developing scanner-specific parsers to translate disparate tool outputs into the common finding model. This includes normalizing metadata, severity classifications, affected file locations, and remediation information. Finding fingerprinting will provide a consistent mechanism for deduplication and historical comparison.

* **Security & Reliability:** A major design consideration is the safe handling of untrusted repositories. Shrike is intended to analyze source code without executing repository-provided application code or scripts. Additional safeguards are planned for temporary repository storage, scanner failures, sensitive credential handling, and secret redaction.

* **Tech Stack:** Python, Pydantic, Gitleaks, Semgrep, Checkov, SQLite, Pytest, Ruff, GitLab CI/CD

### The Result

Shrike is currently in early development, with the initial Python package structure and normalized security finding model implemented. Initial work has also begun on scanner output normalization, establishing the foundation for integrating external security analysis tools.

The planned application will provide a repeatable workflow for acquiring repositories, running security scans, consolidating findings, and generating actionable reports. SQLite persistence will support historical comparisons, allowing users to distinguish newly discovered issues from previously identified findings and track changes between scans.

The project is being developed incrementally, prioritizing a reliable scanning and normalization pipeline before expanding into repository discovery, historical tracking, and reporting.

### Current Development Status

- [x] Python package structure
- [x] Normalized finding model using Pydantic
- [x] Initial model validation tests
- [x] Initial Gitleaks output normalization
- [ ] Common scanner interface and additional integrations
- [ ] Repository acquisition
- [ ] SQLite persistence and historical tracking
- [ ] Consolidated reporting and export

### License

* **Source Code:** This project is licensed under the [MIT License](https://opensource.org/license/mit/).
* **Project Thumbnail:** "[Shrike Loggerhead JG.jpg](https://commons.wikimedia.org/wiki/File:Shrike_Loggerhead_JG.jpg)" by [JeffreyGammon](https://commons.wikimedia.org/wiki/User:JeffreyGammon), used under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license. Cropped and modified for use in this portfolio. No endorsement by the original creator is implied.