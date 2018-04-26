---
title: Visualizzare i criteri delle versioni client
TOCTitle: Visualizzare i criteri delle versioni client
ms:assetid: 6cd9a897-c694-4d6a-8259-2d3c01fce275
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898479(v=OCS.15)
ms:contentKeyID: 52062179
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare i criteri delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

I criteri delle versioni client vengono utilizzati per applicare un set di regole di controllo delle versioni dei client a livello globale oppure a un sito, un pool o un gruppo di utenti specifico. È possibile visualizzare i criteri delle versioni client configurati nell'ambiente di Lync Server 2013 dal Pannello di controllo di Lync Server 2013 o da Lync Server 2013 Management Shell.

## Per visualizzare i criteri delle versioni client tramite il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Criteri versione client**.

4.  Se si desidera visualizzare le regole per un set di criteri delle versioni client, nella pagina **Criteri versione client** fare doppio clic sui criteri che si desidera visualizzare.

## Visualizzazione dei criteri delle versioni client tramite i cmdlet di Windows PowerShell

Per visualizzare i criteri delle versioni client, è possibile utilizzare il cmdlet **Get-CsClientVersionPolicy**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare i criteri delle versioni client

  - Per visualizzare informazioni su tutti i criteri delle versioni client, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsClientVersionPolicy
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity    : Global
        Rules       : {RuleId=2336c611-a243-4c5d-994b-eea8a524d0e4;
                      Description=;Action=Block;ActionUrl=;MajorVersion=1;
                      MinorVersion=3;BuildNumber=;QfeNumber=;
                      UserAgent=RTC;UserAgentFullName=;Enabled=True;
                      CompareOp=LEQ, RuleId=342c9b90-4cef-483a-a73a-
                      4fe75c88711d;Description=;Action=Block;ActionUrl=;
                      MajorVersion=5;MinorVersion=;BuildNumber=;QfeNumber=;
                      UserAgent=WM;UserAgentFullName=;Enabled=True;
                      CompareOp=LEQ,RuleId=ea03af61-9db5-4bf9-af3f-042
                      ab8dd9994;Description=;Action=Block;ActionUrl=;
                      MajorVersion=3;MinorVersion=5;BuildNumber=6907;
                      QfeNumber=83;UserAgent=OC;UserAgentFullName=;
                      Enabled=True;CompareOp=LEQ, RuleId=831edb68-
                      e482-4431-a10e-add365ba8099;Description=;
                      Action=Block;ActionUrl=;MajorVersion=2;MinorVersion=0;
                      BuildNumber=5999;QfeNumber=;UserAgent=UCCP;
                      UserAgentFullName=;Enabled=True;CompareOp=LEQ...}
        Description :

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Get-CsClientVersionPolicy](get-csclientversionpolicy.md).

