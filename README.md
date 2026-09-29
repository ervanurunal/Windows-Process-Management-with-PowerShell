## Windows Process Management with PowerShell

### Overwiev

In this lab, I practiced **monitoring and managing Windows processes** using Windows PowerShell.

I learned how to:

* View running processes
* Search for a specific process
* Identify a process ID (PID)
* Terminate a specific process
* Search for multiple processes using wildcards
* Terminate multiple processes
* Verify that processes have been terminated

Process management is an important IT Support skill because excessive or malfunctioning processes can consume system resources and affect computer performance.

---

### Tools & Resources

* Windows Virtual Machine (Qwiklabs)
* Windows Task Viewer / Task Manager
* Windows PowerShell
* PowerShell `Get-Process`
* `taskkill`
* Process ID (PID)

### **Lab Type:** 
Windows / IT Support Hands-On Lab

----

## 1. Open Windows PowerShell as Administrator

Process termination requires administrative privileges in this lab.

### Steps

1. Open the **Start Menu**.
2. Search for **Windows PowerShell**.
3. Right-click **Windows PowerShell**.
4. Select **Run as Administrator**.
5. If prompted by User Account Control (UAC), select **Yes**.

![1](https://i.imgur.com/6ni26ZQ.png)

---

## 2. Find a Specific Process

Use the PowerShell `Get-Process` cmdlet to search for a process by name.

```powershell
Get-Process -Name "totally_not_malicious"
```

![2](https://i.imgur.com/EL799Ej.png)


#### *Purpose*

`Get-Process` retrieves information about processes currently running on the Windows system.

The command searches for the process named:

```text
totally_not_malicious
```

---

## 3. Understand Process IDs

A **Process ID (PID)** is a unique number assigned to a running process by Windows.

For example:

```text
Process Name: totally_not_malicious
PID: 7164
```

The PID allows Windows commands to identify a specific running process.

---

## 4. Terminate a Specific Process

The `taskkill` command can terminate a process using its PID.

```cmd
taskkill /F /PID [PROCESS ID]
```

![3](https://i.imgur.com/Q24Elel.png)

### *Command Breakdown*

| Option     | Meaning                         |
| ---------- | ------------------------------- |
| `taskkill` | Terminates a running process    |
| `/F`       | Forces the process to terminate |
| `/PID`     | Specifies a Process ID          |
| `7164`     | Example Process ID              |


---

## 5. Verify the Process Was Terminated

Run the search again:

```powershell
Get-Process -Name "totally_not_malicious"
```

Because the process has been terminated, PowerShell should report that no process with that name was found.

![3](https://i.imgur.com/IPSjlMp.png)

---

## 6. Search for Multiple Processes

The lab also contains processes with the word:

```text
razzle
```

The following command searches for an exact process name:

```powershell
Get-Process -Name "razzle"
```

However, this may not find processes such as:

```text
razzle_one
razzle_two
```

because `Get-Process -Name` normally searches for the specified process name.

---

## 7. Use a Wildcard to Find Partial Matches

A wildcard allows us to search for processes containing a specific word.

Use:

```powershell
Get-Process -Name "*razzle*"
```

![4](https://i.imgur.com/oA1HVk1.png)

---

## 8. Identify the PIDs

The command:

```powershell
Get-Process -Name "*razzle*"
```

should display the processes containing `razzle`.

![4](https://i.imgur.com/oA1HVk1.png)

---

## 9. Terminate the First Process

Use `taskkill` with the first PID:

```cmd
taskkill /F /PID [PROCESS ID]
```

![5](https://i.imgur.com/SKH840I.png)

---

## 10. Terminate the Second Process

Use `taskkill` again with the second PID:

```cmd
taskkill /F /PID [PROCESS ID]
```

![5](https://i.imgur.com/SKH840I.png)

---

## 11. Verify Multiple Processes Were Terminated

Run:

```powershell
Get-Process -Name "*razzle*"
```

If all matching processes have been terminated, the command should return no matching processes.

This confirms that the processes containing `razzle` are no longer running.

![6](https://i.imgur.com/O4LzUP4.png)

---

### Commands Learned

| Command                      | Purpose                            |
| ---------------------------- | ---------------------------------- |
| `Get-Process`                | Displays running processes         |
| `Get-Process -Name "name"`   | Finds a process by name            |
| `Get-Process -Name "*name*"` | Finds processes containing a name  |
| `taskkill /PID [PID]`        | Terminates a process using its PID |
| `taskkill /F /PID [PID]`     | Forcefully terminates a process    |
| `*`                          | Wildcard for matching characters   |
| `Id`                         | Process ID (PID)                   |

---

### Key Concepts

#### Process

A **process** is a program that is currently running on a computer.

---

#### Process ID (PID)

A **PID** is a unique numerical identifier assigned to a running process.

---

#### Get-Process

PowerShell's `Get-Process` cmdlet provides information about running processes.

---

#### Wildcards

The `*` character is a wildcard.

---

#### taskkill

`taskkill` is a Windows command-line utility used to terminate processes.

---

### Cybersecurity Relevance

Process management is also relevant to cybersecurity and SOC Analyst work.

Security analysts may examine running processes when investigating:

* Suspicious applications
* Malware
* Unauthorized software
* Resource-intensive processes
* Abnormal system activity
* Potentially compromised systems


For example, a SOC Analyst may investigate an unfamiliar process by checking its:

* Process name
* PID
* Parent process
* Command line
* Resource usage
* Network activity
* File location

Understanding Windows processes provides an important foundation for security monitoring and incident response.

---

### Troubleshooting Notes

#### Process not found

If:

```powershell
Get-Process -Name "process_name"
```

does not find a process, check the spelling of the process name.

You can also list all processes:

```powershell
Get-Process
```

---

#### Partial process name does not work

Instead of:

```powershell
Get-Process -Name "razzle"
```

try:

```powershell
Get-Process -Name "*razzle*"
```

The wildcard searches for processes containing the specified text.

---

#### Access denied when terminating a process

Make sure PowerShell is running as Administrator:

**Start → Windows PowerShell → Right-click → Run as Administrator**

---

#### Need to identify a PID

Run:

```powershell
Get-Process
```

or:

```powershell
Get-Process -Name "process_name"
```

Then look at the:

```text
Id
```

column.

---

#### Process Management Workflow

A basic process-management workflow is:

```text
1. Identify the process
        ↓
2. Find the PID
        ↓
3. Terminate the process
        ↓
4. Verify the process is no longer running
```

Example:

```powershell
Get-Process -Name "totally_not_malicious"
```

↓

```text
Find PID
```

↓

```cmd
taskkill /F /PID [PID]
```

↓

```powershell
Get-Process -Name "totally_not_malicious"
```

↓

```text
Process no longer exists
```

---

### Skills Demonstrated


**Technical Skills**

* Windows process management
* PowerShell
* `Get-Process`
* `taskkill`
* Process ID identification
* Wildcard searches
* Command-line troubleshooting


**IT Support Skills**

* Process monitoring
* Troubleshooting running applications
* Identifying problematic processes
* Terminating unresponsive or unwanted processes
* Windows administration


**Cybersecurity Foundation**

* Windows process analysis
* Suspicious process identification
* Endpoint monitoring
* Malware investigation fundamentals
* Incident-response fundamentals

---

### Final Takeaway

This lab gave me hands-on experience with **Windows process management using PowerShell**.

I learned how to use `Get-Process` to identify running processes, find their PIDs, terminate processes with `taskkill`, use wildcards to locate multiple processes, and verify that processes were successfully terminated.

These skills provide a foundation for both **IT Support** and **Cybersecurity/SOC Analyst** roles.
