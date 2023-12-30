---
layout: post
title:  "Seamless Linux disk encryption with systemd-measure"
date: 2023-12-29
categories: Tech
tags:
 - systemd-measure
 - secureboot
 - LUKS
 - TPM
 - TPM2
 - UKI
 - UEFI
 - ukify
---

I've been using Archlinux for a while. One painpoint for me is that there is no push-button end-to-end data protection solution like [Bitlocker](https://learn.microsoft.com/en-us/windows/security/operating-system-security/data-protection/bitlocker/) on Windows or [FileVault](https://support.apple.com/guide/mac-help/protect-data-on-your-mac-with-filevault-mh11785/mac) on MAC. I've used solutions like [LUKS2](https://wiki.archlinux.org/title/dm-crypt/System_configuration) with [TPM2](https://wiki.archlinux.org/title/Systemd-cryptenroll), but they are not as seamless as Bitlocker. I have to enter the password every time the kernel is updated since the TPM measurement updated.

Recently, I learned that `systemd-measure` is [introduced](https://lwn.net/Articles/913287/) in systemd from version 252. In short, it provides the ability to measure the PCR of a unified kernel image (UKI) before they are actually booted. I played around with it, and below is my config. Hopefully it works for you if you are using Archlinux.

## Environment before the setup
 - An LUKS2 encrypted root partition with `sd-encrpyt` hook, see [here](https://wiki.archlinux.org/title/dm-crypt/Encrypting_an_entire_system)
 - A properly configured secureboot PKI system. I personally use [sbctl](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#Assisted_process_with_sbctl)

## How it works

The `systemd-cryptenroll` allows to config a keyslot, which,  **ANY** PCR values signed by a specific pubkey can unlock the volume. The `systemd-measure` can measure the PCR values of a UKI, and the measurement is signed by the keypair and inserted into the UKI. Thus, the initrd can unlock the volume since a signature of the current PCR measurements is provided to the TPM to release the master key to the volume.

## Steps

1. Generate a keypair to sign the PCR measurement.  
```bash
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out /etc/systemd/tpm2-pcr-private-key.pem
openssl rsa -pubout -in /etc/systemd/tpm2-pcr-private-key.pem -out /etc/systemd/tpm2-pcr-public-key.pem
``` 
The path here `/etc/systemd/tpm2-pcr-private-key.pem` has specific meaning documented in the [man page](https://man.archlinux.org/man/crypttab.5.en)  
> If this option is not specified but it is attempted to unlock a LUKS2 volume with a signed TPM2 PCR enrollment a suitable signature file tpm2-pcr-signature.json is searched for in /etc/systemd/, /run/systemd/, /usr/lib/systemd/ (in this order).  

2. Install `systemd-ukify`  
```bash
pacman -S systemd-ukify
```
3. Draft a config file per the [man page](https://man.archlinux.org/man/ukify.1.en)
```conf
[UKI]
Linux=/boot/vmlinuz-linux
Initrd=/boot/intel-ucode.img /boot/initramfs-linux.img
Cmdline=@/etc/kernel/cmdline
OSRelease=@/etc/os-release
PCRBanks=sha256
SecureBootSigningTool=sbsign
SecureBootPrivateKey=/usr/share/secureboot/keys/db/db.key
SecureBootCertificate=/usr/share/secureboot/keys/db/db.pem
[PCRSignature:default]
PCRPrivateKey=/etc/systemd/tpm2-pcr-private-key.pem
PCRPublicKey=/etc/systemd/tpm2-pcr-public-key.pem
```
Please note that, I used `sbctl`'s db key for secureboot signature. I used the previously generated keypair for PCR measurement signature.
4. Run `ukify` to generate the UKI
```bash
ukify -c /etc/ukify.conf build --output /boot/EFI/Linux/ukify-linux.efi
```
Per man page of `ukify`, it will call the `systemd-measure`, precalculate the PCR values, and sign the measurement with the keypair. The signature is stored in `.pcrsig`. According to the man page of the `systemd-stub`:  
> A ".pcrsig" section with a set of cryptographic signatures for the expected TPM2 PCR
        values after the kernel has been booted, in JSON format. This is useful for 
        implementing TPM2 policies that bind disk encryption and similar to kernels that are
    signed by a specific key.  
The output file `/boot/EFI/Linux/ukify-linux.efi` is also deliberately chosen so that `systemd-boot` can automatically pick it up.

5. Create a new LUKS2 slot with the pubkey of the keypair
```bash
systemd-cryptenroll --tpm2-device=auto --tpm2-public-key=/etc/systemd/tpm2-pcr-public-key.pem \
/dev/disk/by-uuid/$DISKUUID
```
Now that the LUKS2 volume can be unlocked by any PCR measurement signed by the keypair. We already got the PCR measurement signed by the keypair in the UKI. Thus, the initrd can unlock the volume.

Please note, I did not create pacman hooks to recreate the UKI after Linux kernel or ucode updated, please do it yourself.

## Conclusion

In conclusion, implementing seamless Linux disk encryption with `systemd-measure` and related tools offers a robust solution for protecting your data. While the setup process involves several steps, the resulting configuration provides a secure and user-friendly experience.

By leveraging `systemd-cryptenroll` and `ukify`, we've established a system where the Unified Kernel Image's measurements, signed by a secure keypair, enable automatic unlocking of the LUKS2-encrypted volume. This approach reduces the need for manual intervention during kernel updates, enhancing the overall convenience of disk encryption on Arch Linux.

Remember to adapt the configurations to your specific environment and consider additional security measures, such as updating the UKI after kernel or microcode updates.

With these steps, you can enjoy the benefits of seamless Linux disk encryption, bringing us closer to the ease of use provided by similar solutions on other operating systems.

Happy encrypting!