Arch Linux
========

### Setup
1.  Install Arch Linux
    * [linuxveda tutorial](http://www.linuxveda.com/2014/06/07/arch-linux-tutorial)
    * [Archlinux wiki tutorial](https://wiki.archlinux.org/index.php/Installation_guide)

    ```sh
    # 인터넷 연결
    wifi-menu

    # 디스크 파티셔닝
    cfdisk /dev/sda

    # 파티션 포맷
    mkfs.ext4 /dev/sda1

    # 파티션 마운트
    mount /dev/sda1 /mnt

    # 미러 우선순위 변경
    vim /etc/pacman.d/mirrorlist

    # Install Archlinux
    pacstrap /mnt base
    genfstab -p /mnt >> /mnt/etc/fstab
    arch-chroot /mnt

    # hostname (https://wiki.archlinux.org/index.php/Network_configuration#Set_the_hostname)
    echo 'rilakkuma' > /etc/hostname

    # Timezone
    ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

    # Locale
    nano /etc/locale.gen
    locale-gen
    echo LANG=en_US.UTF-8 > /etc/locale.conf
    export LANG=en_US.UTF-8

    # Grub
    pacman -S grub
    grub-install --recheck /dev/sda
    grub-mkconfig -o /boot/grub/grub.cfg

    # New user
    useradd -m -G wheel -s /bin/bash simnalamburt
    passwd simnalamburt
    passwd root -dl
    pacman -S sudo
    EDITOR=nano visudo # 특정 라인 주석해제

    # Gnome desktop environment
    pacman -S gnome xf86-input-synaptics
    systemctl enable gdm
    systemctl enable NetworkManager

    exit
    umount -R /mnt
    ```

1.  Grub 대기시간 줄이기

    ```
    # /etc/default/grub
    GRUB_TIMEOUT=1
    ```
    ```sh
    grub-mkconfig -o /boot/grub/grub.cfg
    ```

1.  Clone [dotfiles](../README.md), symlink those to `/root`
1.  [Configure `ssh`](https://wiki.archlinux.org/index.php/Secure_Shell)

    ```sh
    sudo systemctl start sshd
    sudo systemctl enable sshd
    ```
    ```
    # /etc/ssh/sshd_config
    PermitRootLogin no
    PasswordAuthentication no
    PrintLastLog no
    ```

1.  [Install Yaourt](https://archlinux.fr/yaourt-en)

1.  *(optional)* [Disable lid sleep](http://unix.stackexchange.com/a/52645)

    ```
    # /etc/systemd/login.conf
    HandlePowerKey=ignore
    HandleSuspendKey=ignore
    HandleHibernateKey=ignore
    HandleLidSwitch=ignore
    ```
    ```sh
    sudo systemctl restart systemd-logind
    ```

### `pacman`
- base, grub, sudo, gnome, xf86-input-synaptics
- dialog, wpa_supplicant *(for wifi-menu)*
- openssh, wget, lshw, htop
- git, vim, zsh, tmux, mosh
- chromium *(remove epiphany)*
- gnome-tweak-tool, ibus-hangul, adobe-source-han-sans-otc-fonts

### `yaourt`
- the_platinum_searcher, fasd
- gtk-theme-arc-git, numix-circle-icon-theme-git