---
title: 'Lync Server 2013: Configurazione della pagina di partecipazione alle riunioni'
TOCTitle: Configurazione della pagina di partecipazione alle riunioni
ms:assetid: 45880423-47f4-49af-b825-cbd8e3fc1046
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204861(v=OCS.15)
ms:contentKeyID: 49300396
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della pagina di partecipazione alle riunioni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando un utente fa clic sul collegamento di una riunione in una convocazione di riunione, nella pagina di partecipazione alle riunioni viene rilevato se è già installato un client Lync 2013 nel computer dell'utente. In caso affermativo, il client viene aperto e accede alla riunione. In caso contrario, per impostazione predefinita viene aperta la versione 2013 di Lync Web App.

È possibile modificare il comportamento della pagina di partecipazione alle riunioni in modo da consentire agli utenti di partecipare alle riunioni con Office Communicator 2007 R2 o Lync 2010 Attendant. Queste opzioni di configurazione sono state rimosse dal Pannello di controllo di Lync Server 2013, ma è possibile configurarle usando il cmdlet Set-CsWebServiceConfiguration.

### Parametri di Set-CsWebServiceConfiguration per la pagina di partecipazione alle riunioni

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro Set-CsWebServiceConfiguration</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ShowJoinUsingLegacyClientLink</p></td>
<td><p>Se l'impostazione è True (valore predefinito), gli utenti che partecipano a una riunione utilizzando un'applicazione client diversa da Lync avranno la possibilità di accedere alla riunione usando Office Communicator 2007 R2. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p>ShowAlternateJoinOptionsExpanded</p></td>
<td><p>Se si imposta questo parametro su True, verranno espanse e visualizzate automaticamente agli utenti opzioni alternative per partecipare a una conferenza online, ad esempio Office Communicator 2007 R2. Se invece si imposta il parametro su False (valore predefinito), queste opzioni saranno comunque disponibili, ma l'utente dovrà visualizzare manualmente l'elenco.</p></td>
</tr>
</tbody>
</table>


## Per configurare la pagina di partecipazione alla riunione tramite Lync Server 2013 Management Shell

1.  Avviare Lync Server 2013 Management Shell. A tale scopo, fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per visualizzare le impostazioni dei servizi Web, eseguire il cmdlet seguente:
    
        Get-CsWebServiceConfiguration

3.  Eseguire il comando seguente, con i parametri impostati su True o False in base alle proprie preferenze. Per informazioni dettagliate sui parametri per questo cmdlet, vedere la documentazione relativa a [Set-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsWebServiceConfiguration) nella documentazione relativa a Lync Server 2013 Management Shell:
    
        Set-CsWebServiceConfiguration -Identity global -ShowJoinUsingLegacyClientLink $True

## Vedere anche

#### Ulteriori risorse

[Set-CsWebServiceConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsWebServiceConfiguration)

