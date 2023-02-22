![](./assets/banner.png)

<p align="center">
     <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/bar-follow-me-on.png">
     <br>
     <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/youtube.png">
     <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/twitter.png">
     <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/none.png">
</p>

I'm a french Security Researcher publishing opensource security tools to test for vulnerabilities on many environments. I truly love to tinker with undefined behaviors in computers, mostly in Windows, Active Directory and various web apps. I've publicly released 83 projects and tools so far, and I'm planning to publish many more! 🥳

If any of my tools helped you, please consider sponsoring my work! Sponsorship will help me cover the costs of my projects (server costs, mainframe restoration, buying books on a research subject ...). You can support my work through Patreon: [https://www.patreon.com/podalirius](https://www.patreon.com/podalirius)

I'm also constantly reporting security vulnerabilities found everywhere. I currently have reported **10** of security vulnerabilities found in the wild ([see responsible disclosures](https://github.com/p0dalirius/p0dalirius/blob/main/Responsible-disclosures.md)) and got **6** CVEs ([CVE-2020-16147](https://podalirius.net/en/cves/2020-16147/), [CVE-2020-16148](https://podalirius.net/en/cves/2020-16148/), [CVE-2021-43008](https://podalirius.net/en/cves/2021-43008/), [CVE-2022-26159](https://podalirius.net/en/cves/2022-26159/), [CVE-2022-29710](https://podalirius.net/en/cves/2022-29710/), [CVE-2022-30780](https://podalirius.net/en/cves/2022-30780/)) + 2 waiting for release

<h3 align="left">Connect with me:</h3>

 - 📺 My Youtube channel: <a href="https://www.youtube.com/c/Podalirius_?sub_confirmation=1" title="Subscribe"><img alt="YouTube Channel Subscribers" src="https://img.shields.io/youtube/channel/subscribers/UCF_x5O7CSfr82AfNVTKOv_A?style=social"></a>

 - 🐦 Follow me on Twitter: <a href="https://twitter.com/intent/follow?screen_name=podalirius_" title="Follow"><img src="https://img.shields.io/twitter/follow/podalirius_?label=Podalirius&style=social"></a>
 
 - 📝 My website: [https://podalirius.net/](https://podalirius.net/)

 - 🐘 Mastodon: [https://infosec.exchange/@podalirius](https://infosec.exchange/@podalirius)

<p align="center">
<img src="https://github-readme-stats.vercel.app/api?username=p0dalirius&show_icons=true&include_all_commits=true">
</p>

---

## Summary of my tools

### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-ad.png" width="2%" height="2%"> Active Directory tools

 - [AccountShadowTakeover](https://github.com/p0dalirius/AccountShadowTakeover): A python script to automatically add a KeyCredentialLink to newly created users, by quickly connecting to them with default credentials.
 - [Coercer](https://github.com/p0dalirius/Coercer): A python script to automatically coerce a Windows server to authenticate on an arbitrary machine through 9 methods.
 - [DomainUsersToXLSX](https://github.com/p0dalirius/DomainUsersToXLSX): Extract all users from an Active Directory domain to an Excel worksheet.
 - [DumpSMBShare](https://github.com/p0dalirius/DumpSMBShare): A script to dump files and folders remotely from a Windows SMB share.
 - [FindUncommonShares](https://github.com/p0dalirius/FindUncommonShares): A Python tool allowing to quickly find uncommon shares in vast Windows Domains.
 - [ldap2json](https://github.com/p0dalirius/ldap2json): The ldap2json script allows you to extract the whole LDAP content of a Windows domain into a JSON file. 
 - [ldapconsole](https://github.com/p0dalirius/ldapconsole): The ldapconsole script allows you to perform custom LDAP requests to a Windows domain.
 - [LDAPmonitor](https://github.com/p0dalirius/LDAPmonitor): Monitor creation, deletion and changes to LDAP objects live during your pentest or system administration! 
 - [MSRPRN-Coerce](https://github.com/p0dalirius/MSRPRN-Coerce): A python script to force authentification using MS-RPRN RemoteFindFirstPrinterChangeNotificationEx function (opnum 69).
 - [pydsinternals](https://github.com/p0dalirius/pydsinternals): A Python native library containing necessary classes, functions and structures to interact with Windows Active Directory. 
 - [pyLAPS](https://github.com/p0dalirius/pyLAPS): Python setter/getter for property ms-Mcs-AdmPwd used by LAPS.
 - [TargetAllDomainObjects](https://github.com/p0dalirius/TargetAllDomainObjects): A python wrapper to run a command on against all users/computers/DCs of a Windows Domain.
 
### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-www.png" width="2%" height="2%"> Web exploitation tools

 - [Awesome-RCE-techniques](https://github.com/p0dalirius/Awesome-RCE-techniques): Awesome list of techniques to achieve Remote Code Execution on various apps!
 - [crawlersuseragents](https://github.com/p0dalirius/crawlersuseragents): Python script to check if there is any differences in responses of an application when the request comes from a search engine's crawler. 
 - [http-fuzzing-scripts](https://github.com/p0dalirius/http-fuzzing-scripts): A collection of http fuzzing python scripts to fuzz HTTP servers for bugs. 
 - [ipsourcebypass](https://github.com/p0dalirius/ipsourcebypass): This Python script can be used to bypass IP source restrictions using HTTP headers. 
 - [JoGet-plugin-webshell](https://github.com/p0dalirius/JoGet-plugin-webshell): A webshell plugin and interactive shell for pentesting JoGet application. 
 - [LimeSurvey-plugin-webshell](https://github.com/p0dalirius/LimeSurvey-plugin-webshell): A webshell plugin and interactive shell for pentesting JoGet application. 
 - [LFIDump](https://github.com/p0dalirius/LFIDump): A simple python script to dump remote files through a local file read or local file inclusion web vulnerability. 
 - [LootApacheServerStatus](https://github.com/p0dalirius/LootApacheServerStatus): A script to automatically dump all URLs present in /server-status to a file locally. 
 - [Moodle-webshell-plugin](https://github.com/p0dalirius/Moodle-webshell-plugin): A webshell plugin and interactive shell for pentesting a Moodle instance.
 - [owabrute](https://github.com/p0dalirius/owabrute): Hydra wrapper for bruteforcing Microsoft Outlook Web Application. 
 - [RDWArecon](https://github.com/p0dalirius/RDWArecon): A python script to extract information from a Microsoft Remote Desktop Web Access (RDWA) application.
 - [robotstester](https://github.com/p0dalirius/robotstester): This Python script can enumerate all URLs present in robots.txt files, and test whether they can be accessed or not.
 - [robotsvalidator](https://github.com/p0dalirius/robotsvalidator): The robotsvalidator script allows you to check if URLs are allowed or disallowed by a robots.txt file. 
 - [TimeBasedLoginUserEnum](https://github.com/p0dalirius/TimeBasedLoginUserEnum): A script to enumerate valid usernames based on the requests response times.
 - [Tomcat-application-webshell](https://github.com/p0dalirius/Tomcat-application-webshell): A webshell application and interactive shell for pentesting Apache Tomcat servers. 
 - [webapp-wordlists](https://github.com/p0dalirius/webapp-wordlists): This repository contains wordlists for each versions of common web applications and content management systems (CMS). Each version contains a wordlist of all the files directories for this version.

### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-target.png" width="2%" height="2%"> Vulnerability exploits

 - [RemoteMouse-3.008-Exploit](https://github.com/p0dalirius/RemoteMouse-3.008-Exploit): This exploit allows to connect to the remote RemoteMouse 3.008 service to virtually press arbitrary keys and execute code on the machine. 
 - [CVE-2016-10956-mail-masta](https://github.com/p0dalirius/CVE-2016-10956-mail-masta): MailMasta wordpress plugin Local File Inclusion vulnerability (CVE-2016-10956).
 - [CVE-2020-14144-GiTea-git-hooks-rce](https://github.com/p0dalirius/CVE-2020-14144-GiTea-git-hooks-rce): A script to exploit CVE-2020-14144 - GiTea authenticated Remote Code Execution using git hooks.
 - [CVE-2021-43008-AdminerRead](https://github.com/p0dalirius/AdminerRead): Exploit tool for Adminer 1.0 up to 4.6.2 Arbitrary File Read vulnerability.
 - [CVE-2022-21907-http.sys](https://github.com/p0dalirius/CVE-2022-21907-http.sys): Proof of concept of CVE-2022-21907 Double Free in http.sys driver, triggering a kernel crash on IIS servers
 - [CVE-2022-26159-Ametys-Autocompletion-XML](https://github.com/p0dalirius/CVE-2022-26159-Ametys-Autocompletion-XML): A python exploit to automatically dump all the data stored by the auto-completion plugin of Ametys CMS to a local sqlite database file. 
 - [CVE-2022-30780-lighttpd-denial-of-service](https://github.com/p0dalirius/CVE-2022-30780-lighttpd-denial-of-service): CVE-2022-30780 - lighttpd remote denial of service 

### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-microsoft-logo.png" width="2%" height="2%"> Windows

 - [DownloadPDBSymbols](https://github.com/p0dalirius/DownloadPDBSymbols): A Python script to download PDB files associated with a Portable Executable (PE).
 - [hivetools](https://github.com/p0dalirius/hivetools): A collection of python scripts to work with Windows Hives. 
 - [msFlagsDecoder](https://github.com/p0dalirius/msFlagsDecoder): Decode the values of common Windows properties such as userAccountControl and sAMAccountType.
 - [OffensiveBatchScripts](https://github.com/p0dalirius/OffensiveBatchScripts): Offensive batch scripts. 
 - [SortWindowsISOs](https://github.com/p0dalirius/SortWindowsISOs): Extract the windows major and minor build numbers from an ISO file, and automatically sort the iso files.
 
### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-data.png" width="2%" height="2%"> Data & Researches

 - [linux-kernels](https://github.com/p0dalirius/linux-kernels): List of linux kernel versions in JSON.
 - [microsoft-rpc-fuzzing-tools](https://github.com/p0dalirius/microsoft-rpc-fuzzing-tools): This repository contains a list of python scripts to work with Microsoft RPC for research purposes. 
 - [volatility3-symbols](https://github.com/p0dalirius/volatility3-symbols): Memory mapping profiles for forensic analysis using volatility 3.
 - [volatility2-profiles](https://github.com/p0dalirius/volatility2-profiles): Memory mapping profiles for forensic analysis using volatility 2.
 - [WindowsBuilds](https://github.com/p0dalirius/WindowsBuilds): This repository contains the list of windows builds as parsable JSON files.
 - [windows-coerced-authentication-methods](https://github.com/p0dalirius/windows-coerced-authentication-methods): A list of methods to coerce a windows machine to authenticate to an attacker-controlled machine through a Remote Procedure Call (RPC) with various protocols. 
 
### <img src="https://raw.githubusercontent.com/p0dalirius/p0dalirius/main/assets/icon-arrow.png" width="2%" height="2%"> Other

 - [Argon2Cracker](https://github.com/p0dalirius/Argon2Cracker): A multithreaded bruteforcer of argon2 hashes.
 - [ctfd-parser](https://github.com/p0dalirius/ctfd-parser): A python script to dump all the challenges locally of a CTFd-based Capture the Flag.
 - [factorizator](https://github.com/p0dalirius/factorizator): A script to factorize integers with sagemath and factordb. 
 - [GetFortinetSerialNumber](https://github.com/p0dalirius/GetFortinetSerialNumber): A Python script to extract the serial number of a remote Fortinet device.
 - [GithubBackupAllRepos](https://github.com/p0dalirius/GithubBackupAllRepos): A Python script to backup all repos (public or private) of a user.
 - [Hashes-Harvester](https://github.com/p0dalirius/Hashes-Harvester): Automatically extracts NTLM hashes from Windows memory dumps.
 - [ParseFortinetSerialNumber](https://github.com/p0dalirius/ParseFortinetSerialNumber): A Python script to parse Fortinet products serial numbers, and detect the associated model and version.
 - [python_packages_paths](https://github.com/p0dalirius/python_packages_paths): This repository contains paths to python modules from inside python modules.
 - [streamableDownloader](https://github.com/p0dalirius/streamableDownloader): A simple python script to download videos hosted on streamable from their link.
 - [wav2mmv](https://github.com/p0dalirius/wav2mmv): WAV to MMV converter. You can then use the MMV file in input of MSSTV to decode Slow Scan Television (SSTV) sound signals.
 - [WifiListProbeRequests](https://github.com/p0dalirius/WifiListProbeRequests): Monitor 802.11 probe requests from a capture file or network sniffing!
