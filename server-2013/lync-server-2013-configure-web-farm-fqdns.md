---
title: 'Lync Server 2013: Configurare i nomi di dominio completi (FQDN) delle Web farm'
TOCTitle: Configurare i nomi di dominio completi (FQDN) delle Web farm
ms:assetid: cb25dbbd-dcea-4997-8e14-e5007dd7d3ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429722(v=OCS.15)
ms:contentKeyID: 49301971
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i nomi di dominio completi (FQDN) delle Web farm per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-29_

Quando si definisce la configurazione del server Standard Edition, del pool Front End, del Server Director o del pool di server Director in Generatore di topologie, si configura un nome di dominio completo (FQDN) dei servizi Web esterni. Durante il processo di accesso di un client ospitato nel server Standard Edition o nel pool Front End, gli FQDN dei servizi Web configurati vengono inviati per mezzo del provisioning di tipo in-band. Se è necessario aggiungere o modificare l'URL dei servizi Web esterni, utilizzare Generatore di topologie per configurare o riconfigurare i servizi Web eseguendo la procedura descritta in questo argomento.

## Per configurare l'FQDN di un pool esterno per i servizi Web

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console di Generatore di topologie, in **Standard Edition Front End Server** , **Pool Enterprise Edition Front End** e **Director** , fare clic con il pulsante destro del mouse sul nome del pool da modificare e quindi scegliere **Modifica proprietà** .

3.  Nella sezione **Servizi Web** aggiungere o modificare l'FQDN per i servizi Web esterni.

4.  Controllare e modificare i valori di **Porte di attesa** sia per HTTP che per HTTPS. I valori predefiniti saranno i seguenti:
    
      - **Porte di attesa:** HTTP 8080, HTTPS 4443
    
      - **Porte pubblicate:** HTTP 80, HTTPS 443
    
    Dove per **Porte di attesa** si intendono le porte che verranno configurate per i servizi Web esterni per ricevere le richieste dal proxy inverso e per **Porte pubblicate** si intendono le porte pubblicate esternamente dal proxy inverso e comunicate ai client durante il provisioning di tipo in-band.

5.  Dopo aver aggiunto e aggiornato le configurazioni, fare clic su **OK** per continuare.

6.  Fare clic con il pulsante destro del mouse su **Lync Server 2013** e quindi scegliere **Pubblica** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Al termine della pubblicazione, è possibile che venga visualizzato un collegamento in cui viene indicato che devono essere eseguiti passaggi aggiuntivi. Facendo clic sul collegamento viene visualizzato un elenco di server interessati dalle modifiche effettuate in Generatore di topologie e per i quali sarà necessario rieseguire la Distribuzione guidata di Lync Server per aggiornare la configurazione per i componenti aggiunti, rimossi o modificati.</td>
    </tr>
    </tbody>
    </table>


7.  Ripetere questi passaggi per tutti i server Standard Edition, i pool Front End, i Server Director o i pool di server Director all'interno dell'organizzazione.

