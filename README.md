# MikroTik Auto-Upgrade Script

This script automates the upgrade process for MikroTik RouterBOARD firmware and RouterOS packages. It is designed to be robust, efficient, and easy to configure.

## Features

- Automatically checks and upgrades RouterBOARD firmware if outdated.
- Checks for RouterOS updates and downloads them if available.
- Uses a file flag to persist upgrade phase across reboots.
- Logs upgrade status and device information.
- Configurable update channel with default set to `testing`.

## Configuration

### Update Channel

Set the update channel by modifying the `updateChannel` variable in the script. Valid options are:

- `stable`
- `testing` (default)
- `development`
- `long term`

Example:

```mikrotik
:local updateChannel "testing"
```

## Scheduling

To automate the script execution, add the following schedulers in your MikroTik device:

```mikrotik
/system scheduler
add name=StartupAutoUpgrade on-event="/system script run auto-upgrade" policy=reboot,read,write,policy start-time=startup
add interval=1w name=weeklyAutoUpdate on-event="/system script run auto-upgrade" policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon start-date=2025-06-23 start-time=02:00:00
```

- `StartupAutoUpgrade` runs the script at device startup.
- `weeklyAutoUpdate` runs the script weekly at 2:00 AM starting from June 23, 2025.

## Usage

1. Place the `auto-upgrade` script on your MikroTik device.
2. Configure the `updateChannel` variable as desired.
3. Add the schedulers as shown above.
4. The script will handle upgrades automatically and reboot the device as needed.

## Notes

- The script logs important events and upgrade statuses.
- It cleanly exits without rebooting if no upgrade is needed.
- Ensure you have backups before running automated upgrades.

## License

This script is provided as-is without warranty. Use at your own risk.
