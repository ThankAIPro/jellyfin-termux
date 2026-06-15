# Instale o Jellyfin no Termux [pelo Proot]
Este guia mostra dois métodos para instalar o Jellyfin no Termux

Observação: testado apenas em aarch64/arm64

Nota: Não estou mais atualizando este guia, pois agora você pode instalar o Jellyfin diretamente no Termux. Basta instalar o pacote `jellyfin-server` no Termux. No entanto, muitos usuários tiveram problemas com o dotnet da Microslop e resolvi deixar esse aqui mesmo. 

Esses passos são os mesmos para ambos os métodos:

1. Atualize o repositório
```
pkg update
```

2. Instale o proot-distro e o ffmpeg (o ffmpeg só é necessário no Método 2).
```
pkg install proot-distro ffmpeg -y
```

3. Instale o Ubuntu e faça login.
```
proot-distro install ubuntu
proot-distro login ubuntu
```

4. Atualize e faça o upgrade dos pacotes no Ubuntu.
```
apt update && apt upgrade -y
```

5. .NET 7.0 [solução alternativa](https://github.com/dotnet/runtime/issues/85556):
* Use o nano (ou o editor de sua preferência) para criar um arquivo em `/etc/profile.d`.
```
nano /etc/profile.d/02-dotnet-fix.sh
```
* Cole o seguinte para definir o valor de `DOTNET_GCHeapHardLimit` para `1C0000000` (Talvez seja necessário diminuir o valor para que funcione):
```
export DOTNET_GCHeapHardLimit=1C0000000
```
* Salve e saia do nano pressionando `CTRL + x`, depois `y` e, em seguida, `enter`.
* Torne-o executável.
```
chmod +x /etc/profile.d/02-dotnet-fix.sh
```
* Saia da sua conta e entre novamente no Proot.

Método 1:

6. Instale sudo curl e gnupg
```
apt install sudo curl gnupg -y
```

7. Baixe e verifique o script e, em seguida, execute-o em seu sistema (requer curl e sha256sum):
```
curl -s https://repo.jellyfin.org/install-debuntu.sh -O && \
curl -s https://repo.jellyfin.org/install-debuntu.sh.sha256sum -O && \
sha256sum -c install-debuntu.sh.sha256sum
```
Em seguida, execute-o com:
```
sudo bash install-debuntu.sh
```

8. Crie um link simbólico para o cliente web Jellyfin (pois ele está na pasta errada).
```
ln -s /usr/share/jellyfin/web /usr/lib/jellyfin/bin/jellyfin-web
```

9. Execute o Jellyfin
```
jellyfin
```
* Observação: se você receber erros relacionados à rede, adicione o parâmetro `--nonetchange` ao Jellyfin.

10. Aguarde alguns minutos para que a inicialização seja concluída e, em seguida, acesse http://192.168.x.x:8096 para configurar o Jellyfin.


Método 2: Opcional

6. Instale os pacotes necessários (ignore o wget se você o tiver instalado no Termux; substitua também `74` pela versão mais recente do libicu).
```
apt install wget libicu74 libfontconfig1 ca-certificates -y
```

7. Crie uma nova pasta em /opt com o nome jellyfin e acesse-a pelo comando cd.
```
mkdir /opt/jellyfin
cd /opt/jellyfin
```

8. Baixe a versão genérica mais recente do Linux para sua arquitetura em [here](https://jellyfin.org/downloads/linux) com `wget` (Certifique-se de baixar a arquitetura correta para o seu dispositivo.)
```
wget https://repo.jellyfin.org/files/server/linux/latest-stable/arm64/jellyfin_10.10.6-arm64.tar.gz
```

9. Extraia-o com tar
```
tar xvzf jellyfin_10.10.6-arm64.tar.gz
```

10. Crie quatro subdiretórios para os dados do Jellyfin.
```
mkdir data cache config log
```
11. Use o nano para criar um script para executar o Jellyfin.
```
nano jellyfin.sh
```
* Cole o seguinte:
```
#!/bin/bash
JELLYFINDIR="/opt/jellyfin"

$JELLYFINDIR/jellyfin/jellyfin \
 -d $JELLYFINDIR/data \
 -C $JELLYFINDIR/cache \
 -c $JELLYFINDIR/config \
 -l $JELLYFINDIR/log \
 --ffmpeg /data/data/com.termux/files/usr/bin/ffmpeg
```
* Observação: se você receber erros relacionados à rede, adicione o parâmetro `--nonetchange` ao Jellyfin no arquivo `jellyfin.sh`.
* Salve e saia do nano pressionando `CTRL + x`, depois `y` e, em seguida, `enter`.

12. Torne-o executável. 
```
chmod +x jellyfin.sh
```

13. Execute-o
```
/opt/jellyfin/jellyfin.sh
```

14. Aguarde alguns minutos para que a inicialização seja concluída e, em seguida, acesse http://192.168.x.x:8096 para configurar o Jellyfin.


Obrigado a @sdshan8 pela aula
