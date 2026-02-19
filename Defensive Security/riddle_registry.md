# picoCTF - Easy - Forensics

## Challenge Description
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.
Find the PDF file here Hidden Confidential Document and uncover the flag within the metadata.

## Tools Used
- **ExifTool** – extract metadata PDF
- **Windows CMD** – terminal commands
- **certutil** – decode Base64 (built-in Windows)

## Step 1: Prepare Files
Download PDF and ExifTool to local folder:

C:\xxx\xxx\Desktop\Defensive\confidential.pdf
C:\Program Files\ExifTool\exiftool(-k).exe

## Step 2: Extract Metadata
```cmd
"C:\Program Files\ExifTool\exiftool(-k).exe" "C:\xxx\xxx\Desktop\Defensive\confidential.pdf"

### Response
ExifTool Version Number         : 13.50
File Name                       : confidential.pdf
Directory                       : C:/xxx/xxx/Desktop/Defensive
File Size                       : 183 kB
Zone Identifier                 : Exists
File Modification Date/Time     : 2026:02:20 00:47:27+07:00
File Access Date/Time           : 2026:02:20 01:30:57+07:00
File Creation Date/Time         : 2026:02:20 00:47:27+07:00
File Permissions                : -rw-rw-rw-
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=
-- press ENTER --
> Note: Field Author terlihat mencurigakan, panjang dan acak → ini Base64.

## Step 3: Decode Base64 (Windows CMD)
echo cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0= > temp.txt
certutil -decode temp.txt decoded.txt
type decoded.txt

> Input Length = 59
> Output Length = 41
> CertUtil: -decode command completed successfully.

picoCTF{puzzl3d_m3tadata_f0und!_REDACTED}

## Flag
picoCTF{puzzl3d_m3tadata_f0und!_REDACTED}
