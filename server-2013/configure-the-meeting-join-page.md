---
title: Configurare la pagina di partecipazione alle riunioni
TOCTitle: Configurare la pagina di partecipazione alle riunioni
ms:assetid: 036c9d03-ad95-4d63-a3d8-6cae1a8ad530
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204635(v=OCS.15)
ms:contentKeyID: 49299519
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la pagina di partecipazione alle riunioni

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando un utente fa clic sul collegamento di una riunione in una convocazione riunione, nella pagina di partecipazione alla riunione viene rilevato se nel computer dell'utente è già installato un client Lync 2013. In caso affermativo, il client viene aperto e accede alla riunione. In caso negativo, per impostazione predefinita viene aperta la versione 2013 di Lync Web App.

È possibile modificare il comportamento della pagina di partecipazione alla riunione se si desidera consentire agli utenti di partecipare alle riunioni con Office Communicator 2007 R2 o Lync 2010 Attendant. Queste opzioni di configurazione sono state rimosse dal Pannello di controllo di Lync Server 2013, ma è possibile configurarle mediante il cmdlet CsWebServiceConfiguration.

### Parametri di CsWebServiceConfiguration per la pagina di partecipazione alla riunione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro di CsWebServiceConfiguration</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ShowJoinUsingLegacyClientLink</p></td>
<td><p>Se l'impostazione è True, gli utenti che accedono a una riunione con un'applicazione client diversa da Lync avranno la possibilità di partecipare alla riunione utilizzando Office Communicator 2007 R2. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p>ShowAlternateJoinOptionsExpanded</p></td>
<td><p>Se si imposta questo parametro su True, verranno espanse e visualizzate automaticamente agli utenti opzioni alternative per partecipare a una conferenza online, ad esempio Office Communicator 2007 R2. Se invece si imposta il parametro su False (valore predefinito), queste opzioni saranno comunque disponibili, ma l'utente dovrà visualizzare manualmente l'elenco.</p></td>
</tr>
</tbody>
</table>


## Per configurare la pagina di partecipazione alla riunione tramite Lync Server 2013 Management Shell

1.  Avviare Lync Server 2013 Management Shell. A tale scopo, fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet seguente:
    
        Get-CsWebServiceConfiguration
    
    Questo cmdlet restituirà le impostazioni di configurazione del servizio Web.

3.  Eseguire il comando seguente, con i parametri impostati su True o False in base alle proprie preferenze. Per informazioni dettagliate sui parametri per questo cmdlet, vedere la documentazione relativa a Lync Server 2013 Management Shell:
    
        Set-CsWebServiceConfiguration -Identity global -ShowJoinUsingLegacyClientLink $True

