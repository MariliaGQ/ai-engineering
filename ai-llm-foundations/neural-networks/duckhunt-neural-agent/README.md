# DUCK HUNT JS v3.0

[Jogar o jogo](https://duckhuntjs.com)

Esta é uma implementação de DuckHunt em Javascript e HTML5. Ela usa o mecanismo de renderização PixiJS, Animações Green Sock, Howler e Promessas Bluebird.

## Renderização
Este jogo suporta renderização WebGL e Canvas através do mecanismo de renderização PixiJS.

## Áudio
Este jogo tentará usar a WebAudioAPI e retornará para HTML5 Audio se necessário. O áudio é carregado e controlado via HowlerJS.

## Animação
As animações deste jogo são uma combinação de MovieClips do PixiJS construídos a partir de imagens de sprite e tweens. Como o PixiJS não fornece uma API de tweening, Green Sock foi utilizado.

## Lógica do Jogo
O fluxo deste jogo é gerenciado usando Javascript. Os principais blocos de lógica de negócios são implementados como classes ES6 que são transpiladas para ES5 usando Babel.

## Trabalhando Com Este Repositório

 - Você deve ter [nodejs](https://nodejs.org/) instalado.
 - Clone o repositório em um diretório de sua escolha
 - `cd` para esse diretório e execute `npm install`
 - Use `npm start` para iniciar um servidor web local que disponibilizará o site em http://localhost:8080/. Erros de origem cruzada impedem que este projeto seja acessado no navegador com o protocolo `file://`. Isso também acionará compilações automáticas e recarregamentos da página quando mudanças forem detectadas no diretório `src`.
 - Se você deseja compilar manualmente o código da aplicação, execute `npm run build`
 
## Trabalhando Com Áudio e Ativos Visuais
Este repositório é fornecido com arquivos dist confirmados para facilitar o trabalho dos desenvolvedores. Se você realmente quer fazer algumas modificações legais e mudar a aparência e som deste jogo, você precisará trabalhar com sprites de áudio e imagem. As seguintes tarefas tornam isso possível: 

 - Para reconstruir ativos de áudio, use `npm run audio` (há uma dependência obrigatória de [ffmpeg](https://ffmpeg.org/download.html) para executar esta tarefa)
 - Para reconstruir ativos de imagem, use `npm run images` (há uma dependência obrigatória de [texturepacker](https://www.codeandweb.com/texturepacker/download) para executar esta tarefa)


