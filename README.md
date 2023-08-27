# Finalized, working, modified copy of clover for my specific use case

## ABOUT

Customized version of Clover Bootloader (<https://github.com/CloverHackyColor/CloverBootloader> Copyright (c) 2019, CloverHackyColour) to load UEFI NVMe drivers and boot into proxmox loaded on a WD Blue NVMe PCIe SSD in a pcie-m.2 adapter on a Dell Poweredge R720 that does not natively support newer gen M.2 Drives. You can absolutely replace an SD card with a USB or extra hard drive or anything bootable, I just used an SD card because it was already integrated for such a purpose in my server.

## HOW-TO

## My steps were as followed, using an SD card loaded into the vFlash sd port and proxmox already installed on the nvme drive

### 1. flash original ISO as a bootable ISO to the SD card, and boot into clover

### 2. Write bootlog in the clover menu, and powerdown

### 3. Mount SD card in Windows, and copy the boot-log (/EFI/CLOVER/misc/preboot.log), along with the config (/EFI/CLOVER/config.plist) to a convenient place

### 4. Extract an unmodified clover ISO using the tool of your choice (I used Anyburn) BUT ensure you have a folder labelled '[BOOT]' as this contains the boot info that makes it bootable

### 5. Clone the 3 folders you got from dumping the unmodified ISO to another location for modification (These should be folders named '[BOOT]', 'EFI', and 'USER')

### 6. Inside the bootlog , there should be a few locations that identifies the device ID and path of all available boot options, and identifies the drivers that were loaded

### 7. Using these, move the drivers that are needed from /EFI/CLOVER/drivers/off to /EFI/CLOVER/drivers/UEFI and /EFI/CLOVER/drivers/BIOS inside the cloned directory of iso files

### 8. Copy the config.plist you retrieved earlier to the cloned set of clover directories in /EFI/CLOVER/ and edit, adding the volume ID and intended bootloader location, as well as changing other options as you see fit

### 9. Using the tool of your choice (again, Anyburn was what I used), add '/EFI' and '/usr' to a new iso archive, and choose '[BOOT]' as your bootinfo

### 10. Burn the iso you just made as bootable to your internal drive, or upload to vFlash as a boot option (what i did)

### 11. ensure a working boot, and you are done
