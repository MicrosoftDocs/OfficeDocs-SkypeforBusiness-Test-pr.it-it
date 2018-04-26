---
title: Creare un dispositivo per testare la funzionalità di aggiornamento
TOCTitle: Creare un dispositivo per testare la funzionalità di aggiornamento
ms:assetid: ce509fd1-17b3-4b78-b269-fe5d06fe2e1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182587(v=OCS.15)
ms:contentKeyID: 49302021
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un dispositivo per testare la funzionalità di aggiornamento

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile aggiungere un dispositivo di test nella pagina **Dispositivo di test** e quindi utilizzarlo per verificare le funzionalità dei nuovi aggiornamenti prima di distribuirli nei dispositivi di produzione. Il dispositivo può essere testato a livello globale, ovvero in tutto l'ambiente Lync Server, o in un singolo sito. Per identificare un dispositivo di test, utilizzare il relativo indirizzo MAC (Media Access Control) o il numero di serie. Quando si aggiunge un dispositivo, questo viene visualizzato nell'elenco della pagina **Dispositivo di test** del Pannello di controllo di Lync Server.

## Per aggiungere un dispositivo di test

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi su **Dispositivo di test**.

3.  Fare clic su **Nuovo** e quindi scegliere **Dispositivo di test globale** o **Dispositivo di test sito**.

4.  Eseguire una delle operazioni seguenti:
    
      - Se si è fatto clic su **Dispositivo di test globale**, procedere al passaggio successivo.
    
      - Se si è fatto clic su **Dispositivo di test sito**, selezionare un sito nell'elenco dei siti disponibili e quindi fare clic su **OK**.

5.  In **Nuovo dispositivo di test** digitare un nome per il dispositivo in **Nome dispositivo**.

6.  In **Tipo di identificatore** fare clic su **Indirizzo MAC** o **Numero di serie**.

7.  Nella casella **Identificatore univoco** digitare l'indirizzo MAC o il numero di serie del dispositivo.

8.  Fare clic su **Commit**.

## Creazione di dispositivi di test mediante i cmdlet di Windows PowerShell

I dispositivi di test possono essere creati utilizzando Windows PowerShell e il cmdlet New-CsTestDevice. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

Se si creano dispositivi di test utilizzando questo cmdlet, è necessario eseguire due operazioni:

  - Specificare MACAddress o SerialNumber come IdentifierType.

  - Includere l'ambito quando si specifica l'identità (Identity) del dispositivo. Per creare un nuovo dispositivo nell'ambito globale, utilizzare una sintassi simile alla seguente:
    
        -Identity "global/WindowsPhone"
    
    Per creare un dispositivo di test nell'ambito del sito, utilizzare una sintassi simile alla seguente:
    
        -Identity "site:Redmond/WindowsPhone"

## Per creare un dispositivo di test utilizzando l'indirizzo MAC

  - Il comando seguente crea un dispositivo di test nell'ambito globale utilizzando l'indirizzo MAC come IdentifierType:
    
        New-CsTestDevice -Identity "global/WindowsPhone" -IdentifierType "MACAddress" -Identifier "01:02:03:04:05:06"

## Per creare un dispositivo di test utilizzando il numero di serie

  - Il comando seguente crea un nuovo dispositivo di test nell'ambito del sito (per il sito Redmond) e utilizza il numero di serie come IdentifierType:
    
        New-CsTestDevice -Identity "site:Redmond/WindowsPhone" -IdentifierType "SerialNumber" -Identifier "01ABC5419JKR55T"

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [New-CsTestDevice](new-cstestdevice.md).

