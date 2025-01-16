# Lolbas CertUtil

[Lolol Farm](https://lolol.farm/) is a project that groups all living of the land techniques. [Lolbas](https://lolbas-project.github.io/#) is specifically targetting Windows binaries.

## Download file from Internet Case 1

Test:

```Shell
certutil.exe -urlcache -split -f http://7-zip.org/a/7z1604-x64.exe 7zip.exe
```

This gets detected and prevented by Microsoft Defender but (16th of January 2025) instead of detecting the download using a lolbin it named the incident `Defender prevented execution of 'Trojan:Win/Ceprolad.A' in the command line ...`.
It tags it as a `low` priority event since it got prevented.

## Download file from Internet Case 2

Test:

```Shell
certutil.exe -verifyctl -f -split http://7-zip.org/a/7z1604-x64.exe 7zip.exe
```

## Download file from Internet and Save to alternate data stream

Test:

```
certutil.exe -urlcache -split -f https://raw.githubusercontent.com/Xiobe/Get-ShortcutsContent/refs/heads/main/Get-LNKShortcutsContent.ps1 c:\temp:ttt
```

## Encode a file

### Encode to a base64 encoded file

Test:

```
certutil -encode c:\windows\system32\calc.exe encoded_calc.exe
```

### Encode to a hexadecimal encoded file

Test:

```
certutil -encodehex c:\windows\system32\calc.exe encodedhex_calc.exe
```

## Decode a file

### Decode a base64 file

Test:

```
certutil -decode encoded_calc.exe decoded_calc.exe
```

### Decode a hexadecimal encoded file

Test:

```
certutil -decodehex encodedhex_calc.exe decodedhex_calc.exe
```
