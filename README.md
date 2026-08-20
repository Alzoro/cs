# Digital Forensics CTF Cheat Sheet

A comprehensive, command-line focused cheat sheet repository tailored for cybersecurity students preparing for **Digital Forensics and Incident Response (DFIR) Capture The Flag (CTF)** competitions. 

This repository is optimized into 8 primary study categories that match common CTF practice areas, with a master operational lookup sheet at the beginning.

## Introduction to Forensic Categories

In a digital forensics CTF, you are handed raw artifacts or disk images and must piece together the attacker's actions. This repository organizes the essential tools and techniques into the following areas:
- **Operational Triage**: High-speed mapping of any evidence extension to its tool workflow.
- **Network Forensics**: Capturing and analyzing protocol sequences, file transfers, and connection histories.
- **Windows Memory Forensics**: Extracting volatile artifacts from RAM captures (like processes, drivers, and network sockets).
- **Log Forensics**: Processing text-based log files using Linux command-line utilities, and parsing structured audit records (Windows Security logs and database authentications).
- **Windows Artifact Forensics**: Diving into Windows registry hives and parsing OS-specific tracking artifacts (Prefetch, LNK, ShellBags).
- **Disk/File-System Forensics**: Reconstructing partitions and recovering files from raw disk images.
- **Steganography**: Uncovering hidden data or secret ciphers embedded in cover images or audio streams.
- **Email Forensics**: Tracing phishing sources, email headers, authentication alignments, and malicious attachments.
- **Malware/File Analysis**: Triaging unknown executables, analyzing compiler signatures, extracting strings, and hashing for threat intel lookup.

---

## Digital Forensics CTF Workflow

Use this overall mental model when approaching a new forensic challenge:

```text
Identify evidence
       ↓
Determine forensic category
       ↓
Choose tool
       ↓
Filter/search
       ↓
Extract artifact
       ↓
Correlate evidence
       ↓
Answer the question
```

---

## Cheat Sheet Category Index

Click on any category to view its corresponding cheat sheet:

0. [**00_CTF_Artifact_Identification.txt**](./00_CTF_Artifact_Identification.txt)  
   *Master operational lookup index mapping forensic file extensions and clues to their categories and starting tools.*  
   * **Common Extensions/Clues**: `.pcap`, `.pcapng`, `.raw`, `.mem`, `.dmp`, `.evtx`, `.E01`, `.dd`, `.img`, `.jpg`, `.png`, `.bmp`, `.wav`, `.eml`, `.msg`, `.docx`, `.pdf`, `.exe`, `.dll`, `.elf`, Browser Files, Linux Logs, Registry Hives.
1. [**01_Network_Forensics.txt**](./01_Network_Forensics.txt)  
   *Network capture analysis (Wireshark protocol filters, TCP streams, object exports) and file transfer utilities (`wget`).*  
   * **Common Extensions**: `.pcap`, `.pcapng`, `.cap`
2. [**02_Windows_Memory_Forensics.txt**](./02_Windows_Memory_Forensics.txt)  
   *Volatility 3 plugins reference, memory investigation workflows, and process/network/registry triage mappings.*  
   * **Common Extensions**: `.raw`, `.mem`, `.dmp`, `.vmem`, `.img`
3. [**03_Log_Forensics.txt**](./03_Log_Forensics.txt)  
   *Linux text processing command-line utilities (`cut`, `tr` with ROT13, `grep`, `awk`, `sed` multi-line scripts) and auditing of successful/failed logons (Windows Security EVTX Event IDs `4624`/`4625`, SQL Server errors `18454`/`18456`).*  
   * **Common Extensions**: `.log`, `.evtx`, `.txt`, `syslog`, `auth.log`
4. [**04_Windows_Artifact_Forensics.txt**](./04_Windows_Artifact_Forensics.txt)  
   *Windows Registry analysis (`Registry Explorer`, `RECmd`, `RegRipper` plugins, auto-start persistence) and specialized Zimmerman artifact parsers (`PECmd`, `EvtxECmd`, `LECmd`, `JLECmd`, `SBECmd`, `RBCmd`, `MFTECmd`).*  
   * **Common Extensions**: `.hve` (Amcache.hve), `.DAT` (NTUSER.DAT), `.pf` (Prefetch), `.lnk` (Shortcuts), `$MFT`, `automaticDestinations-ms` (Jump Lists), `SAM`, `SYSTEM`, `SOFTWARE`
5. [**05_Disk_FileSystem_Forensics.txt**](./05_Disk_FileSystem_Forensics.txt)  
   *Raw partition analysis, metadata inspection, and file recovery using The Sleuth Kit (`mmls`, `fls`, `icat`, `fsstat`, `istat`, `ils`, `tsk_recover`) and GUI platforms (`FTK Imager`, `Autopsy`).*  
   * **Common Extensions**: `.E01`, `.dd`, `.img`, `.vmdk`, `.raw`
6. [**06_Steganography.txt**](./06_Steganography.txt)  
   *Image and audio steganography using `steghide` (JPEG/BMP/WAV/AU), `zsteg` (PNG/BMP LSB planes/channels), and automated web triage via `Aperi'Solve`.*  
   * **Common Extensions**: `.jpg`, `.jpeg`, `.png`, `.bmp`, `.wav`, `.au`, `.gif`
7. [**07_Email_Forensics.txt**](./07_Email_Forensics.txt)  
   *Email message investigation, bottom-to-top header tracing to find sender origin IP address, phishing indicators (SPF/DKIM/DMARC), display name spoofing, and attachment extraction.*  
   * **Common Extensions**: `.eml`, `.msg`
8. [**08_Malware_File_Analysis.txt**](./08_Malware_File_Analysis.txt)  
   *Metadata parsing (`ExifTool`), compiler/packer signature analysis (`Detect It Easy`), binary string extraction, cryptographic hashing, and querying VirusTotal.*  
   * **Common Extensions**: `.exe`, `.dll`, `.sys`, `.elf`, `.bin`, `.docx`, `.pdf`, `.db` (Browser History/Cache)

---

## Quick Artifact Identification Table

| Clue/File Extension | Forensic Category             | Start Tool          | Cheat Sheet File                  |
| ------------------- | ----------------------------- | ------------------- | --------------------------------- |
| `.pcap` / `.pcapng` | Network Forensics             | Wireshark / tshark  | [01_Network_Forensics.txt](./01_Network_Forensics.txt) |
| `.raw` / `.mem`     | Windows Memory Forensics      | Volatility 3        | [02_Windows_Memory_Forensics.txt](./02_Windows_Memory_Forensics.txt) |
| `.evtx`             | Log Forensics                 | EvtxECmd / Viewer   | [03_Log_Forensics.txt](./03_Log_Forensics.txt) |
| Linux Logs/History  | Log Forensics                 | Text editors / grep | [03_Log_Forensics.txt](./03_Log_Forensics.txt) |
| SQL Server Logs     | Log Forensics                 | Event Viewer        | [03_Log_Forensics.txt](./03_Log_Forensics.txt) |
| Registry Hives      | Windows Artifact Forensics    | Registry Explorer   | [04_Windows_Artifact_Forensics.txt](./04_Windows_Artifact_Forensics.txt) |
| Amcache.hve         | Windows Artifact Forensics    | AmcacheParser.exe   | [04_Windows_Artifact_Forensics.txt](./04_Windows_Artifact_Forensics.txt) |
| `.pf` (Prefetch)    | Windows Artifact Forensics    | PECmd.exe           | [04_Windows_Artifact_Forensics.txt](./04_Windows_Artifact_Forensics.txt) |
| `.lnk` (LNK shortcuts)| Windows Artifact Forensics  | LECmd.exe           | [04_Windows_Artifact_Forensics.txt](./04_Windows_Artifact_Forensics.txt) |
| `$MFT` (NTFS MFT)   | Windows Artifact Forensics    | MFTECmd.exe         | [04_Windows_Artifact_Forensics.txt](./04_Windows_Artifact_Forensics.txt) |
| `.E01` / `.dd` / `.img` | Disk/File-System Forensics | mmls / fls / FTK Imager | [05_Disk_FileSystem_Forensics.txt](./05_Disk_FileSystem_Forensics.txt) |
| `.jpg` / `.png` / `.bmp` | Steganography             | zsteg / Steghide    | [06_Steganography.txt](./06_Steganography.txt) |
| `.wav` / `.au` (Audio) | Steganography               | steghide info       | [06_Steganography.txt](./06_Steganography.txt) |
| `.eml` / `.msg`     | Email Forensics               | Thunderbird / editor| [07_Email_Forensics.txt](./07_Email_Forensics.txt) |
| `.docx` / `.pdf`    | Malware/File Analysis         | ExifTool            | [08_Malware_File_Analysis.txt](./08_Malware_File_Analysis.txt) |
| `.exe` / `.dll`     | Malware/File Analysis         | Detect It Easy (DIE)| [08_Malware_File_Analysis.txt](./08_Malware_File_Analysis.txt) |
| Browser Files       | Malware/File Analysis         | DB Browser (SQLite) | [08_Malware_File_Analysis.txt](./08_Malware_File_Analysis.txt) |
