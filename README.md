# TP

```
$: make warp7_defconfig
```

```
$: mkdir keys
$: openssl genpkey -algorithm RSA -out keys/ynov.key -pkeyopt rsa_keygen_bits:4096
$: openssl req -new -x509 -key keys/ynov.key -out keys/ynov.crt
```

```
$: tools/mkimage -f fitImage.its fitImage
$: cp arch/arm/dts/imx7s-warp.dtb pubkey.dtb
$: tools/mkimage -f fitImage.its -K pubkey.dtb -k keys -r fitImage
$: tools/fit_check_sign -f fitImage -k pubkey.dtb
$: dtc -I dtb -O dts -o pubkey_ynov.dts u-boot.dtb
$: make V=1 EXT_DTB=pubkey.dtb 

```

```
$: sudo cp fitImage /var/lib/tftpboot/fitImage_ynov
```
