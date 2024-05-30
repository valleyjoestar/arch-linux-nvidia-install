# arch-linux-nvidia-install

## 1.Adım

Öncelikle masaüstü ortamımıza giriş yapıyoruz. Eğer driverdan sebep masaüstüne erişemiyorsak tty modunda giriş yapıyoruz.

Sonrasında kullandığınız terminali açıp gerekli paketleri indiriniz.

 • **sudo pacman -S base-devel linux-headers**

(Kernel paketini kullandığınız kernele bağlı olarak indiriniz. Örneğin zen kernel için "sudo pacman -S linux-zen-headers" yazıp indirebilirsiniz.)

Sonrasında nvidia-dkms paketini indiriyoruz.

 • **sudo pacman -S nvidia-dkms** 

(Ekran kartınız eski ise kendinize uygun paketi bulunuz. Benim bu öğreticide kullandığım ekran kartı GTX 750ti)

## 2.Adım

GRUB Kullanıcıları için:

Bu paketler indikten sonra GRUB config dosyamızı düzenliyoruz. Kullandığınız metin düzenleyici uygulaması ile /etc/default/grub dosyasını açıyoruz.

(Ben bu öğreticide vim kullanırmış gibi konuşacağım.)

 • **sudo vim /etc/default/grub**

GRUB_CMDLINE_LINUX_DEFAULT dizisini bulup tırnak içindeki kısmın sonuna gelip "nvidia_drm.modeset=1" yazıyoruz. Esc tuşuna basıp, :wq yazıp, enter tuşuna basıyoruz.

Sonrasında terminale 

 • **sudo grub-mkconfig -o /boot/grub/grub.cfg**

Yazıyoruz.

(Bu işlem GRUB kullanıcıları içindir. systemd-boot kullanlar için ne yapmaları gerektiği hakkında bilgim yok. İnternette yabancı kaynaklardan rahatlıkla bulabilirsiniz.)

## 3.Adım

Sonrasında mkinitcpio configimizi düzenliyoruz.

 • **sudo vim /etc/mkinitcpio.conf**

MODULES kısmının parantez içine "nvidia nvidia_modeset nvidia_uvm nvidia_drm" yazıyoruz.

ESC tuşuna basıp :wq yazıp enter tuşuna basıyoruz.

Sonrasında terminale 

 • **sudo mkinitcpio -P**

Yazıyoruz ve hata olup olmadığına bakıyoruz. Eğer hata var ise hatayı düzeltip tekrar deneyiniz.

## 4.Adım

nvidia-utils paketlerini de indirmekte fayda var. nvidia-settings de isteğinize bağlı. Ben hiç kullanmadım. Bunları indirmek için de

 • **sudo pacman -S nvidia-utils lib32-nvidia-utils nvidia-settings** 

Yazıp indiriniz.

## SON

Ve bu kadardı, artık driveriniz kurulmuş durumda! Sisteminizi yeniden başlatıp giriş yapabilirsiniz. 
