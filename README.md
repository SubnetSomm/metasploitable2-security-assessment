# Metasploitable2 security assessment

**Franco Pisano · ITN 261 · Summer 2026 · Authorized home-lab capstone**

I built a mixed-architecture lab, mapped a deliberately vulnerable target, compared scanner output with service evidence, and validated two remote-command-execution findings. Both controlled exploit paths produced root access on Metasploitable2.

## Lab and scope

Kali Linux ran as an ARM guest in VMware Fusion Pro on an Apple-silicon MacBook. The x86 Metasploitable2 target ran in UTM. Bridged networking allowed the guests to communicate. This was my authorized lab; the target was powered off outside project use. The historical bridged layout is documented as used, not presented as an isolation model for future vulnerable-machine deployments.

## Project flow

1. Establish the lab and identify the target.
2. Discover services using Netdiscover and Nmap.
3. Review OpenVAS/Greenbone findings and investigate service/version evidence.
4. Research the Samba username-map vulnerability and UnrealIRCd backdoor.
5. Validate the selected conditions using Metasploit and record identity/host evidence.
6. Assess impact and propose remediation and retesting.

## Validated findings

| Finding | Lab evidence | Result |
|---|---|---|
| Samba username-map command execution, CVE-2007-2447 | Affected service evidence, module configuration and shell identity/host output | Root command shell |
| Trojanized UnrealIRCd 3.2.8.1, CVE-2010-2075 | Service/version evidence, module check, session establishment and shell identity output | Root session |

An open SMB/IRC port alone does not establish either condition. The Samba path depends on the vulnerable configuration, and the UnrealIRCd issue concerns compromised builds rather than every installation with that version label.

## Evidence highlights

![Samba root-shell evidence](assets/image9.png)

![UnrealIRCd root-shell evidence](assets/image12.png)

The [full report](report/final-report.md) preserves topology, scanner/service evidence, vulnerability analysis, controlled test details, risk and mitigation recommendations.

## What I learned

| Objective | Supporting work | Status |
|---|---|---|
| Build a usable mixed-architecture lab | Kali ARM plus x86 target across two hypervisors | Documented |
| Connect enumeration with vulnerability research | Nmap service/version evidence and selected CVEs | Documented |
| Validate exploitability and access level | Sessions plus id/whoami/hostname evidence | Demonstrated in saved screenshots |
| Evaluate scanner coverage | Initial limited scan versus later scan and manual validation | Documented; scan runs kept distinct |
| Recommend layered remediation | Patching/rebuild, exposure reduction, least privilege, monitoring and retesting | Recommendations; not verified fixes |

The most useful lesson was to separate discovery, scanner findings, manual validation and corrective recommendations. An automated scan is one input to an assessment, and a successful exploit is evidence of a specific tested path rather than proof of every possible risk.

## Timeline and interpretation limits

The saved report prose and embedded evidence span more than one run. The prose describes July activity; later evidence shows a July 31 scan and August 1 testing. The target’s displayed date differs from the host/session clock. I retain that discrepancy instead of presenting a falsely precise chronology. Screenshot captions and the report’s evidence note explain the distinction.

The screenshots show successful lab access. The report recommends remediation and retesting; it does not establish those fixes were deployed. CVSS values and vendor references are preserved as historical report content.

## Provenance

Converted from my revised final report, preserving its original structure and reviewed screenshots. Portfolio formatting and evidence caveats were prepared with AI assistance. The scenario uses deliberately vulnerable Metasploitable2; it is not a third-party penetration-test engagement. Related guided exercises remain in [Subnetsomm-lab](https://github.com/SubnetSomm/Subnetsomm-lab).
