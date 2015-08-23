Przekierowanie karty graficznej do wirtualnej maszyny.

Linijka w /etc/default/grub
pci_stub.ids=1002:6658,1002:aac0 iommu=pt



find /sys/kernel/iommu_groups/ -type l
/sys/kernel/iommu_groups/0/devices/0000:00:00.0
/sys/kernel/iommu_groups/1/devices/0000:00:01.0
/sys/kernel/iommu_groups/1/devices/0000:00:01.1
/sys/kernel/iommu_groups/2/devices/0000:00:02.0
/sys/kernel/iommu_groups/2/devices/0000:01:00.0
/sys/kernel/iommu_groups/2/devices/0000:01:00.1
/sys/kernel/iommu_groups/3/devices/0000:00:10.0
/sys/kernel/iommu_groups/3/devices/0000:00:10.1
/sys/kernel/iommu_groups/4/devices/0000:00:11.0
/sys/kernel/iommu_groups/5/devices/0000:00:12.0
/sys/kernel/iommu_groups/5/devices/0000:00:12.2
/sys/kernel/iommu_groups/6/devices/0000:00:13.0
/sys/kernel/iommu_groups/6/devices/0000:00:13.2
/sys/kernel/iommu_groups/7/devices/0000:00:14.0
/sys/kernel/iommu_groups/7/devices/0000:00:14.2
/sys/kernel/iommu_groups/7/devices/0000:00:14.3
/sys/kernel/iommu_groups/8/devices/0000:00:14.4
/sys/kernel/iommu_groups/9/devices/0000:00:15.0
/sys/kernel/iommu_groups/9/devices/0000:00:15.1
/sys/kernel/iommu_groups/9/devices/0000:00:15.2
/sys/kernel/iommu_groups/9/devices/0000:04:00.0
/sys/kernel/iommu_groups/9/devices/0000:05:00.0
/sys/kernel/iommu_groups/10/devices/0000:00:18.0
/sys/kernel/iommu_groups/10/devices/0000:00:18.1
/sys/kernel/iommu_groups/10/devices/0000:00:18.2
/sys/kernel/iommu_groups/10/devices/0000:00:18.3
/sys/kernel/iommu_groups/10/devices/0000:00:18.4
/sys/kernel/iommu_groups/10/devices/0000:00:18.5


Jak widać GPU + audio trzeba przekierować.

01:00.0 VGA compatible controller [0300]: Advanced Micro Devices, Inc. [AMD/ATI] Bonaire XTX [Radeon R7 260X] [1002:6658] (prog-if 00 [VGA controller])
	Subsystem: ASUSTeK Computer Inc. Device [1043:04cb]
	Flags: bus master, fast devsel, latency 0, IRQ 255
	Memory at c0000000 (64-bit, prefetchable) [size=256M]
	Memory at d0000000 (64-bit, prefetchable) [size=8M]
	I/O ports at e000 [size=256]
	Memory at fea00000 (32-bit, non-prefetchable) [size=256K]
	Expansion ROM at fea40000 [disabled] [size=128K]
	Capabilities: <access denied>
	Kernel driver in use: pci-stub

01:00.1 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] Device [1002:aac0]
	Subsystem: ASUSTeK Computer Inc. Device [1043:aac0]
	Flags: fast devsel, IRQ 255
	Memory at fea60000 (64-bit, non-prefetchable) [disabled] [size=16K]
	Capabilities: <access denied>
	Kernel driver in use: pci-stub

Nie można przekierować karty jeżeli jest inne urządzenie w tej samej grupie (oprócz root portów). Karta musi być "przejęta" przez pci-stub. Karta graficzna którą chcemy przekierować nie może być używana przez system. Maszyna wirtualna odpalana przez virt-manager-a.

Pozostaje problem dźwięku. Można dodać kartę na USB i przekierować dźwięk z karty do line-in na dźwiękówce na płycie głównej. W pulse-audio dodać loop.
Klawiatura i myszka można użyć synergy.


Hardware:
Płyta głowna F2A85-V PRO
CPU AMD A10-5800K
Software:
Xubuntu 15.04
3.19.0-21-generic
virt-manager                          1:1.0.1-5ubuntu1
libvirt-bin                           1.2.12-0ubuntu13
libvirt0                              1.2.12-0ubuntu13

Przydatne linki:
http://vfio.blogspot.com/

