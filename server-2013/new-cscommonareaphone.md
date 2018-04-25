---
title: New-CsCommonAreaPhone
TOCTitle: New-CsCommonAreaPhone
ms:assetid: 6082d24d-de92-4a3c-8639-5d28341cbc84
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398430(v=OCS.15)
ms:contentKeyID: 49300729
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCommonAreaPhone

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo telefono di area comune che può essere gestito tramite Lync Server. I telefoni di area comune sono telefoni posizionati nelle sale d'attesa degli edifici, nelle sale di ritrovo del personale o in altre posizioni in cui possono essere utilizzati da persone diverse e per usi diversi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsCommonAreaPhone -DN <ADObjectId> <COMMON PARAMETERS>

    New-CsCommonAreaPhone -OU <OUIdParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: -LineUri <String> -RegistrarPool <Fqdn> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare un nuovo telefono in un'area comune con numero telefonico 1-425-555-6710. Si noti che il parametro LineUri deve essere specificato utilizzando il formato E.164. Oltre a specificare il numero di telefono, il comando specifica anche il pool di registrazione (RegistrarPool), il nome visualizzato di Active Directory (DisplayName) e il nome distinto dell'unità organizzativa in cui deve essere creato il corrispondente oggetto contatto (OU).

    New-CsCommonAreaPhone -LineUri tel:+14255556710 -RegistrarPool redmond-cs-001.litwareinc.com -DisplayName "Building 14 Lobby" -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## ESEMPIO 2

Il comando riportato nell'Esempio 2 è una variante del comando riportato nell'Esempio 1. Nell'Esempio 2, però, il nuovo telefono in un'area comune è associato a un oggetto contatto di Active Directory esistente. Per ottenere questo risultato, il comando utilizza il parametro DN invece del parametro OU, specificando il nome distinto dell'oggetto contatto esistente (cn=Building 14 Lobby,ou=Telecommunications,dc=litwareinc,dc=com) come valore del parametro. In questo comando, anche il parametro DisplayName viene ignorato e ciò significa che il nuovo telefono in un'area comune utilizzerà il nome visualizzato assegnato all'oggetto contatto esistente.

    New-CsCommonAreaPhone -LineUri tel:+14255556710 -RegistrarPool redmond-cs-001.litwareinc.com -DN "cn=Building 14 Lobby,ou=Telecommunications,dc=litwareinc,dc=com"

## Descrizione dettagliata

I telefoni delle aree comuni sono telefoni IP non associati a un singolo utente. Anziché trovarsi nell'ufficio di un dipendente, si trovano in genere nelle sale d'attesa dell'edificio, nelle mense, nelle sale di ritrovo del personale, nelle sale riunioni e in altri luoghi in cui è probabile che si riuniscano molte persone. Da un punto di vista della gestione, ciò rappresenta una sfida per gli amministratori, in quanto l'utilizzo del telefono in Lync Server di solito viene controllato mediante criteri vocali e dial plan assegnati a singoli utenti. Ai telefoni delle aree comuni invece non sono assegnati utenti specifici.

Una soluzione a questa sfida è rappresentata dalla creazione di oggetti contatto di Active Directory per tutti i telefoni nelle aree comuni. Questi oggetti contatto possono essere creati usando il cmdlet **New-CsCommonAreaPhone**. Come nel caso degli account utente, anche a questi oggetti contatto è possibile assegnare criteri e voice plan. Di conseguenza, sarà possibile mantenere il controllo dei telefoni nelle aree comuni anche se non sono associati a singoli utenti. Ad esempio, se si desidera evitare che le persone possano trasferire o parcheggiare le chiamate da un telefono in un'area comune, è possibile creare un criterio vocale che impedisca il trasferimento o il parcheggio delle chiamate e quindi assegnare questo criterio ai telefoni nelle aree comuni (oppure, più correttamente, all'oggetto contatto che rappresenta il telefono nell'area comune). Questo comando assegna il criterio vocale CommonAreaPhoneVoicePolicy a tutti i telefoni nelle aree comuni:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Si noti che è possibile creare nuovi telefoni nelle aree comuni usando il cmdlet **New-CsCommonAreaPhone**. Il cmdlet **New-CsCommonAreaPhone** consente di creare nuovi oggetti contatto da utilizzare per i telefoni nelle aree comuni o associare oggetti contatto esistenti a un nuovo telefono in un'area comune. Per ulteriori informazioni, vedere le descrizioni dei parametri OU e DN in questo argomento.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsCommonAreaPhone** i membri dei seguenti gruppi: amministratori di dominio. Le autorizzazioni per l'esecuzione di questo cmdlet per siti oppure unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCommonAreaPhone"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DN</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ADObjectId</p></td>
<td><p>Consente di associare un oggetto contatto di Active Directory esistente al nuovo telefono nell'area comune. Se si dispone di un oggetto contatto che si desidera associare a un telefono in un'area comune, utilizzare il parametro DN seguito dal nome distinto del contatto. Ad esempio: -DN &quot;cn=Building 14 Lobby,dc=litwareinc,dc=com&quot;. Si noti che il comando avrà esito negativo, se il contatto specificato non esiste. Il comando avrà esito negativo anche se il contatto è già stato abilitato per Lync Server. In tal caso, è necessario prima disabilitare il contatto utilizzando il cmdlet <strong>Disable-CsUser</strong> e quindi eseguire il cmdlet <strong>New-CsCommonAreaPhone</strong>.</p>
<p>Il parametro DN è particolarmente utile per le organizzazioni che hanno già creato oggetti contatto per sale conferenza e altre entità. Questi contatti vengono spesso utilizzati a scopo di pianificazione. Utilizzando il parametro DN è possibile creare un nuovo telefono nell'area comune utilizzando uno di questi oggetti contatto pre esistenti.</p>
<p>Non è possibile utilizzare i parametri OU e DN nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono per il telefono nell'area comune. L'URI di linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;. Ad esempio: TEL:+14255551297. Qualsiasi numero di interno deve essere aggiunto alla fine dell'URI di linea, ad esempio: TEL:+14255551297;ext=51297.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Nome distinto dell'unità organizzativa (OU) di Active Directory in cui deve essere posizionato l'oggetto contatto, ad esempio -OU &quot;ou=Redmond,dc=litwareinc,dc=com”.</p>
<p>Se si include il parametro OU, nell'unità organizzativa specificata verrà creato un nuovo contatto e a questo verrà automaticamente assegnato un identificatore univoco globale (GUID) come nome comune. Di conseguenza, l'oggetto contatto avrà un nome simile a questo: {ce84964a-c4da-4622-ad34-c54ff3ed361f}.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione in cui deve essere inserito l'oggetto contatto, ad esempio -RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di impostare l'attributo Description di Active Directory per il telefono nell'area comune. A sua volta, questa operazione consente di fornire informazioni aggiuntive sul telefono (ad esempio, dettagli sulla persona da contattare in caso si verifichino dei problemi con l'apparecchio).</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di impostare il nome visualizzato di Active Directory del telefono nell'area comune.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono come viene visualizzato in Lync. La proprietà DisplayNumber può essere formattata in qualsiasi modo, ad esempio 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234 e così via. Quando si sceglie un numero da visualizzare, tenere presente che il numero verrà visualizzato sullo schermo del telefono di area comune solo se può essere normalizzato. La normalizzazione è il processo di conversione delle stringhe di numeri in un formato standard dei numeri di telefono. Se non esiste una regola di normalizzazione per il formato dei numeri di telefono utilizzato durante la configurazione del numero da visualizzare, sullo schermo del telefono di area comune verrà visualizzato il valore della proprietà LineUri anziché il valore della proprietà DisplayNumber.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce un oggetto che rappresenta il telefono delle aree comuni.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco che consente al telefono di area comune di comunicare con i dispositivi SIP, ad esempio Lync. L'indirizzo SIP deve essere preceduto dal prefisso &quot;sip:&quot; e includere un dominio SIP valido. Ad esempio: sip:bldg14lobby@litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsCommonAreaPhone** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsCommonAreaPhone** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

