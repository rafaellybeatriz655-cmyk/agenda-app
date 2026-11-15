# Agenda — app de verdade para Android (com notificações)

Este projeto transforma a Agenda em um app Android (arquivo .apk) com notificações do próprio celular.
Os avisos são agendados no aparelho: tocam com o app fechado e sem internet.

## Caminho A — sem instalar nada no computador (recomendado)
O GitHub monta o app para você, de graça.
1. Crie uma conta grátis em github.com e depois um repositório novo chamado `agenda-app` (público ou privado).
2. Envie os arquivos desta pasta: no repositório, "Add file" > "Upload files" e arraste tudo (as pastas www e assets e os arquivos capacitor.config.json, package.json).
3. Crie o arquivo do montador: "Add file" > "Create new file", digite o nome `.github/workflows/android.yml` (as barras criam as pastas) e cole o conteúdo do arquivo `android.yml` desta pasta. Clique em "Commit changes".
4. Abra a aba "Actions", escolha "Build Android APK" e clique em "Run workflow". Espere uns 10 minutos até aparecer um ✅ verde.
5. Abra a execução concluída e, no fim da página, baixe `agenda-apk` (é um .zip com o arquivo app-debug.apk dentro).
6. Passe o .apk para o celular (e-mail, Drive ou cabo), abra e permita "instalar de fontes desconhecidas" quando o Android pedir.

## Caminho B — com Android Studio
1. Instale o Node.js (nodejs.org) e o Android Studio (developer.android.com/studio).
2. Na pasta do projeto, rode:
   npm install @capacitor/core @capacitor/cli @capacitor/android @capacitor/local-notifications @capacitor/assets
   npx cap add android
   npx capacitor-assets generate --android
   npx cap sync android
3. Abra a pasta `android` no Android Studio, conecte o celular (depuração USB ligada) e clique em Run ▶.
4. No arquivo android/app/src/main/AndroidManifest.xml, antes de `<application`, confirme estas linhas:
   <uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
   <uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />
   <uses-permission android:name="android.permission.USE_EXACT_ALARM" />
   <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## Ligar as notificações (importante)
1. Abra o app > Mais > Ajustes > Avisos > "Ativar notificações". Permita as notificações e, se o Android pedir, os "alarmes e lembretes".
2. Toque em "Testar (5 s)" e feche o app. O aviso deve chegar em 5 segundos.
3. Se os avisos atrasarem: Configurações do Android > Apps > Agenda > Bateria > "Sem restrições" (em Xiaomi, Samsung e Motorola essa etapa costuma ser necessária).
O app agenda blocos (inclusive repetidos), tarefas (começar, véspera e dia do prazo), o bom dia e o fechamento do dia. Ele reagenda sozinho quando você muda algo.

## Atualizar o app
Troque `www/index.html` pelo arquivo novo e rode o montador de novo (Caminho A, passo 4). Os dados ficam no aparelho e continuam ao atualizar por cima. Faça backup em Mais > Ajustes de vez em quando.

## iPhone
É possível, mas exige um Mac com Xcode. Com Apple ID grátis o app expira a cada 7 dias; para uso permanente ou TestFlight é preciso a conta de desenvolvedor da Apple (US$ 99 por ano).

## Observações
- O .apk gerado é de teste ("debug"), ótimo para uso pessoal. Publicar na Google Play exige assinatura e uma conta de desenvolvedor (US$ 25, uma vez).
- Os arquivos desta pasta não foram testados num celular real.
