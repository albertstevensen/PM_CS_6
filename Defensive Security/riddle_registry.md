# picoCTF - Easy - Forensics

## Challenge Description
Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.
Find the PDF file here Hidden Confidential Document and uncover the flag within the metadata.

## Tools Used
- ExifTool – extract metadata PDF
- Windows CMD – terminal commands
- certutil – decode Base64 (built-in Windows)

## Step 1: Prepare Files
Download PDF and ExifTool to local folder:
```
"C:\xxx\xxx\Desktop\Defensive\confidential.pdf"
"C:\Program Files\ExifTool\exiftool(-k).exe"
```
---

## Step 2: Extract Metadata

**Command:**
```
"C:\Program Files\ExifTool\exiftool(-k).exe" "C:\xxx\xxx\Desktop\Defensive\confidential.pdf"
```

**Output:**
```
ExifTool Version Number         : 13.50
File Name                       : confidential.pdf
Directory                       : C:/xxx/xxx/Desktop/Defensive
File Size                       : 183 kB
Zone Identifier                 : Exists
File Type                       : PDF
Page Count                       : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=
```

> Note: Field Author terlihat mencurigakan, panjang dan acak → ini Base64.

---

## Step 3: Decode Base64 (Windows CMD)

**Command:**
```
echo cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0= > temp.txt
certutil -decode temp.txt decoded.txt
type decoded.txt
del temp.txt decoded.txt
```

**Output:**
```
> Input Length = 59
> Output Length = 41
> CertUtil: -decode command completed successfully.

picoCTF{puzzl3d_m3tadata_f0und!_REDACTED}
```

---

## Flag

```
picoCTF{puzzl3d_m3tadata_f0und!_REDACTED}
```