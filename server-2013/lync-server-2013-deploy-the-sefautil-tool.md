---
title: Distribuire lo strumento SEFAUtil
TOCTitle: Distribuire lo strumento SEFAUtil
ms:assetid: fb556e50-88dd-4404-a3d5-be36f5ba41e6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945659(v=OCS.15)
ms:contentKeyID: 52062489
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire lo strumento SEFAUtil

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Per distribuire e gestire la risposta alle chiamate di gruppo, è necessario usare lo strumento SEFAUtil, incluso negli strumenti del Resource Kit di Lync Server 2013. Per potere installare SEFAUtil, innanzitutto necessario disporre di un pool di applicazioni attendibili nella topologia, specificare SEFAUtil come applicazione attendibile e abilitare la topologia.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È necessario che Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK sia installato nei computer in cui si prevede di eseguire lo strumento SEFAUtil.</td>
</tr>
</tbody>
</table>


È possibile eseguire SEFAUtil in qualsiasi pool Front End nella distribuzione.


> [!NOTE]
> Per informazioni dettagliate sull'esecuzione di SEFAUtil, vedere l'articolo relativo alla procedura per l'esecuzione di SEFAutil nel blog di Technet all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=278940">http://go.microsoft.com/fwlink/?linkid=278940</A>.



## Per distribuire SEFAUtil

1.  Accedere al computer in cui è installata Lync Server Management Shell come membro del gruppo RTCUniversalServerAdmins oppure con i diritti utente necessari, come descritto in [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Lo strumento SEFAUtil può essere eseguito solo su un computer appartenente a un pool di applicazioni attendibili. Se necessario, definire un pool di applicazioni attendibili per il pool Front End in cui si prevede di eseguire SEFAUtil. Nella riga di comando digitare il comando seguente:
    
        New-CsTrustedApplicationPool -id <Pool FQDN> -Registrar <Pool Registrar FQDN> -site Site:<Pool Site>

4.  Definire lo strumento SEFAUtil come un'applicazione attendibile. Nella riga di comando digitare il comando seguente:
    
        New-CsTrustedApplication -ApplicationId sefautil -TrustedApplicationPoolFqdn <Pool FQDN>  -Port 7489
    

    > [!NOTE]
    > Se necessario, è possibile utilizzare una porta diversa.



5.  Abilitare le modifiche nella topologia. Nella riga di comando digitare il comando seguente:
    
        Enable-CsTopology

6.  Installare gli strumenti del Resource Kit di Lync Server 2013 su un Front End Server presente nel pool di applicazioni attendibili creato nel passaggio 3.

7.  Assicurarsi che lo strumento SEFAUtil venga eseguito correttamente, come indicato di seguito:
    
    1.  Eseguire lo strumento dal prompt dei comandi di Windows con privilegi di amministratore per visualizzare le impostazioni relative al trasferimento chiamate di un utente della distribuzione.
        

        > [!NOTE]
        > Lo strumento è disponibile in \Programmi\Microsoft Lync Server 2013\Reskit.

    
    2.  Visualizzare le impostazioni relative al trasferimento chiamate di un utente. Nella riga di comando digitare il comando seguente:
        
            SEFAUtil.exe <user SIP address> /server:<Lync Server/Pool FQDN>
        
        Verranno visualizzate le impostazioni relative al trasferimento chiamate di un utente.

