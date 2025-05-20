# Enterprise Windows System Refresh

![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)
![PowerShell Version](https://img.shields.io/badge/PowerShell-5.1%2B-blue)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-brightgreen)
![Maintenance](https://img.shields.io/badge/maintained-yes-green.svg)

A comprehensive enterprise-grade PowerShell script that refreshes Windows systems to a near-fresh state without requiring reinstallation. This tool significantly reduces IT overhead by automating what would otherwise be hours of manual system maintenance, allowing organizations to quickly restore optimal performance to problematic workstations without disrupting user workflows or data.

## Features

- **Complete System Refresh**: Restore Windows performance without reinstallation
- **System Integrity Repair**: Fix corrupted system files and Windows components
- **Advanced Cleanup**: Remove temporary files, caches, and system debris
- **Performance Optimization**: Enhance system responsiveness and boot times
- **Registry Cleanup**: Fix and optimize the Windows registry
- **Store & App Repair**: Reset Microsoft Store and fix problematic Windows apps
- **Network Stack Reset**: Completely rebuild network configuration
- **Service Optimization**: Configure services for optimal performance
- **Enterprise-Ready**: Designed for professional IT environments
- **Detailed Logging**: Comprehensive logging of all operations

## Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer
- Administrator privileges
- 2GB+ free disk space

## Quick Start

1. Download the script
2. Open PowerShell as Administrator
3. Set execution policy to allow the script to run:
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
   ```
4. Navigate to the script location
5. Run the script:
   ```powershell
   .\WindowsRefresh.ps1
   ```

## What Does It Do?

This script performs a deep refresh of Windows by:

1. Creating a system restore point
2. Resetting Windows Update components
3. Repairing system file integrity with SFC and DISM
4. Completely resetting the network stack
5. Performing advanced system cleanup
6. Optimizing and cleaning the registry
7. Resetting Microsoft Store and app packages
8. Optimizing Windows services
9. Enhancing system performance
10. Optionally removing bloatware

The script includes extensive error handling, logging, and retry mechanisms to ensure a smooth refresh process.

## Business Value

This tool provides significant value to IT departments and businesses:

- **Reduced Downtime**: Refresh systems in minutes rather than hours or days required for reimaging
- **Extended Hardware Lifecycle**: Revitalize aging hardware without replacement costs
- **Lower Support Burden**: Resolve common performance issues with a standardized approach
- **Improved Productivity**: End users experience faster, more reliable systems without losing their data
- **Cost Savings**: Minimize the need for specialized technical intervention and reduce new hardware purchases
- **Compliance Support**: Restore systems to optimal state while maintaining security configurations
- **Consistent Results**: Standardized approach ensures reliable outcomes across different machine configurations

## Advanced Usage

### Command Line Parameters

```powershell
.\WindowsRefresh.ps1 [-NoRestore] [-Silent] [-NoAppCleanup] [-Light]
```

| Parameter | Description |
|-----------|-------------|
| `-NoRestore` | Skip creating a system restore point |
| `-Silent` | Run with minimal prompts (auto-accepts defaults) |
| `-NoAppCleanup` | Skip app cleanup and reset |
| `-Light` | Perform a lighter refresh (faster but less thorough) |

### Configuration

Edit the script to customize:
- Services to optimize
- Apps to remove
- Cleanup targets
- Performance settings

## Technical Details

### Security Descriptors

The script uses Security Descriptor Definition Language (SDDL) strings to reset service permissions. For example:

```powershell
D:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWRPWPDTLOCRRC;;;SY)
```

These complex strings define permissions for different security principals:

**For Built-in Administrators (BA):**
- `D:` - Begins a Discretionary Access Control List (DACL)
- `(A;` - Starts an Access Control Entry (ACE) of type "Allow"
- `;;` - Field separators
- `CCDCLCSWRPWPDTLOCRSDRCWDWO` - Permission flags:
  - `CC` - SERVICE_QUERY_CONFIG (Query service configuration)
  - `DC` - SERVICE_CHANGE_CONFIG (Change service configuration)
  - `LC` - SERVICE_QUERY_STATUS (Query service status)
  - `SW` - SERVICE_ENUMERATE_DEPENDENTS (Enumerate dependent services)
  - `RP` - SERVICE_START (Start the service)
  - `WP` - SERVICE_STOP (Stop the service)
  - `DT` - SERVICE_PAUSE_CONTINUE (Pause/resume service)
  - `LO` - SERVICE_INTERROGATE (Interrogate service)
  - `CR` - SERVICE_USER_DEFINED_CONTROL (User-defined control codes)
  - `SD` - DELETE (Delete the service)
  - `RC` - READ_CONTROL (Read security descriptor)
  - `WD` - WRITE_DAC (Modify DACL)
  - `WO` - WRITE_OWNER (Change owner)
- `;;;` - More field separators
- `BA)` - Indicates the Built-in Administrators group

**For Local System Account (SY):**
- `(A;;CCLCSWRPWPDTLOCRRC;;;SY)` - Grants the following permissions:
  - `CC` - SERVICE_QUERY_CONFIG
  - `LC` - SERVICE_QUERY_STATUS
  - `SW` - SERVICE_ENUMERATE_DEPENDENTS
  - `RP` - SERVICE_START
  - `WP` - SERVICE_STOP
  - `DT` - SERVICE_PAUSE_CONTINUE
  - `LO` - SERVICE_INTERROGATE
  - `CR` - SERVICE_USER_DEFINED_CONTROL
  - `RC` - READ_CONTROL

These permissions are critical for proper service operation—they ensure that both administrators and the system have appropriate access to manage Windows services after reset.

### Windows Image Maintenance

The script uses DISM with specific parameters:

```powershell
DISM.exe /Online /Cleanup-Image /StartComponentCleanup /ResetBase
```

This command:
- `/Online` - Targets the running Windows installation
- `/Cleanup-Image` - Performs image maintenance
- `/StartComponentCleanup` - Removes superseded components
- `/ResetBase` - Removes all superseded versions of components

## Logging

The script creates a detailed log file in the same directory:

```
WindowsRefresh_YYYYMMDD_HHMMSS.log
```

Log entries include:
- Timestamp
- Operation level (INFO, WARNING, ERROR, SUCCESS)
- Detailed description of actions
- Command results and error information

## Implementation Considerations

### Preparation
1. **Create a backup** before running this script
2. Always run on a **stable power source**
3. Close all applications before execution
4. Ensure adequate disk space (minimum 2GB free)

### Execution Environment
1. Some operations may take **considerable time** on older systems
2. **Do not interrupt** the script once started
3. System **restart is required** after completion
4. Enterprise deployment should be tested on representative systems first

### Post-Execution
1. Verify system stability after reboot
2. Check event logs for potential issues
3. Review the generated log file
4. Update antivirus definitions (some may flag the cleaned system)

## Contributing

Contributions welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -m 'Add system improvement'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

- Microsoft documentation on system maintenance best practices
- PowerShell community for scripting techniques
- Enterprise IT administrators who provided valuable feedback

---

Star this repo if you found it useful!
