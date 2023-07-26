# ATW - Atalho Temas Windows

Ficheiro .bat e instruções sobre como trocar rapidamente os temas no Windows

## Instruções
1. Criar um ficheiro .theme através das definições do Windows ou Painel de Controlo;
2. Os temas são guardados na pasta Themes que pode ser acedida em  **%localappdata%\Microsoft\Windows\Themes** ou **Utilizador\AppData\Local\Microsoft\Windows\Themes**;
3. Substituir no ficheiro .bat [localização do ficheiro .theme] pela localização do ficheiro
4. Renomear o ficheiro .bat para o nome do tema
5. Criar um atalho para o ficheiro .bat
6. Colocar o atalho dentro da pasta **%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs** para aparecer no Menu Iniciar.

## Funcionamento do ficheiro bat
Primeiro usou-se a seguinte expressão para que os carácteres do janela que abre estejam codificados como UTF-8:
```batch
@chcp 65001 > nul
```
De seguida usa-se a expressão seguinte que abre o ficheiro .theme mudando o tema, espera 10 segundos e fecha a janela das definições que abre:
```batch
start "" "[localização do ficheiro .theme]" & timeout /t 10 & taskkill /im "SystemSettings.exe" /f
```

**NOTA : Este método foi testado e funciona tanto no Windows 10 e 11, mas tem alguns pontos a ter em consideração:**
* O tempo de espera foi definido como 10 segundos uma vez a janela das definições tem de abrir antes de terminar a sua tarefa relacionada. Isto resulta em 2 problemas detetados:
    * No Windows 10 a janela das definições pode demorar mais de 10 segundos a abrir, resultando no código terminar e não fechar a janela das definições;
    * No Windows 11 o código termina mais cedo do que normal deixando aberta a janela das definições.