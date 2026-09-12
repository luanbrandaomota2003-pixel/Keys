NAUVAMP3 ANDROID - NODE + WEBVIEW + PYTHON/YT-DLP + FFMPEG
============================================================

O projeto foi preparado para Android Studio.

ARQUITETURA
-----------
1. MainActivity copia assets/nodejs-project para filesDir/nodejs-project.
2. libnode.so inicia server.js dentro do próprio APK.
3. Chaquopy inicia Python 3.13 e inclui yt-dlp + yt-dlp-ejs.
4. MediaBridgeServer abre somente em 127.0.0.1:8765.
5. server.js usa essa ponte para pesquisar, obter preview e baixar áudio.
6. O yt-dlp baixa a melhor faixa de áudio.
7. FFmpegKit converte o arquivo para MP3.
8. O Node serve o MP3 em /musicas/... e o WebView abre http://127.0.0.1:3000.

COMPILAR
--------
1. Abra esta pasta no Android Studio.
2. Espere o Gradle Sync terminar. Internet é necessária na primeira compilação.
3. Instale pelo SDK Manager se solicitado:
   - Android SDK 35
   - NDK compatível com CMake
   - CMake 3.22.1
4. Build > Build APK(s).

O Gradle baixa automaticamente o libnode.so ARM64 na primeira compilação.
O Chaquopy baixa Python/yt-dlp durante o build.
O FFmpegKit é obtido via Maven.

ARQUITETURA SUPORTADA
---------------------
arm64-v8a

ROTAS PRINCIPAIS
----------------
http://127.0.0.1:3000/
http://127.0.0.1:3000/api
http://127.0.0.1:3000/api/musica/NOME_DA_MUSICA
http://127.0.0.1:3000/api/musicas

OBSERVAÇÃO SOBRE YOUTUBE
------------------------
O yt-dlp atual exige um runtime JavaScript externo (Deno, Node executável ou QuickJS)
para suporte COMPLETO aos desafios JavaScript do YouTube. Este projeto inclui Node como
biblioteca embutida para rodar o servidor, mas isso não cria automaticamente um executável
Node que o yt-dlp possa chamar como subprocesso. Em muitos vídeos o yt-dlp ainda consegue
resolver e baixar formatos; outros podem exigir a inclusão futura de um runtime JS externo
compatível com Android.

Não use o app para baixar ou redistribuir conteúdo sem autorização.
