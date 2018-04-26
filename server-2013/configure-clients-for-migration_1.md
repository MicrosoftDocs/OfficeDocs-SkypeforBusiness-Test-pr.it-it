---
title: Configurare i client per la migrazione
TOCTitle: Configurare i client per la migrazione
ms:assetid: 8f17862b-d9d1-47f6-b248-51f4710f5030
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688130(v=OCS.15)
ms:contentKeyID: 49887652
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i client per la migrazione

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento viene illustrata la procedura di distribuzione client consigliata da eseguire prima della migrazione a Lync Server 2013. Queste modifiche della configurazione devono essere eseguite in Office Communications Server 2007 R2. È molto importante eseguire questa procedura prima della migrazione. Per ulteriori informazioni, vedere [Pianificazione dei client e dei dispositivi in Lync Server 2013](lync-server-2013-planning-for-clients-and-devices.md).

## Per configurare i client prima della migrazione

1.  Distribuire gli aggiornamenti più recenti dei client, dei dispositivi e dei server per Office Communications Server 2007 R2.
    
      - [Applicare gli aggiornamenti di Office Communications Server 2007 R2](apply-office-communications-server-2007-r2-updates.md)
    
      - [Descrizione del pacchetto di aggiornamento cumulativo per Communicator 2007 R2](http://go.microsoft.com/fwlink/p/?linkid=335808)
    
      - [Aggiornamenti software per i dispositivi](http://go.microsoft.com/fwlink/?linkid=335809)

2.  In Office Communications Server 2007 R2, usare il filtro delle versioni client per consentire l'accesso solo ai client Office Communications Server 2007 R2 con gli aggiornamenti più recenti installati.

3.  In Office Communications Server 2007 R2 utilizzare il filtro delle versioni client per bloccare l'accesso dei client Lync Server 2013. Eseguire la procedura descritta in **Configurazione del filtro delle versioni client** all'indirizzo [http://go.microsoft.com/fwlink/?linkid=202488\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=202488%26clcid=0x410) aggiungere i filtri di versione elencati nella tabella seguente. Per ogni filtro di versione assegnare l'azione **Blocca** .
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Client</th>
    <th>Intestazione agente utente</th>
    <th>Versione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Lync 2013</p></td>
    <td><p>OC</p></td>
    <td><p>15.*.*.*</p></td>
    </tr>
    <tr class="even">
    <td><p>Lync Web App</p></td>
    <td><p>CWA</p></td>
    <td><p>5.*.*.*</p></td>
    </tr>
    <tr class="odd">
    <td><p>Lync Phone Edition</p></td>
    <td><p>OCPhone</p></td>
    <td><p>4.*.*.*</p></td>
    </tr>
    </tbody>
    </table>

