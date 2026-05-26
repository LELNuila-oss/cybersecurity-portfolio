# Project: Basic Network Connectivity and DNS Analysis

## Date

YYYY-MM-DD

## Summary

This project documents basic network connectivity and DNS analysis using common networking commands.

## Objective

The objective of this project is to practice:

- Checking local network configuration
- Testing connectivity
- Resolving domain names
- Understanding basic network paths

## Tools Used

- Windows Command Prompt
- PowerShell
- ping
- nslookup
- tracert

## Commands Used

```powershell
ipconfig
ping google.com
nslookup google.com
tracert google.com
```

## Evidence Collected

| Command | Purpose |
|---|---|
| ipconfig | Shows local IP configuration |
| ping | Tests connectivity to a host |
| nslookup | Resolves a domain name to an IP address |
| tracert | Shows the path packets take to reach a destination |

## Analysis

The `ipconfig` command helps identify the local IP address, default gateway, and DNS configuration.

The `ping` command tests if the device can reach an external domain.

The `nslookup` command shows how DNS resolves a domain name into an IP address.

The `tracert` command shows the network path between my device and the destination.

## Findings

- The device had an active network configuration.
- DNS resolution worked successfully.
- External connectivity was available.
- The route to the destination passed through multiple network hops.

## Risk

If DNS resolution fails, users may not be able to access websites by name. If connectivity fails, there may be issues with the local network, gateway, firewall, or internet service provider.

## Recommendations

- Verify IP configuration when troubleshooting connectivity issues.
- Check DNS settings if domain names do not resolve.
- Use ping and tracert to identify where connectivity may be failing.
- Document network behavior during troubleshooting.

## Conclusion

This project helped me understand basic network troubleshooting commands that are useful for IT support, NOC, and SOC analyst roles.

## Skills Demonstrated

- Basic networking
- DNS analysis
- Command line usage
- Troubleshooting methodology
- Technical documentation
