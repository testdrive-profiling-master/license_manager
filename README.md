# license_manager
License Manager Sub-Package for TestDrive

```text
> Testdrive_LM
- TestDrive Profiling Master License Manager. (SEED 128bit + SHA256) - (build :Aug 23 2022)

Usage : testdrive_lm [options] OP ...
        [options]
            -f flag_file_name  : specify custom flag file name.
            -k key_file_name   : specify custom private key file name.
            -t tag_string      : specify custom tag string.
        OP
            register private_key
                : register private key on this system.
            export public_key
                : export public key file('.TestDrive.public_key').
            hash public_key (private_hash)
                : Get private Key.
            check [public_key]
                : check license status on public_key.
            encrypt input_files ...
                : encryt files.
            decrypt input_files ...
                : decrypt files.
            discard
                : discard all licenses on your system.
```

## 1. Make public key file (Host side)
```text
> TestDrive_LM export "PublicKey"
```
You can see the encypted ".TestDrive.public_key" file in the same working folder.   
For "PublicKeyName", enter the desired key sentence appropriately.   
"PublicKeyName" must not be shared with unauthorized persons, instead share the encrypted public key file ".TestDrive.public_key".

## 2. Encrypt your files (Host side)
```text
> TestDrive_LM encrypt yourfile.ext ...
```
(This operation can be executed only when the ".TestDrive.public_key" file exists in the current folder or its parent folder.)   
You can see the ".TestDrive.ext.encrypted" file in the same working folder.


## 3. Generate & Register private key from private hash (Client side)
First, you must check private hash code.
```text
> TestDrive_LM check
Your public key : C:/~/.TestDrive.public_key
*E: No private key. Contact your license manager with following your private hash code.

    - Your private hash : 538E1CC5EFF907074FCF25C82BAC2B772DED23F47DB235FC293018150A21C5A13900FCF928559443738E6626EA8C3D48346F8CF6568D5DDCF8C06B4445D033A4
```
The client side has no license rights to decrypt, and each client PC has a different private hash code.   
The client needs to generate private_key from private hash code to decrypt the files.   
   
Then, generate private code from private hash
```text
> TestDrive_LM hash "PublicKey" 538E1CC5EFF907074FCF25C82BAC2B772DED23F47DB235FC293018150A21C5A13900FCF928559443738E6626EA8C3D48346F8CF6568D5DDCF8C06B4445D033A4

SHA256 Private key : D140E28AB0FD52EE3AC3F26E7FC81FCCDA6054C2EFE53EF124EEF5A9206AF93D
```
Now you've got a private key "D140E28AB0FD52EE3AC3F26E7FC81FCCDA6054C2EFE53EF124EEF5A9206AF93D"   
   
And you must register the private code like this.
```text
> TestDrive_LM register D140E28AB0FD52EE3AC3F26E7FC81FCCDA6054C2EFE53EF124EEF5A9206AF93D
*I: Done.
```

## 4. Decrypt your files
```text
> TestDrive_LM decrypt yourfile.ext.encrypt ...
```
Now you can find decrypted file "yourfile.ext".
