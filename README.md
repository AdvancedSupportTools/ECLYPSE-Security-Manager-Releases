# ECLYPSE Security Manager

> ⚠️ **IMPORTANT: COMMUNITY TOOL - NOT AN OFFICIAL DISTECH CONTROLS PRODUCT**
>
> This application is a special project developed by the Distech Controls Advanced Support Team and is **NOT a sanctioned or official release** by Distech Controls. Please read the **[DISCLAIMER.txt](DISCLAIMER.txt)** before using this tool.

**Enterprise-grade certificate lifecycle management and network operations for ECLYPSE Building Automation Systems**

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)]()
[![PowerShell](https://img.shields.io/badge/PowerShell-7.0%2B-blue)]()
[![OpenSSL](https://img.shields.io/badge/OpenSSL-3.x-green)]()
[![Community Tool](https://img.shields.io/badge/status-community%20tool-orange)]()

---

## ⚠️ Important Notice

**THIS IS A COMMUNITY TOOL - READ BEFORE USE**

This application is:
- ✅ **Freely available** for use and redistribution
- ✅ **Built using** only publicly available RESTful API endpoints
- ✅ **Supported by Advanced Support** at their discretion, primarily for Distech SI's, Distributors, OEMs, and partners
- ❌ **NOT an official Distech Controls product**
- ❌ **NOT covered** by Distech Controls warranties or support agreements
- ❌ **NOT subject** to standard Distech Controls release procedures

**📋 [READ THE FULL DISCLAIMER](DISCLAIMER.txt)** - Contains important legal information about warranty, liability, and support.

**By using this tool, you acknowledge and accept the terms in the disclaimer.**

---

## 🔄 Semantic Versioning Adoption

**Version Numbering Change:** v6.17.399b → v1.0.1 → v1.0.7

We've transitioned from development versioning (6.x.x) to **semantic versioning** for clearer release communication:

- **MAJOR** (1.x.x): Breaking changes requiring user action
- **MINOR** (x.1.x): New features, backward compatible
- **PATCH** (x.x.1): Bug fixes and improvements

**This is NOT a downgrade** - v1.0.7 is **NEWER** than v6.17.399b and v1.0.1. The built-in update checker correctly detects these transitions.

**Upgrading from v6.17.x or v1.0.1?** Your profiles are fully compatible. Just replace the executable/AppImage - no migration needed.

---

## 🎯 What is This?

ECLYPSE Security Manager is a **complete PKI and network management solution** designed specifically for ECLYPSE controllers in Building Automation Systems. It streamlines certificate lifecycle management, automates routine tasks, and provides enterprise-level security features for BAS environments ranging from single-site installations to large distributed deployments.

**Built for:** System integrators, IT administrators, and support engineers managing ECLYPSE controllers

**Developed by:** Distech Controls Advanced Support Team (community project)

**Replaces:** Manual certificate generation, ad-hoc OpenSSL commands, spreadsheet-based controller tracking

---

<details>
<summary><b>🖼️ Click to view application screenshots</b></summary>

### Profile Selection
![Profile Selection](images/profile-selection.png)
*Secure, encrypted profiles with multi-user support*

### Main Dashboard
![Main Menu](images/main-menu.png)
*Intuitive menu-driven interface for all operations*

### Network Discovery
![mDNS Discovery](images/mdns-discovery.png)
*Automatic controller discovery using mDNS/Avahi*

### Backup Management
![Backup Dashboard](images/backup-dashboard.png)
*Visual dashboard with bar charts for backup status*

### Certificate Inventory
![Certificate Inventory](images/certificate-inventory.png)
*Comprehensive certificate tracking across all controllers*

</details>

---

## ✨ Key Features

### 🌐 **Network Interface Management (NEW in v1.0.7)**

- **View Interface Status:** Real-time IPv4/IPv6 configuration monitoring
  - Bridge, primary, secondary interface support
  - Operational status: Routable, Carrier, NoCarrier, Off
  - IP address display with color-coded status indicators
  - Bulk queries across all controllers

- **Configure IPv4/IPv6 Settings:** Batch operations with enterprise reliability
  - 6 action options: Enable/disable IPv4, IPv6, or both
  - Multi-interface selection (comma-separated: "1,2" for primary+secondary)
  - Typed confirmation for safety ("CONFIRM" required)
  - Automatic verification scan after changes

- **3-Pass Retry System:** Intelligent failure recovery
  - Pass 1: Attempt all controllers
  - Pass 2: Retry failures from Pass 1
  - Pass 3: Final retry for persistent failures
  - **Result:** 97-99% success rate vs 85-90% single-pass
  - Silent retries with final summary (✓/✗ per controller)
  - Real-time progress: `⚡ Pass 2 : 5/10 (50%) | controller-01 | ETA: 45s`

- **Adaptive Network Integration:** Dynamic operation tuning
  - Pre-operation network quality detection (5-sample latency test)
  - Delay adjustment based on conditions (Excellent/Good/Fair/Poor/Critical)
  - Automatic throttle increases on failures (reliability over speed)
  - Live metrics: Avg latency, packet loss %, quality badge

### 🔐 **Advanced Certificate Management**

- **Multi-CA Architecture:** Manage multiple Certificate Authorities simultaneously with intelligent selection
- **Custom Certificate Builder:** 8-step wizard with full control over extensions, SANs, and key usage
- **CSR Workflow:** Generate Certificate Signing Requests for external CA signing with automatic import matching
- **16 Export Formats:** PKCS#12, PEM, DER, JKS, PKCS#8, and specialized formats (EC-Net/Niagara bundles)
  - **Improved in v1.0.7:** Windows EXE export stability (all formats working)
- **Certificate Templates:** Save and reuse certificate configurations
- **Variable Expansion:** Batch generate certificates with patterns (`controller{+1}`, `device-{001}`)
- **Expiration Tracking:** Automated monitoring with configurable warning periods
- **3-Pass Deployment:** Matches interface management reliability (carried from v6.17.x)

### 🌐 **Intelligent Network Discovery**

- **Hybrid mDNS:** Avahi (Linux), Bonjour (Windows), and native .NET fallback
- **Smart Caching:** Skip validation for recently-scanned controllers (60-80% faster repeat scans)
- **TCP Pre-Flight:** Filter dead IPs before HTTPS validation (saves 4.5s per dead IP)
- **Parallel Scanning:** Configurable thread count (1-50 threads) with adaptive performance
- **IPv6 Optimization:** Automatic adapter management with hybrid restoration
- **Metadata Pre-Loading:** Batch API calls fetch backup/cert counts in parallel
- **Improved in v1.0.7:** Port number filtering (cleaner scan results)

### 💾 **Comprehensive Backup System**

- **Remote Backup Operations:**
  - Create, download, and delete backups via controller API
  - Granular selection: All/Latest/By-Age/By-Count/Specific
  - Overwrite behavior control (skip existing vs force re-download)
  - **Improved in v1.0.7:** 3-pass retry for backup operations

- **Local Backup Management:**
  - Profile-based organization (`Backups/{Profile}/{Controller}/`)
  - Optional AES-256 encryption with profile password
  - Date-based filtering and bulk operations
  - Automated retention policies

- **Backup Dashboard:** Real-time status with coverage metrics and bar chart visualization

### 👤 **Profile & Session Management**

- **Encrypted Profiles:**
  - AES-256-CBC with PBKDF2 key derivation (10,000 iterations)
  - Per-profile password protection (separate from session credentials)
  - Controller lists, CAs, jobs, and settings stored encrypted

- **Profile Export/Import:**
  - Portable encrypted packages with integrity validation
  - HMAC-SHA256 signature + SHA256 per-file checksums
  - Selective component inclusion (CAs, certificates, backups, job templates)
  - Cross-profile security (re-encryption with target password)
  - Comprehensive audit logging

- **Session Management:**
  - Configurable timeout with lock/logout actions
  - Operation protection (suspend timeout during backups/scans)
  - Warning countdown (2-minute alert before timeout)
  - Inactivity tracking with automatic reset

- **Profile Locking:**
  - Multi-instance protection with stale detection
  - Process ID tracking (crash recovery)
  - Automatic lock file cleanup
  - Override options for legitimate concurrent access

### ⚙️ **Background Job System**

- **Automated Execution:**
  - Timer-based job execution (checks every minute)
  - Sequential queue processing prevents conflicts
  - Smart catch-up (missed jobs execute on restart)

- **Job Types:**
  - Remote Backup (download with advanced filters)
  - Remote Backup Create (scheduled backup creation)
  - Remote Backup Cleanup (age-based remote deletion)
  - Local Cleanup (retention policy enforcement)
  - Certificate Renewal (planned)
  - Network Scan (planned)

- **Scheduling Options:**
  - Daily, Weekly, Monthly
  - Hourly intervals
  - Minute intervals (5-1440 min)
  - Manual/on-demand

- **Job Management:**
  - Real-time dashboard with countdown timers
  - Execution history with retention policies
  - Enable/disable toggles
  - Manual execution triggers

### 🗂️ **Controller Management**

- **Dashboard View:** Summary-first design for 100+ controller environments
- **Improved in v1.0.7:** Submenu structure with Network Interface Management
  - Option 1: Controller Dashboard
  - Option 2: Network Interface Management (NEW)
  - Clear navigation labels ("Return to Controller Management")
- **Per-Controller Credentials:** Override session credentials for specific controllers (encrypted)
- **Metadata Caching:** Operation-aware cache with configurable TTL (10-60 minutes)
- **Bulk Operations:** Filter-based actions (no backups, no CA, no certs, by age)
- **Validation Tools:** Parallel connectivity testing with reachability reports

### 📊 **Dual-Channel Modular Logging**

- **Two Independent Channels:**
  - File Output: Persistent log files (default: WARNING level)
  - Console Output: Real-time display (default: ERROR level)

- **Five Verbosity Levels:** ERROR < WARNING < INFO < DEBUG < TRACE
- **Per-Module Overrides:** Separate verbosity for Scanning, Certificates, Backups, General
- **Quick Presets:** Troubleshooting, Production, Development, Silent modes
- **Improved in v1.0.7:** Silent mode for retry operations (DEBUG level, file-only)

### 🔒 **Security Features**

- **Licensing System:**
  - Time-limited builds (30/60/90/180/365 day validity)
  - Password-protected licenses (optional)
  - CA-signed certificates with signature validation
  - Embedded license PFX in compiled binaries
  - Expiration enforcement with countdown warnings

- **Credential Management:**
  - 3-tier storage (session/profile/don't save)
  - Certificate passwords cached for batch operations
  - Controller credentials saved encrypted in profile
  - Per-controller credential overrides
  - **Improved in v1.0.7:** Per-operation credential prompts with reuse option

- **Encryption:**
  - Profile data: AES-256-CBC with PBKDF2
  - Backup files: Optional AES-256 encryption
  - Private keys: Always encrypted (AES-256 or PKCS#8)

### 🚀 **Performance Optimizations**

- **Parallel Operations:**
  - RunspacePool-based multi-threading (configurable 1-50 threads)
  - Batch API calls (75% faster than sequential)
  - TCP pre-flight filtering (85-90% faster IP scans)
  - Smart metadata caching (4-8x faster repeat scans)

- **Adaptive Network Management (MODULE-1415 - Enhanced in v1.0.7):**
  - Pre-operation network quality testing
  - Dynamic delay calculation based on latency and packet loss
  - Automatic throttle adjustment during operations
  - Live visual feedback with network metrics

- **3-Pass Retry System (Universal in v1.0.7):**
  - Certificate deployment (carried from v6.17.x)
  - Interface configuration (NEW)
  - Backup operations (NEW)
  - Silent console output (errors logged to file at DEBUG level)
  - Intelligent recovery (only retries failures)
  - ETA calculation per pass

- **Windows Performance Tuning:**
  - DefaultConnectionLimit=100 (unlocks true parallelism)
  - Expect100Continue=false (prevents EXE connection drops)
  - UseNagleAlgorithm=false (reduces latency)
  - **Fixed in v1.0.7:** Separate try-catch blocks (EXE-compatible pattern)

- **Memory Management:**
  - Secure string bypasses for large file operations
  - Direct binary encryption for backup files (no 64KB limits)
  - Runspace disposal prevents memory leaks

---

## 📥 Download & Installation

### **Latest Release: v1.0.7**

**⚠️ License Validity:** This build is valid until **April 6, 2026** (89 days from release)

Download the latest release from the [Releases](../../releases) page.

### **Windows (Compiled .exe)**

1. **Download** the latest release:
   ```
   ECY-Security-Manager-v1.0.7.exe
   ```

2. **Verify Download (Recommended):**
   ```powershell
   (Get-FileHash .\ECY-Security-Manager-v1.0.7.exe -Algorithm SHA256).Hash
   # Should match: 3150E743B8CAAD356F98FECCA849088FB0A46CDAE0CF6DCA95951AB9AA06F332
   ```

3. **First Run Setup:**
   - Double-click to launch
   - OpenSSL extracts to `%APPDATA%\EclypseManager\bin\` (one-time, 5-10 seconds)
   - Subsequent runs are instant (uses cached binaries)

4. **File Structure:**
   ```
   ECY-Security-Manager-v1.0.7.exe
   share/
   ├── app-core.dat (encrypted application code)
   └── openssl-binaries.dat (encrypted OpenSSL)

   [On first run, extracts to:]
   %APPDATA%\EclypseManager\bin\
   ├── openssl.exe (~3.5 MB)
   ├── libcrypto-3-x64.dll (~5.8 MB)
   ├── libssl-3-x64.dll (~731 KB)
   └── openssl.cnf
   ```

5. **Cleanup (Optional):**
   ```
   Settings → Diagnostics → (scroll down) → Remove OpenSSL Files
   ```

**Requirements:**
- Windows 10/11 (x64 or ARM64)
- Administrator rights **ONLY** needed for IPv6 optimization (optional)

---

### **Linux (Self-Contained .AppImage)**

1. **Download** the latest release:
   ```bash
   wget https://github.com/LesserOfTwoWeevils/releases/download/v1.0.7/ECY-Security-Manager-v1.0.7.AppImage
   ```

2. **Verify Download (Recommended):**
   ```bash
   sha256sum ECY-Security-Manager-v1.0.7.AppImage
   # Should match: 0A85E4C702415538BED865810D73D19AD5AA4F84369C026002D79195ED8F87A5

   # OR use the checksum file:
   sha256sum -c ECY-Security-Manager-v1.0.7.AppImage.sha256
   ```

3. **Make executable:**
   ```bash
   chmod +x ECY-Security-Manager-v1.0.7.AppImage
   ```

4. **Run:**
   ```bash
   ./ECY-Security-Manager-v1.0.7.AppImage
   ```

5. **Optional: Install Avahi for mDNS:**
   ```bash
   # Fedora/RHEL/Rocky/CentOS:
   sudo dnf install avahi avahi-tools

   # Ubuntu/Debian:
   sudo apt install avahi-daemon avahi-utils
   ```

6. **Data Storage:**
   ```
   ~/.local/share/ECYSecurityManager/
   ├── Profiles/ (encrypted profile data)
   ├── CA/ (certificate authorities)
   ├── Certificates/ (generated certificates)
   ├── Backups/ (downloaded backups)
   ├── Logs/ (session logs)
   └── Config/ (application settings)
   ```

**Requirements:**
- Most Linux distributions (Ubuntu 20.04+, Fedora 35+, etc.)
- No additional dependencies
- First run: ~5-10 seconds (FUSE mount + extraction)
- Subsequent runs: Instant

---

## 🎮 Quick Start Guide

### **1. First Launch: Profile Setup**

**On first launch, you'll see a profile selection screen:**

```
Create New Profile:
  • Encrypted with your password
  • Stores your settings, CAs, controllers
  • Survives application restarts

OR

Use Temporary Profile:
  • No password required
  • Changes not saved
  • Good for testing
```

**Best Practice:** Create a named profile unless you're just exploring.

---

### **2. Scan Your Network**

**Option 1: mDNS Discovery (Automatic)**

```
Main Menu → [1] Scan Network → [2] mDNS Discovery
  ✓ Auto-discovers ECLYPSE controllers on local subnet
  ✓ Works with Avahi (Linux) or Bonjour (Windows)
  ✓ Fast: Typically finds controllers in 20-30 seconds
```

**Option 2: IP Range Scan**

```
Main Menu → [1] Scan Network → [1] IP Range
  → Enter: 10.110.210.50-100
  ✓ Validates each IP for ECLYPSE API
  ✓ Parallel scanning (10-20 threads recommended)
  ✓ TCP pre-flight filtering (skips dead IPs)
```

**Result:** Authenticated controllers added to session with metadata pre-loaded

---

### **3. Generate Certificate Authority**

```
Main Menu → [4] Generate/Manage CA
  → Follows 8-step wizard:
     1. CA Name & Common Name
     2. Configuration Mode (Defaults vs Custom)
     3. CA Type & Constraints (Root vs Intermediate, Path Length)
     4. Key Parameters (4096-bit recommended for CAs)
     5. Subject Fields
     6. SANs (optional for CAs)
     7. Preview
     8. Generation

  ✓ Password-protected private key (AES-256)
  ✓ Metadata saved for tracking
  ✓ Template system for reuse
```

**Best Practice:** Use 4096-bit keys for CAs, 10-20 year validity

---

### **4. Generate Controller Certificates**

**Quick Generate (Fast):**
```
Main Menu → [5] Generate Certificates → [1] Quick Generate
  → Uses config defaults
  → Select controllers
  → Enter password once
  → Batch generates all certificates
  ✓ 2048-bit RSA, 1-year validity, BACnet SC extensions
```

**Custom Builder (Full Control):**
```
Main Menu → [5] Generate Certificates → [2] Custom Builder
  → 8-step workflow:
     1. Mode (Defaults vs Customize)
     2. Signing (Local CA vs External CSR)
     3. Targets (Single/List/Batch/Template)
     4. Subject Fields
     5. SANs (DNS, IP, Email)
     6. Extended Key Usage (9 presets)
     7. Final Preview
     8. Generation

  ✓ Variable expansion: {hostname}, {+1}, {001}
  ✓ Batch generation with templates
  ✓ Save as template for reuse
```

---

### **5. Deploy Certificates**

```
Main Menu → [6] Deploy Certificates
  → Select controllers (ALL or specific)
  → Choose stores:
     • user-trusted (CA certificates)
     • user-keychain (server certificates)
     • Both
  → Auto-detects format compatibility:
     • PS7: PKCS#12 (.pfx) - binary upload
     • PS5.1/EXE: Combined PEM - text upload
  → 3-pass retry with adaptive throttling (NEW in v1.0.7)
  ✓ Smart CA detection (deploys matching CA automatically)
  ✓ Per-controller credential support
  ✓ Silent retries with final summary
  ✓ 97-99% success rate
```

---

### **6. Manage Network Interfaces (NEW in v1.0.7)**

**View Interface Status:**
```
Main Menu → [2] Controller Management → [2] Network Interface Management
  → [1] View Interface Status
  → Enter credentials (or reuse session credentials)
  → Queries all controllers
  ✓ Shows: bridge, primary, secondary interfaces
  ✓ Status: Routable, Carrier, NoCarrier, Off
  ✓ IPv4/IPv6 enabled states with IP addresses
  ✓ Color-coded indicators
```

**Configure IPv4/IPv6:**
```
Main Menu → [2] Controller Management → [2] Network Interface Management
  → [2] Configure IPv4/IPv6 Settings
  → Enter credentials
  → Select controllers (ALL or specific)
  → Select interfaces (1,2 for primary+secondary or Enter for bridge)
  → Choose action:
     1. Enable IPv4
     2. Disable IPv4
     3. Enable IPv6
     4. Disable IPv6
     5. Enable both
     6. Disable both
  → Type "CONFIRM" to proceed
  → 3-pass retry with adaptive throttling
  → Automatic verification scan (5s delay)
  ✓ Real-time progress with ETA
  ✓ Silent retries during passes
  ✓ Final summary shows all ✓/✗
```

---

### **7. Schedule Automated Backups**

```
Main Menu → [14] Manage Jobs → [C] Create Job
  → Job Type: Remote Backup - Download
  → Schedule: Daily at 03:00
  → Targets: All Controllers
  → Options:
     • Backup Selection: Latest per controller
     • Encryption: Yes (profile password)
     • Overwrite: Skip existing
  ✓ Runs while application is open (15-second check interval)
  ✓ Executes even when session is locked
  ✓ History tracking with retention policies
```

---

## 🏗️ Architecture Overview

### **Security Architecture**

```
┌─────────────────────────────────────────────────────────────┐
│ Profile Layer (AES-256 + PBKDF2)                           │
│  • User password unlocks profile                            │
│  • Contains: Config, Controllers, CAs, Credentials, Jobs    │
│  • Separate password from certificate passwords             │
└─────────────────────────────────────────────────────────────┘
           ▼
┌─────────────────────────────────────────────────────────────┐
│ Credential Layer (3-Tier Caching)                          │
│  • Session: Memory only (cleared on exit)                   │
│  • Profile: Encrypted with profile password                 │
│  • Per-Controller: Override for specific controllers        │
│  • Per-Operation: Prompt with reuse option (NEW v1.0.7)    │
└─────────────────────────────────────────────────────────────┘
           ▼
┌─────────────────────────────────────────────────────────────┐
│ Certificate Layer (PKI Operations)                         │
│  • CA Private Keys: AES-256 encrypted on disk               │
│  • Controller Certs: PKCS#12 with user-defined password     │
│  • CSRs: Private keys encrypted, auto-delete on import      │
└─────────────────────────────────────────────────────────────┘
           ▼
┌─────────────────────────────────────────────────────────────┐
│ Transport Layer (HTTPS API)                                │
│  • Self-signed cert bypass (global ServicePointManager)     │
│  • Basic Auth over TLS 1.2/1.3                              │
│  • 3-method fallback (Script/EXE/WebRequest compatibility)  │
│  • Separate try-catch blocks for EXE stability (v1.0.7)    │
└─────────────────────────────────────────────────────────────┘
```

### **3-Pass Retry Flow (NEW - Universal in v1.0.7)**

```
Operation Start (Certificate Deploy / Interface Config / Backup)
  ↓
Network Quality Detection (MODULE-1415)
  → 5-sample latency test
  → Calculate: Excellent/Good/Fair/Poor/Critical
  → Adaptive delay: +0% (Good) to +100% (Critical)
  ↓
Initialize Throttle
  → Base delay from settings
  → Apply network multiplier
  ↓
┌─────────────────────────────────────────────────────────────┐
│ PASS 1: Attempt All Controllers                            │
│  • Silent mode (errors logged at DEBUG level, not console)  │
│  • Progress: ⚡ Pass 1 : 5/12 (42%) | controller-01 | ETA:45s │
│  • Result: 10 success, 2 failures                           │
│  • Success Rate: 83% (typical for Pass 1)                   │
└─────────────────────────────────────────────────────────────┘
  ↓
┌─────────────────────────────────────────────────────────────┐
│ PASS 2: Retry Failures Only (2 controllers)                │
│  • Silent mode (DEBUG level logging)                        │
│  • Progress: ⚡ Pass 2 : 1/2 (50%) | controller-07 | ETA: 12s │
│  • Result: 1 success, 1 failure                             │
│  • Cumulative: 11/12 success (92%)                          │
└─────────────────────────────────────────────────────────────┘
  ↓
┌─────────────────────────────────────────────────────────────┐
│ PASS 3: Final Retry (1 controller)                         │
│  • Silent mode (DEBUG level logging)                        │
│  • Progress: ⚡ Pass 3 : 1/1 (100%) | controller-07 | ETA: 6s  │
│  • Result: 1 success, 0 failures                            │
│  • Final: 12/12 success (100%)                              │
└─────────────────────────────────────────────────────────────┘
  ↓
Final Summary (Console Display)
  ✓ controller-01
  ✓ controller-02
  ...
  ✓ controller-12

Overall Success: 12/12 (100%)
```

---

## 🚢 Deployment Scenarios

### **Single-Site Installation (1-20 Controllers)**

```yaml
Profile Setup:
  • Name: "Site-Alpha-Production"
  • CA: Single root CA (4096-bit, 10-year)
  • Scan: mDNS discovery (automatic)
  • Certificate Generation: Quick mode (uses defaults)
  • Backup: Manual (before deployments)
  • Network Management: Available for IPv6 migrations (NEW)

Workflow:
  1. Scan network once
  2. Generate CA once
  3. Generate certificates (batch, 5 minutes)
  4. Deploy with 3-pass retry (3 minutes, 99% success)
  5. Verify via inventory
  6. Configure interfaces if needed (IPv4/IPv6 settings)

Time to Production: ~15 minutes
```

### **Multi-Site Enterprise (100+ Controllers)**

```yaml
Profile Setup:
  • Name: "Enterprise-Central-Office"
  • CAs: Multiple (one per site or function)
  • Scan: Import CSV lists (pre-populated)
  • Certificate Generation: Custom builder with templates
  • Jobs: Automated nightly backups
  • Network Management: Bulk IPv6 enablement across sites (NEW)

Workflow:
  1. Import controller lists (CSV per site)
  2. Generate CAs (one per site, save as templates)
  3. Generate certificates (template-based, 30-minute batch)
  4. Deploy in phases (site-by-site, 3-pass retry)
  5. Configure network interfaces (bulk IPv6 rollout)
  6. Schedule backup jobs (daily downloads)
  7. Monitor via dashboards

Features Used:
  • Per-controller credentials (different admin passwords per site)
  • Job system (nightly backups to central location)
  • Metadata caching (instant dashboard refresh)
  • Profile export (backup configuration to other machines)
  • 3-pass retry (97-99% success across enterprise scale)
  • Adaptive throttling (network-aware operations)

Time to Production: ~2-4 hours (initial setup), ~15 min/site (ongoing)
```

### **Service Provider / MSP (Multi-Customer)**

```yaml
Profile Structure:
  • One profile per customer
  • Isolated CAs, credentials, and settings
  • Profile export for team sharing

Example Profiles:
  • "Customer-A-Main-Office"
  • "Customer-B-Production"
  • "Customer-C-Test-Environment"

Workflow:
  1. Create profile per customer
  2. Import customer's controller list
  3. Generate customer-specific CA
  4. Deploy certificates (3-pass reliability)
  5. Configure interfaces per customer requirements (NEW)
  6. Export profile (encrypted) for team backup
  7. Switch profiles as needed (no restart)

Profile Security:
  • Each profile has separate password
  • Per-profile credential isolation
  • Export packages encrypted with separate password
  • Import re-encrypts with target profile password

NEW in v1.0.7:
  • Bulk interface management for IPv6 rollouts
  • 3-pass operations across all critical functions
  • Network quality detection before operations
```

### **IPv6 Migration Scenario (NEW in v1.0.7)**

```yaml
Objective: Enable IPv6 across 50-controller facility

Workflow:
  1. Controller Management → Network Interface Management
  2. View Interface Status (baseline - all IPv6 disabled)
  3. Select All Controllers
  4. Select bridge interface
  5. Choose Action: Enable IPv6
  6. Type "CONFIRM"
  7. 3-pass execution:
     • Pass 1: 45/50 success (90%)
     • Pass 2: 4/5 success (80% of failures recovered)
     • Pass 3: 1/1 success (100% final)
     • Overall: 50/50 (100% success)
  8. Automatic verification scan confirms changes
  9. Document results in change log

Time: ~15 minutes for 50 controllers (3-pass with delays)
Success Rate: 97-99% typical with 3-pass retry
```

---

## 🔐 Security Best Practices

### **Profile Management**

```powershell
DO:
  ✓ Use strong profile passwords (8+ characters)
  ✓ Export profiles periodically (Settings → Profile Management → Export)
  ✓ Store exports in secure location (encrypted backup)
  ✓ Use named profiles for production (not temporary)

DON'T:
  ✗ Share profile passwords via unencrypted channels
  ✗ Use same password for profile and certificates
  ✗ Disable session timeout in shared environments
  ✗ Skip profile backups before major changes
```

### **Certificate Passwords**

```powershell
ENCRYPTION OPTIONS (Prompted during generation):
  1. Session Only - Cleared on exit (good for one-time use)
  2. Profile Storage - Reused next session (good for automation)
  0. Don't Save - Re-enter every time (maximum security)

RECOMMENDATION:
  • Production CAs: Don't save (manual entry prevents unauthorized use)
  • Controller certs: Save to profile (enables batch deployments)
```

### **Controller Credentials**

```powershell
DEFAULT BEHAVIOR:
  • Single username/password for all controllers
  • Saved encrypted in profile (opt-in)
  • Reused across sessions
  • Per-operation prompt with reuse option (NEW in v1.0.7)

OVERRIDE FOR SENSITIVE CONTROLLERS:
  Controller Manager → Edit Controller → Set Custom Credentials
  • CEO's controller: admin/special-password
  • Server room controller: admin/different-password
  • Default controllers: session credential
```

### **Network Interface Changes**

```powershell
SAFETY MECHANISMS (v1.0.7):
  • Typed confirmation required ("CONFIRM")
  • Detailed preview before execution
  • Credential prompt per operation
  • Automatic verification scan after changes
  • 3-pass retry prevents partial failures

BEST PRACTICES:
  • Test on single controller first
  • Document baseline configuration
  • Schedule during maintenance windows
  • Verify connectivity after changes
  • Use verification scan to confirm
```

### **Backup Encryption**

```powershell
WHEN DOWNLOADING BACKUPS:
  → Prompt: "Encrypt backups after download?"
     • [N] No - Standard ZIP (fast, extractable anywhere)
     • [Y] Yes - AES-256 encrypted (requires profile to decrypt)

USE ENCRYPTION IF:
  • Storing backups on shared drives
  • Emailing backups to remote teams
  • Compliance requires encrypted storage

USE PLAIN ZIP IF:
  • Backups stay on local machine
  • Need to extract on systems without this tool
```

---

## 📚 Advanced Features

### **Opportunistic Cache Updates**

Operations automatically update controller metadata **without user action**:

```
Backup Created → BackupCount++
CA Deployed → CADeployStatus = true
Cert Deployed → CertDeployStatus = true
Delete Backup → BackupCount--
Interface Changed → InterfaceConfigTimestamp updated (NEW v1.0.7)
```

**Result:** Dashboard always shows current state without manual refresh

### **Adaptive Network Management (MODULE-1415)**

Dynamic operation tuning based on real-time conditions:

```
Pre-Operation Detection:
  → 5-sample latency test to selected controllers
  → Calculate average latency and packet loss
  → Quality Rating:
     • Excellent: <10ms, 0% loss
     • Good: 10-50ms, 0-2% loss
     • Fair: 50-100ms, 2-5% loss
     • Poor: 100-200ms, 5-10% loss
     • Critical: >200ms or >10% loss

Delay Adjustment:
  → Base Delay: User configured (1-60s, default 5s)
  → Multiplier:
     • Excellent/Good: 1.0x (no change)
     • Fair: 1.25x (+25%)
     • Poor: 1.5x (+50%)
     • Critical: 2.0x (+100%)

During Operation:
  → Throttle increases on failures (max 3x base)
  → Throttle maintains/reduces on success streaks
  → Live metrics: "Network Quality: Good (Avg: 6ms, Loss: 0%)"

Result: Operations adapt to network conditions automatically
```

### **Variable Expansion in Batch Operations**

Generate 100 certificates with patterns:

```powershell
Pattern: floor-{001}-controller{+1}

Expands to:
  floor-001-controller1
  floor-002-controller2
  floor-003-controller3
  ...
  floor-100-controller100

Supports:
  {hostname}  - From controller list
  {ip}        - Dots become dashes
  {alias}     - Custom name from list
  {+N}        - Increment by N
  {NNN}       - Zero-padded sequence
```

### **Profile Export/Import Use Cases**

**Scenario 1: Team Sharing**
```
Engineer A: Scans network, generates CAs
Engineer A: Settings → Profile Management → Export Profile
           → Includes: Config, Controllers, CAs, Credentials
           → Creates: encrypted .zip package

Engineer B: Import package, enters export password
           → Result: Instant access to same environment
```

**Scenario 2: Disaster Recovery**
```
Before Update: Export profile (backup)
After Update: Update causes issues?
             → Import old profile
             → Use archived old binary
             → Back to working state
```

**Scenario 3: Machine Migration**
```
Old Laptop: Export profile
New Laptop: Install app, import profile
           → All settings, controllers, and CAs migrated
           → No reconfiguration needed
```

---

## 🔧 Configuration & Tuning

### **Performance Settings**

```
Settings → ECLYPSE API Settings:
  • Max Concurrent Threads: 10-50 (default: 10)
    → Higher = faster, more network load
    → Lower = slower, more reliable

  • Timeout: 5-60 seconds (default: 30)
    → Fast LAN: 5-10s
    → Slow/Remote: 30-60s

  • Operation Delay: 0-60 seconds (default: 5)
    → Wait time after POST/DELETE operations
    → Prevents stale reads from controller web UI
    → Adaptive throttling adjusts automatically (MODULE-1415)

  • TCP Pre-Flight: ON/OFF (default: ON)
    → Filters dead IPs before HTTPS validation
    → Saves 4.5 seconds per dead IP
```

### **Logging Configuration**

```
Settings → Configure Logging:
  FILE CHANNEL (Persistent):
    • Production: WARNING (captures issues)
    • Development: INFO (operations visibility)
    • Troubleshooting: DEBUG (technical details)
    • Deep Debugging: TRACE (every step)

  CONSOLE CHANNEL (Real-time):
    • Production: ERROR (silent until problems)
    • Development: WARNING (occasional cautions)
    • Troubleshooting: INFO (progress messages)

  PER-MODULE OVERRIDES:
    • Scanning: DEBUG (diagnose network issues)
    • Certificates: WARNING (keep others quiet)
    • Backups: INFO (visibility)
    • General: ERROR (default)

  NEW in v1.0.7:
    • Silent mode for retry operations
    • Errors during retries: DEBUG level (file only)
    • Final results: INFO/ERROR level (console + file)
```

### **mDNS Discovery Settings**

```
Settings → Configure mDNS Discovery:
  • Initial Stabilization: 5-15s (default: 10s)
    → Wait after discovery before first auth attempt

  • Retry Stabilization: 5-15s (default: 10s)
    → Wait before retry after failed auth

  • Max Retries: 0-3 (default: 1)
    → Silent retry attempts for timing failures

  • Max Threads: 1-20 (default: 3)
    → Parallel auth threads
    → Lower = more reliable (SSL race conditions)
    → Higher = faster (but may lose some controllers)

  • Cache Recognition: ON/OFF (default: ON)
    → Skip validation for recently-scanned controllers
    → 60-80% faster repeat scans

  • Discovery Mode: 1x Fast vs 2x Thorough (default: 1x)
    → Fast: Single browse+resolve pass (~25s)
    → Thorough: Double passes with delays (~50s)
```

---

## 🐛 Troubleshooting

### **Common Issues**

**Issue:** "OpenSSL not found"
```
SYMPTOMS:
  • Options 3-5 locked in main menu
  • "LIMITED MODE" message on startup

FIX:
  Windows: Settings → Diagnostics → Check OpenSSL Status
           → Shows winget command for installation

  Linux:   sudo dnf install openssl openssl-devel  (Fedora/RHEL)
           sudo apt install openssl libssl-dev      (Ubuntu/Debian)
```

**Issue:** "Authentication failures during mDNS"
```
SYMPTOMS:
  • 10/13 controllers authenticate
  • Others timeout or fail

CAUSE: IPv6 causes SSL timing conflicts

FIX (Option 1 - Automatic):
  Scan → mDNS Enhanced → Disable IPv6 Temporarily
  → Auto-restores after scan

FIX (Option 2 - Manual):
  Control Panel → Network Connections
  → Right-click adapter → Properties
  → UNCHECK "Internet Protocol Version 6 (TCP/IPv6)"
```

**Issue:** "Slow scans (60+ seconds for 13 controllers)"
```
SYMPTOMS:
  • Each controller takes 5+ seconds
  • Progress bar crawls

CAUSES:
  1. Low thread count (MaxConcurrentThreads = 1)
  2. High timeout (Timeout = 60s)
  3. Cache disabled (UseCachedControllers = false)

FIX:
  Settings → ECLYPSE API Settings:
    • Max Concurrent Threads: 10-20 (increase)
    • Timeout: 5-10 seconds (decrease for fast LANs)

  Settings → Configure mDNS Discovery:
    • Cache Recognition: ON (enable)
```

**Issue:** "Interface configuration fails instantly (1 second)"**
```
SYMPTOMS:
  • 12 controllers, all fail in ~1 second
  • No network activity observed

CAUSE: Nested try-catch breaks in Windows EXE (fixed in v1.0.7)

FIX:
  • Update to v1.0.7 or later
  • Uses separate try-catch blocks (EXE-compatible)
```

**Issue:** "Profile password incorrect"
```
SYMPTOMS:
  • Profile selection → Enter password → Fails 3 times
  • 10-second delay, returns to menu

FIX (If you forgot password):
  ✗ Cannot recover encrypted profile (by design)
  ✓ Create new profile
  ✓ OR: Use temporary profile
  ✓ OR: Restore from profile export (if you have backup)

FIX (If password is correct but fails):
  → Check for leading/trailing spaces
  → Password is case-sensitive
  → Verify keyboard layout (QWERTY vs AZERTY)
```

**Issue:** "3-pass retry shows errors during operation" (v1.0.6 and earlier)**
```
SYMPTOMS:
  • Red error messages appear during Pass 1, Pass 2
  • Console cluttered with failure notices

FIXED in v1.0.7:
  • Silent mode enabled for retry operations
  • Errors logged to file at DEBUG level
  • Console only shows final summary (✓/✗ per controller)
```

**Issue:** "Downloaded file is 0 bytes" or "Download fails silently"
```
SYMPTOMS:
  • Update download shows 0% progress
  • File created but empty
  • No error message

CAUSE: GitHub redirects to Azure blob storage, WebClient doesn't follow

FIX:
  • Update will retry with Invoke-WebRequest automatically
  • If both fail, try curl (Linux) or BITS (Windows)
  • Manual download: Visit GitHub releases page
```

### **Performance Optimization**

**For 300+ Controller Deployments:**

```yaml
Config Tuning:
  MaxConcurrentThreads: 30-50 (aggressive)
  Timeout: 5-10 seconds (fast LAN assumed)
  OperationDelay: 2-3 seconds (balanced)
  UseCachedControllers: true (essential)
  UseTCPPreFlight: true (massive savings)
  AdaptiveThrottling: Enabled (MODULE-1415, automatic)

Expected Performance:
  • Initial scan: ~90 seconds (parallel validation + metadata)
  • Repeat scan: ~15 seconds (cache hits + new controllers)
  • Certificate generation: ~10-15 minutes (batch with 2s delay)
  • Certificate deployment: ~8-12 minutes (3-pass with adaptive delays)
  • Interface configuration: ~5-8 minutes (3-pass with adaptive delays)
  • Backup download (latest per controller): ~45-60 minutes
```

**For Slow/Remote Networks:**

```yaml
Config Tuning:
  MaxConcurrentThreads: 5-10 (conservative)
  Timeout: 30-60 seconds (patient)
  OperationDelay: 5-10 seconds (safe)
  MaxRetries: 3 (thorough)
  AdaptiveThrottling: Enabled (automatically increases delays)

Expected Performance:
  • Operations slower but more reliable
  • Fewer authentication failures
  • Better for WAN/VPN connections
  • 3-pass retry compensates for network issues
```

---

## 🔄 Update System

### **Check for Updates**

```
Settings → [15] Check for Updates
  → Queries GitHub Releases API
  → Compares semantic versions
  → Shows release notes preview
  → Offers one-click download
```

### **Download Process**

```
1. User: [D] Download Update
2. System: Profile backup check
   → If >24h since last export: Prompt for backup
   → If recent export: Skip prompt (non-nagging)
3. System: Download binary to ~/Downloads
   → Progress bar with speed and ETA
   → 3-method fallback (Invoke-WebRequest, BITS, curl)
4. System: Show installation instructions
   → Windows: Move new .exe to install folder
   → Linux: Replace .AppImage file
```

---

## 🌍 Localization

**Supported Languages:**
- English (en) - Default
- Français (fr) - Partial
- Deutsch (de) - Partial
- Español (es) - Partial
- Polski (pl) - Partial

**Coverage:** ~120 translation keys (menus, prompts, status messages)

**Change Language:**
```
Settings → Profile Management → Change Language
  OR
Create new profile → Select language during setup
```

---

## 📜 Legal & Licensing

### **Software License**
This software is released under the **GNU General Public License v3.0 (GPL-3.0)**.
See [LICENSE.txt](LICENSE.txt) for full terms.

### **Important Notices**
- **[DISCLAIMER.txt](DISCLAIMER.txt)** - Legal disclaimer, warranty information, and project status
- **[THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt)** - Third-party component licenses (OpenSSL, PowerShell, etc.)

### **No Telemetry**
This application:
- ✅ Collects **zero** usage data
- ✅ Makes **no** outbound connections (except manual update checks to GitHub public API)
- ✅ Stores all data locally or sends directly to your controllers
- ✅ Contains **no** tracking, analytics, or telemetry of any kind

---

## 🤝 Contributing & Support

This is a **releases-only** repository. Source code is maintained in a separate private repository.

### **Report Issues**
Use the [Issues](../../issues) tab for:
- 🐛 Bug reports
- 💡 Feature requests
- 📖 Documentation improvements

### **Community Discussions**
Use the [Discussions](../../discussions) tab for:
- ❓ General questions
- 💬 Community support
- 🎓 Tips and best practices

### **Support Availability**
Support is provided by the Distech Controls Advanced Support Team on a **discretionary basis**, primarily for:
- Distech Controls System Integrators (SI's)
- Authorized Distributors
- OEM Partners
- Other Distech Controls business partners

**Please note:** This is not covered by standard Distech Controls support agreements. Response times may vary, and complex issues may not be addressed.

### **Translations**
Contact the repository maintainer if you'd like to contribute language translations.

---

## 📞 Contact

**Development Team:** Distech Controls Advanced Support Team
**Project Lead:** Robert Lastinger
**Purpose:** Community tool for PKI and network management in BAS environments

**For Assistance:**
- 📖 Check this [README](../../)
- 🐛 Search [Issues](../../issues)
- 💬 Ask in [Discussions](../../discussions)
- 📋 Read the [DISCLAIMER](DISCLAIMER.txt)

**For Official Distech Controls Support:**
Please contact Distech Controls through official support channels for product-related inquiries.

---

## 🏆 Acknowledgments

This tool leverages the following open-source projects:

- **[OpenSSL Project](https://www.openssl.org/)** - Certificate generation and cryptographic operations
- **[PowerShell Team](https://github.com/PowerShell/PowerShell)** - Cross-platform runtime environment
- **[PS2EXE Community](https://github.com/MScholtes/PS2EXE)** - Windows executable compilation

See [THIRD-PARTY-NOTICES.txt](THIRD-PARTY-NOTICES.txt) for complete licensing information.

---

## 📊 Project Information

**Current Version:** v1.0.7
**Versioning Scheme:** Semantic Versioning (MAJOR.MINOR.PATCH)
**Release Date:** January 7, 2026
**License Validity:** 90 days (expires April 6, 2026)
**License:** GPL-3.0
**Status:** Community Tool - Stable Release
**Minimum PowerShell:** 7.0+
**Supported Platforms:** Windows 10/11, Linux (most distributions)

---

**Built with ⚡ by Distech Controls Advanced Support Team**

*This is a community project. Please read [DISCLAIMER.txt](DISCLAIMER.txt) before use.*

---