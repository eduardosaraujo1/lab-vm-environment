# Especificações de Virtualização

Esse documento especifica decisões tomadas para o ambiente de virtualização em que a máquina virtual será executada. Vale ressaltar que o projeto foi testado sob essas condições, mas é possível ajustar certos parâmetros conforme adequado para cada ambiente.

> Observação: Embora a máquina virtual seja projetada e testada em um host Windows com VirtualBox, o disco .vdi foi gerado em um host Linux utilizando a stack de virtualização KVM/QEMU/Libvirt. Consequentemente, pode-se esperar que o projeto também funcionará sob essas condições.

## Especificações Gerais
CPU, RAM, Firmware UEFI, GPU Acceleration, X video memory, Network NAT, VirtualBox Guest Utils (?), Graphics controller -> VMSVGA

## Disco Virtual Imutável
(falar de como o disco é .vdi, imutável e portanto uma alteração não será permanente, credenciais serão apagadas em reboot, etc)

## USB Passthrough
(falar que suporte para passar dispositivos externos como pendrives e celulares via USB foi testado em ambientes com USB 3.0)

## Pastas Compartilhadas

(falar das decisões tomadas para lidar com facilidade de transferência de arquivos entre hospedeiro e 

---

# Scratchpad
TODO: configuração da VM:
disco imutável
USB 3 passthrough
pasta compartilhada 
- Previnir localizada em AppData e atalho em Documents/ com permissões funcionais
Guest OS -> Debian 13 64-bit
Firmware -> BIOS or UEFI
vCPU -> 4 recommended
RAM -> 8 GB
Disk -> VDI, dynamic, X GB maximum
Network -> NAT
Network adapter -> Default/virtio-compatible
Audio -> Enabled/disabled
Video memory -> Decide/test
3D acceleration -> Enabled/tested
USB -> USB 3.x
Shared folders -> Enabled
Guest Additions -> Installed
Clipboard -> Disabled
Drag & Drop -> Disabled
Mouse integration -> Enabled
Time synchronization -> Enabled
VM encryption -> Decide whether necessary
Boot order -> HDD → optical
Host key -> Default/custom
Virtual disk location -> Defined
Shared folder location -> Defined
