## Activar los LVM desde un live

```
	# apt-get install lvm2
```

```
	# pvscan 
	  PV /dev/sda5   VG VGroup   lvm2 [407,16 GiB / 0    free]
	  Total: 1 [407,16 GiB] / in use: 1 [407,16 GiB] / in no VG: 0 [0   ]

	# vgscan 
	  Reading all physical volumes.  This may take a while...
	  Found volume group "VGroup" using metadata type lvm2

	# lvscan 
	  ACTIVE            '/dev/VGroup/vg-root' [13,97 GiB] inherit
	  ACTIVE            '/dev/VGroup/vg-swap' [2,04 GiB] inherit
	  ACTIVE            '/dev/VGroup/vg-home' [391,16 GiB] inherit
```

Si no esta activo cuando ejecute vgscan debe ejecutar.

```
	# vgchange -a y
	  3 logical volume(s) in volume group "VGroup" now active

```

## Verificar un volumen con fsck

```
	$vgchange --ignorelockingfailure -ay
	$lvscan --ignorelockingfailure
	$fsck -y /dev/VolumeGroup/LVname

```

Forzara chequear los bloques malos y automaticamente repararlos. Si luego sigue teniendo problemas es motivado ya a fallas irreparables del HDD.

```
	fsck -pvcf/dev/VGroup/vg-home
