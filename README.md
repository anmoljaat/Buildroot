# Buildroot
Do diretório home, acessar a pasta do BuildRoot: buildroot

Executar o comando make menuconfig

Habilitar Wchar (necessário para o python)

    Toolchain → Wchar (*)

Habilitar o suporte a linguagem python na distribuição:

    Interpreter languages and scripting → python(*)

Salvar alterações e sair do menuconfig

Abra a pasta buildroot/custom-scrpits
edite o arquivo S41network-config
Nas linhas abaixo altere "150.162.221.158" pelo ip da maquina host

        /sbin/route add -host 150.162.221.158 dev eth0
        /sbin/route add default gw 150.162.221.158

No diretório buildroot, executar os comandos:


make clean e make para compilar a nova distribuição.

rode a distribuição
 sudo qemu-system-i386 --device e1000,netdev=eth0,mac=aa:bb:cc:dd:ee:ff   --netdev tap,id=eth0,script=custom-scripts/qemu-ifup   --kernel output/images/bzImage   --hda output/images/rootfs.ext2 --nographic   --append "console=ttyS0 root=/dev/sda" 

no navegador da maquina host digite: http://192.168.1.10:8080/
O sitema deve estar funcionando
