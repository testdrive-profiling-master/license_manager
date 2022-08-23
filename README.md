# license_manager
License Manager Sub-Package for TestDrive

```text
> Testdrive_LM
- TestDrive Profiling Master License Manager. (SEED 128bit + SHA256) - (build :Mar 29 2022)

Usage : testdrive_lm [options] OP ...
        [options]
            -f flag_file_name  : specify custom flag file name.
            -k key_file_name   : specify custom key file name.
            -t tag_string      : specify custom tag string.
        OP
            register HASH256_key
                : register key on this system.
            export public_key
                : export public key file('.TestDrive.public_key').
            hash public_key (private_string)
                : Get Hash Key.
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
> TestDrive_LM encrypt yourfile.ext
```
(This operation can be executed only when the ".TestDrive.public_key" file exists in the current folder or its parent folder.)   
You can see the ".TestDrive.ext.encrypted" file in the same working folder.


## 3. Generate hash_key (Client side)
```text
> TestDrive_LM check
Your public key : /.TestDrive.public_key
*E: No license key. Contact your license manager with following your private key code.

    - E647742AB1C8479A02A4CBF1C5D841E5F48543E10ECBC002FB3A3603610B8F8A32179D36C2E55EF8AD30B54B3964DA54FAD4CB39E3CA971D4749678A3CC1CF3F
```
The client side has no license rights to decrypt, and each client PC has a different private key code.   
The client needs to know the hash_key for the private key to decrypt the files.   

## 4. Decrypt your files
