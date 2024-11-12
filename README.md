<p align="center"><img src="./app/assets/images/SealCircle.png" width="150px" height="150px" alt="aventium softworks"></p>

<h1 align="center">Helios Launcher</h1>

<em><h5 align="center">(anteriormente Electron Launcher)</h5></em>

[<p align="center"><img src="https://img.shields.io/github/actions/workflow/status/dscalzi/HeliosLauncher/build.yml?branch=master&style=for-the-badge" alt="gh actions">](https://github.com/dscalzi/HeliosLauncher/actions) [<img src="https://img.shields.io/github/downloads/dscalzi/HeliosLauncher/total.svg?style=for-the-badge" alt="downloads">](https://github.com/dscalzi/HeliosLauncher/releases) <img src="https://forthebadge.com/images/badges/winter-is-coming.svg"  height="28px" alt="winter-is-coming"></p>

<p align="center">Entre em servidores modificados sem se preocupar em instalar Java, Forge ou outros mods. Nós cuidamos disso para você.</p>

![Captura de tela 1](https://i.imgur.com/6o7SmH6.png)
![Captura de tela 2](https://i.imgur.com/x3B34n1.png)

## Funcionalidades

* 🔒 Gerenciamento completo de contas.
  * Adicione várias contas e troque entre elas facilmente.
  * Suporte total para autenticação Microsoft (OAuth 2.0) + Mojang (Yggdrasil).
  * As credenciais nunca são armazenadas e são transmitidas diretamente para a Mojang.
* 📂 Gerenciamento eficiente de ativos.
  * Receba atualizações do cliente assim que as lançarmos.
  * Os arquivos são validados antes do lançamento. Arquivos corrompidos ou incorretos serão baixados novamente.
* ☕ **Validação automática de Java.**
  * Se você tiver uma versão incompatível do Java instalada, instalaremos a correta *para você*.
  * Você não precisa ter Java instalado para executar o launcher.
* 📰 Feed de notícias integrado nativamente ao launcher.
* ⚙️ Gerenciamento intuitivo de configurações, incluindo um painel de controle de Java.
* Suporta todos os nossos servidores.
  * Altere entre as configurações dos servidores com facilidade.
  * Veja o número de jogadores do servidor selecionado.
* Atualizações automáticas. Isso mesmo, o launcher se atualiza.
* Veja o status dos serviços da Mojang.

Esta não é uma lista exaustiva. Baixe e instale o launcher para explorar tudo o que ele pode fazer!

#### Precisa de Ajuda? [Confira o wiki.][wiki]

#### Gostou do projeto? Deixe uma ⭐ estrela no repositório!

## Downloads

Você pode baixar em [GitHub Releases](https://github.com/dscalzi/HeliosLauncher/releases)

#### Última Versão

[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases/latest)

#### Última Pré-Lançamento
[![](https://img.shields.io/github/release/dscalzi/HeliosLauncher/all.svg?style=flat-square)](https://github.com/dscalzi/HeliosLauncher/releases)

**Plataformas Suportadas**

Se você baixar na aba [Releases](https://github.com/dscalzi/HeliosLauncher/releases), selecione o instalador para o seu sistema.

| Plataforma | Arquivo |
| -------- | ---- |
| Windows x64 | `Helios-Launcher-setup-VERSION.exe` |
| macOS x64 | `Helios-Launcher-setup-VERSION-x64.dmg` |
| macOS arm64 | `Helios-Launcher-setup-VERSION-arm64.dmg` |
| Linux x64 | `Helios-Launcher-setup-VERSION.AppImage` |

## Console

Para abrir o console, use a combinação de teclas a seguir.

```console
ctrl + shift + i
```

Certifique-se de que a aba do console está selecionada. Não cole nada no console a menos que tenha 100% de certeza do que irá fazer. Colar algo incorreto pode expor informações sensíveis.

#### Exportar Saída para um Arquivo

Se você quiser exportar a saída do console, basta clicar com o botão direito em qualquer lugar do console e clicar em **Salvar como..**

![exemplo do console](https://i.imgur.com/T5e73jP.png)

## Desenvolvimento

Esta seção detalha a configuração de um ambiente de desenvolvimento básico.

### Começando

**Requisitos do Sistema**

* [Node.js][nodejs] v20

---

**Clonar e Instalar Dependências**

```console
> git clone https://github.com/dscalzi/HeliosLauncher.git
> cd HeliosLauncher
> npm install
```

---

**Aplicativo de lançamento**

```console
> npm start
```

---

**Instaladores de construção**

Para construir para sua plataforma atual.

```console
> npm run dist
```

Crie para uma plataforma específica.

| Platform    | Command              |
| ----------- | -------------------- |
| Windows x64 | `npm run dist:win`   |
| macOS       | `npm run dist:mac`   |
| Linux x64   | `npm run dist:linux` |

Compilações para macOS podem não funcionar no Windows/Linux e vice-versa.

---

### Visual Studio Code

Todo o desenvolvimento do iniciador deve ser feito usando [Visual Studio Code][vscode].

Paste the following into `.vscode/launch.json`

```JSON
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug Main Process",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceFolder}",
      "program": "${workspaceFolder}/node_modules/electron/cli.js",
      "args" : ["."],
      "outputCapture": "std"
    },
    {
      "name": "Debug Renderer Process",
      "type": "chrome",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceFolder}/node_modules/.bin/electron.cmd"
      },
      "runtimeArgs": [
        "${workspaceFolder}/.",
        "--remote-debugging-port=9222"
      ],
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

Isso adiciona duas configurações de depuração.

#### Depurar processo principal

Isso permite que você depure o [processo principal][processo principal] do Electron. Você pode depurar scripts no [processo de renderização][processo de renderização] abrindo a janela DevTools.

#### Depurar processo de renderização

Isso permite que você depure o [processo de renderização][processo de renderização] do Electron. Isso requer que você instale a extensão [Debugger for Chrome][chromedebugger].

Observe que você **não pode** abrir a janela DevTools enquanto estiver usando esta configuração de depuração. O Chromium permite apenas um depurador, abrir outro travará o programa.

---

### Observação sobre uso de terceiros

Por favor, dê crédito ao autor original e forneça um link para a fonte original. Este é um software livre, por favor, faça pelo menos isso.

Para obter instruções sobre como configurar a Autenticação da Microsoft, consulte https://github.com/dscalzi/HeliosLauncher/blob/master/docs/MicrosoftAuth.md.

---

## Recursos

* [Wiki][wiki]
* [Nebula (Create Distribution.json)][nebula]
* [v2 Rewrite Branch (Inactive)][v2branch]

A melhor maneira de entrar em contato com os desenvolvedores é no Discord.

[![discord](https://discordapp.com/api/guilds/211524927831015424/embed.png?style=banner3)][discord]

---

### Vejo você no jogo.

[nodejs]: https://nodejs.org/en/ 'Node.js'
[vscode]: https://code.visualstudio.com/ 'Visual Studio Code'
[mainprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Main Process'
[rendererprocess]: https://electronjs.org/docs/tutorial/application-architecture#main-and-renderer-processes 'Renderer Process'
[chromedebugger]: https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome 'Debugger for Chrome'
[discord]: https://discord.gg/zNWUXdt 'Discord'
[wiki]: https://github.com/dscalzi/HeliosLauncher/wiki 'wiki'
[nebula]: https://github.com/dscalzi/Nebula 'dscalzi/Nebula'
[v2branch]: https://github.com/dscalzi/HeliosLauncher/tree/ts-refactor 'v2 branch'
