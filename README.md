# SN50v3-CB
Kod źródłowy dla SN503-CB
Węzeł czujnika NB-IoT/CAT-M oparty na Quectel BG95-M2/M3

<!-- TOC depthFrom:1 -->
- Dokumentacja płyty głównej: https://github.com/dragino/Lora/tree/master/LSN50/v3.0/motherboard 
- Dokumentacja modułu NB-IoT/CAT-M: https://github.com/dragino/NB-IoT/tree/master/NB%20ST/BG95-NGFF%20v1.0
<!-- /TOC -->

# Instrukcja budowania projektu
## 1. Pobrać środowisk programistyczne Arm Keil uVision5
Link do pobrania Arm Keil uVision5: https://www.keil.com/demo/eval/arm.htm
Instrukcja do pobrania oraz uzyskania licencji programu  Arm Keil uVision5 od Dragino: https://wiki.dragino.com/xwiki/bin/view/Main/Firmware%20Compile%20Instruction%20--%20STM32/

## 2. Instalacja urządzenia serii STM32L0 w systemie Keil (CMSIS + Device Family Pack)
link do pobrania Device Family Pack dla STMicroelectronics STM32L072CZTx: https://www.keil.com/dd2/stmicroelectronics/stm32l072cztx/#/eula-container
Po instalacji, upewnij się że zostały zainstalowane wszystkie niezbędne pakiety oraz doinstaluj CMSIS Pack.
  1. W programie Arm Keil uVision5 wybierz Pack Installer
  2. Po lewej stronie w panelu „Devices” znajdź i zaznacz: STMicroelectronics → STM32L0 Series → STM32L072CZTx
  3. Przejdź do zakładki "Packs" i zainstaluj: STM32L0xx_DFP, CMSIS CORE
     
## 3. Instalacja ARM Compiler 5
Uwaga: ARM Compiler 5 jest klasyfikowany jako produkt "Legacy", co oznacza, że nie jest już aktywnie rozwijany, dlatego nie jest on pobierany i instalowany automatycznie wraz z programem Arm Keil uVision5.
  1. ARM Compiler 5.06 Update 7 (build 960) – Pobierz: https://developer.arm.com/downloads/view/ACOMP5
     Po przejściu na stronę, może być konieczne zalogowanie się na konto ARM Developer.
  2. Zainstaluj W lokalizacji programu Arm Keil uVision5 w folderze ARM na przykład C:\programs\Keil_v5\ARM\
  3. W programie Arm Keil uVision5 wybierz Menage Project Items
     3.1. Przejdź do zakładki Folders/Extensions
     3.2. Kliknij 3 kropki w polu Use ARM Compiler
     3.3. Kliknij Add another ARM Compiler  Versin to List... 
          i wybierz ścieżkę do folderu z zainstalowanym Compiler 5
     3.4. W polu Use ARM Compiler kliknij Setup Default ARM Compiler Version i wybiezrz zainstalowaną wersję 5.06 Update 7 (build 960) i zatwierdź OK

## 4. Options for Target
     4.1. W zakładce Device upewnij się że jest wybrane odpowiednie urządzenie 
          STMicroelectronics → STM32L0 Series → STM32L072CZTx
     4.2. W zakładce Target w polu Code generation wybierz  RM Compiler V5.06 Update 7 (build 960)
     4.3. W zakładce Output upewnij się że zaznaczone jest pole Create HEX File
     4.4. W zakładce User upewnij śię że W polu After Build → Run #1 jest wybrana odpowiednia ścieżka do pliku fromelf.exe  np.
          C:\programs\Keil_v5\ARM\ARMCLANG\bin\fromelf.exe 
     4.5. Zakładka C/C++
          Źródło wsparcia definiuje zarówno modele serii -CB, jak i -CS. Seria -CS pobiera próbkę napięcia z akumulatora, co różni się od serii -CB.
        <img width="480" alt="eb575b8259f1ed115c87e391dc8c438" src="https://github.com/dragino/NBSN95/assets/652246/48784b33-20f5-48ea-abcd-a5b7854687b2">

        * Jeśli zdefiniowano NB_NS , kod źródłowy jest przeznaczony dla serii -CS. 
        * Jeśli nie zdefiniowano parametru NB_NS, kod źródłowy jest przeznaczony dla serii -CB.
          Czyli dla urządzenia seri CB należy usunąć , NB_NS w polu Define



