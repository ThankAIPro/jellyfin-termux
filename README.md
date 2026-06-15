📱🎬 Jellyfin no Android Antigo com Termux
Transforme um celular velho em um servidor de filmes, séries e músicas

📖 Sobre o Projeto

Este projeto demonstra como instalar e configurar o Jellyfin utilizando o Termux em um smartphone Android antigo, transformando-o em um servidor multimídia de baixo custo para armazenar e transmitir filmes, séries, músicas e outros conteúdos pela rede local.

A proposta é reaproveitar dispositivos antigos que normalmente ficariam esquecidos em uma gaveta, criando uma solução simples, econômica e eficiente para uso doméstico.

🚀 O Que Você Vai Aprender

✅ Instalar o Termux corretamente
✅ Atualizar os pacotes do sistema
✅ Configurar o ambiente Linux dentro do Android
✅ Instalar o Jellyfin
✅ Configurar bibliotecas de mídia
✅ Acessar o servidor pela rede local
✅ Utilizar um celular antigo como mini servidor doméstico

📋 Requisitos

Hardware
Smartphone Android antigo
Pelo menos 2 GB de RAM (recomendado)
8 GB ou mais de armazenamento disponível
Conexão Wi-Fi estável
Carregador conectado durante o uso

Software
Android 7 ou superior
Termux atualizado
Navegador Web
📦 Instalação do Termux

Baixe a versão mais recente do Termux:

F-Droid (recomendado)
GitHub Releases

Após instalar:
```
pkg update && pkg upgrade -y
```

Instale os pacotes básicos:
```
pkg install git wget curl nano -y
```

Conceda acesso ao armazenamento:
```
termux-setup-storage
```
⚙️ Instalação do Ambiente Linux

Instale o Proot-Distro:
```
pkg install proot-distro -y
```

Instale o Ubuntu:
```
proot-distro install ubuntu
```

Entre no Ubuntu:
```
proot-distro login ubuntu
```

Atualize o sistema:
```
apt update && apt upgrade -y
```

🎥 Instalação do Jellyfin

Siga os passos apresentados no tutorial original para instalar o Jellyfin dentro do ambiente Ubuntu.

Dependendo da versão utilizada, os comandos podem sofrer alterações.

📂 Organização das Mídias

Sugestão de estrutura:

Media/
├── Filmes/
├── Series/
├── Musicas/
├── Animes/
└── Documentarios/

🌐 Acessando o Servidor

Após iniciar o Jellyfin:
```
http://IP_DO_CELULAR:8096
```

Exemplo:

http://192.168.0.100:8096

Abra o endereço em qualquer dispositivo conectado à mesma rede.

🔋 Recomendações
Mantenha o aparelho conectado ao carregador.
Desative otimizações de bateria.
Utilize armazenamento externo para grandes bibliotecas.
Prefira conexão Wi-Fi de 5 GHz quando disponível.
Faça backups periódicos dos seus dados.

🎯 Vantagens
✔ Baixo custo
✔ Reaproveitamento de hardware antigo
✔ Consumo reduzido de energia
✔ Fácil manutenção
✔ Plataforma totalmente gratuita
✔ Sem mensalidades

📺 Vídeo Tutorial

O passo a passo completo está disponível no canal:

ThinkAI Pro

Inscreva-se para acompanhar novos projetos envolvendo:

Inteligência Artificial
Android
Linux
Termux
Automação
Servidores domésticos
Tecnologia e dispositivos móveis
🤝 Contribuindo

Contribuições são bem-vindas.

Você pode:

Reportar problemas
Sugerir melhorias
Corrigir documentação
Compartilhar adaptações para outros dispositivos

Faça um Fork do projeto e envie seu Pull Request.

📜 Licença

Este projeto é disponibilizado apenas para fins educacionais e de aprendizado.

Todos os direitos sobre o Jellyfin pertencem aos seus respectivos desenvolvedores.

⭐ Se este projeto foi útil para você, considere deixar uma estrela no repositório!
