---
title: Visualizzare gli aggiornamenti software per i dispositivi in Lync Server 2013
TOCTitle: Visualizzare gli aggiornamenti software per i dispositivi in Lync Server 2013
ms:assetid: d2cca12b-ed43-4e1f-90ab-d14bca8b482c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182592(v=OCS.15)
ms:contentKeyID: 49302070
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare gli aggiornamenti software per i dispositivi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Con Lync Server 2013 su utilizza il servizio Web di aggiornamento dispositivi per visualizzare e gestire gli aggiornamenti software per i dispositivi dell'organizzazione. Questi aggiornamenti sono disponibili come file CAB (cabinet) nel sito Web del Supporto Tecnico Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?linkid=204091\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=204091%26clcid=0x410). Dopo aver scaricato il file CAB, eseguire il cmdlet **Import-CSdeviceUpdate** per importare le regole di aggiornamento dei dispositivi da tale file. Per informazioni dettagliate sul cmdlet **Import-CSdeviceUpdate**, vedere [Import-CsDeviceUpdate](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsDeviceUpdate) nella documentazione relativa a Lync Server Management Shell.

> [!tip]  
> Prima di distribuire un nuovo aggiornamento nell'organizzazione, verificarne il corretto funzionamento su un dispositivo di test.

## Per visualizzare gli aggiornamenti software per i dispositivi per comunicazioni unificate

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Dal sito Web del Supporto Tecnico Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?linkid=204091\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=204091%26clcid=0x410) scaricare il file CAB in un percorso di un computer con Lync Server 2013, ad esempio C:\\Updates\\UCUpdates.cab.

3.  Importare le regole di aggiornamento dei dispositivi dal file C:\\Updates\\UCUpdates.cab eseguendo uno dei cmdlet seguenti:
    
      - Se il file CAB si trova sullo stesso computer sul quale è in esecuzione il servizio da aggiornare (service:Redmond-websvc-2), eseguire il cmdlet seguente:
        
            Import-CsDeviceUpdate -Identity service:Redmond-websvc-2 -FileName C:\Updates\UCUpdates.cab
    
      - Se il file CAB si trova su un computer diverso da quello sul quale è in esecuzione il servizio da aggiornare (service:Redmond-websvc-3), eseguire il cmdlet seguente:
        
            Import-CsDeviceUpdate -Identity service:Redmond-websvc-3 -ByteInput C:\Updates\UCUpdates.cab

4.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

5.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi su **Aggiornamento dispositivi**.

6.  Nella pagina **Aggiornamento dispositivi** fare clic su un aggiornamento nell'elenco ed eseguire una delle operazioni seguenti:
    
      - **Annullare un aggiornamento in sospeso.** Per impedire che l'aggiornamento selezionato venga distribuito nei dispositivi dell'organizzazione, fare clic sul menu **Azione** e quindi su **Annulla aggiornamenti in sospeso**.
    
      - **Approvare un aggiornamento.** Per consentire la distribuzione dell'aggiornamento selezionato nei dispositivi dell'organizzazione, fare clic sul menu **Azione** e quindi su **Approva**.
    
      - **Ripristinare un aggiornamento.** Per consentire la distribuzione di un aggiornamento approvato in precedenza nei dispositivi dell'organizzazione, fare clic sul menu **Azione** e quindi su **Ripristina**.

## Vedere anche

#### Ulteriori risorse

[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

