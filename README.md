# Linux Web Server Troubleshooting Lab

## Objective
Practice investigating a web server outage, restoring the service, and documenting the results.

## Environment
- Debian 13 virtual machine in VirtualBox
- nginx web server
- Linux command line

## 1. Install the tools
```bash
sudo apt update
sudo apt install nginx
sudo apt install curl
```
`apt update` refreshed the available software list. I installed nginx to serve web pages and curl to test HTTP responses.

## 2. Verify normal operation
```bash
systemctl status nginx --no-pager
curl -I http://127.0.0.1
```
The service showed active (running). The local HTTP test returned 200 OK.

## 3. Simulate an outage
```bash
sudo systemctl stop nginx
curl -I http://127.0.0.1
```
I deliberately stopped nginx. The HTTP test then failed to connect.

## 4. Investigate the cause
```bash
systemctl status nginx --no-pager
sudo journalctl -u nginx -n 20 --no-pager
```
The service showed inactive (dead). The logs recorded a clean stop, consistent with my deliberate action.

## 5. Restore and verify
```bash
sudo systemctl start nginx
systemctl status nginx --no-pager
curl -I http://127.0.0.1
```
After restarting nginx, the service showed active (running), and the HTTP test returned 200 OK again.

## 6. Document the findings
I saved the problem, evidence, cause, resolution, and verification in nginx-findings.txt.

## Outcome
I completed a controlled service-outage investigation and verified recovery from inside the VM. This was a troubleshooting exercise, not a security attack.

## What I learned
- Check both service status and the actual HTTP response.
- Use service logs to understand what happened.
- Verify recovery before documenting an issue as resolved.
- Distinguish an intentional service stop from a crash.

## Screenshots
The uploaded screenshot folder contains evidence of installation, normal operation, the outage, service logs, recovery, and final findings.
