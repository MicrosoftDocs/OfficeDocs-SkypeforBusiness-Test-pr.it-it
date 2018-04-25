---
title: Configurazione della modalità privacy della presenza avanzata
TOCTitle: Configurazione della modalità privacy della presenza avanzata
ms:assetid: e7a6b873-486d-4dfb-a967-c48f61f237f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399028(v=OCS.15)
ms:contentKeyID: 49302319
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della modalità privacy della presenza avanzata

 

_**Ultima modifica dell'argomento:** 2014-12-08_

Con la modalità privacy della presenza avanzata, gli utenti possono limitare le informazioni sulla presenza in modo da essere visibili solo per i contatti contenuti nell'elenco contatti di Lync 2013. Questa opzione è controllata dal parametro EnablePrivacyMode dei cmdlet **New-CsPrivacyConfiguration** e **Set-CsPrivacyConfiguration**. Quando EnablePrivacyMode è impostato su True, l'opzione per limitare le informazioni sulla presenza solo ai contatti diventa disponibile nelle opzioni relative allo stato di Lync 2013. Se invece EnablePrivacyMode è impostato su False, gli utenti possono scegliere di consentire sempre a tutti di visualizzare le informazioni sulla presenza oppure di accettare qualsiasi modifica futura apportata dall'amministratore alla modalità privacy.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le impostazioni della privacy di Lync 2013 e Lync 2010 non vengono rispettate dalle precedenti versioni (Microsoft Office Communicator 2007 R2 o Microsoft Office Communicator 2007). Se alle precedenti versioni di Office Communicator è consentito di accedere, è possibile che un utente non autorizzato visualizzi lo stato, le informazioni di contatto o l'immagine di un utente di Lync 2013. Inoltre, le impostazioni della privacy di un utente di Lync 2013 vengono reimpostate se in seguito accede con la precedente versione di Communicator.<br />
Per questi motivi, in uno scenario di migrazione, prima di abilitare la modalità privacy della presenza avanzata, eseguire le operazioni seguenti:
<ul>
<li><p>Verificare che ogni utente abbia installato Lync 2013.</p></li>
<li><p>Definire una regola dei criteri di versione dei client per impedire alle precedenti versioni di Communicator di accedere.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Per abilitare la modalità privacy della presenza avanzata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il comando seguente:
    
        Get-CsPrivacyConfiguration | Set-CsPrivacyConfiguration -EnablePrivacyMode $True
    
    Questo comando abilita la modalità privacy per tutte le impostazioni di configurazione della privacy attualmente in uso nell'organizzazione.

## Vedere anche

#### Ulteriori risorse

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

