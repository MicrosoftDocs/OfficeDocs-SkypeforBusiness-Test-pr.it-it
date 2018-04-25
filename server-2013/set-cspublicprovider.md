---
title: Set-CsPublicProvider
TOCTitle: Set-CsPublicProvider
ms:assetid: ff7c1a5a-823c-41f7-80dc-1f5842609ccb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413087(v=OCS.15)
ms:contentKeyID: 49302595
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un provider pubblico attualmente configurato per l'utilizzo nell'organizzazione. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo\!, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-VerificationLevel <AlwaysVerifiable | AlwaysUnverifiable | UseSourceVerification>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene impostato il parametro VerificationLevel per il provider pubblico con valore Identity Messenger. Questa operazione viene eseguita includendo il parametro VerificationLevel e il valore di parametro AlwaysVerifiable.

    Set-CsPublicProvider -Identity "Messenger" -VerificationLevel "AlwaysVerifiable"

## ESEMPIO 2

Nell'esempio 2 il livello di verifica viene modificato per tutti i provider pubblici attualmente utilizzati nell'organizzazione. A tal scopo, viene innanzitutto chiamato il cmdlet **Get-CsPublicProvider** senza parametri per restituire una raccolta di tutti i provider pubblici attualmente configurati per l'utilizzo. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPublicProvider**, che seleziona ogni provider nella raccolta e ne modifica il valore della proprietà VerificationLevel in AlwaysVerifiable.

    Get-CsPublicProvider | Set-CsPublicProvider -VerificationLevel "AlwaysVerifiable"

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 viene modificato il livello di verifica per qualsiasi provider pubblico per cui il livello sia attualmente impostato su AlwaysUnverifiable. Per eseguire questa attività, viene innanzitutto chiamato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici configurati per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo i provider in cui la proprietà VerificationLevel è uguale a AlwaysUnverifiable. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsPublicProvider**, che modifica la proprietà VerificationLevel per ogni provider nella raccolta in AlwaysVerifiable.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysUnverifiable"} | Set-CsPublicProvider -VerificationLevel "AlwaysVerifiable"

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Quando è stata stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando le applicazioni SIP. Ad esempio, Microsoft Lync 2010. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che fornisce servizi di comunicazione SIP al pubblico. Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider. Ad esempio, se si stabilisce una federazione con Messenger (MSN), in base alla configurazione del sistema, gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di messaggistica istantanea Messenger.

Per poter stabilire una federazione con un provider pubblico, sarà necessario crearne e abilitarne uno nuovo, e il provider pubblico dovrà creare una relazione di federazione con l'utente o l'organizzazione. Lync Server include tre provider pubblici già configurati: Yahoo\!, AOL e MSN. Quando diventano disponibili altri provider pubblici, è possibile creare relazioni di federazione con tali nuovi provider utilizzando il cmdlet **New-CsPublicProvider**. Dopo aver stabilito le relazioni federate, è possibile utilizzare il cmdlet **Set-CsPublicProvider** per modificare due importanti valori delle proprietà, ovvero Enabled e VerificationLevel, di tali relazioni.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsPublicProvider** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPublicProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la relazione di federazione tra l'organizzazione e il provider pubblico è attiva o meno. Se è impostato su True, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con utenti che dispongono di un account ospitato dal provider pubblico. Se è impostato su False, gli utenti dell'organizzazione non potranno scambiare messaggi istantanei e informazioni sulla presenza con utenti che dispongono di un account ospitato dal provider pubblico.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider pubblico da modificare. Il parametro Identity in genere corrisponde al nome del sito Web che fornisce i servizi, ad esempio Yahoo!, AOL, MSN e così via.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DisplayPublicProvider</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>VerificationLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Edge.VerificationLevelType</p></td>
<td><p>Indica come o se i messaggi inviati dal provider pubblico devono essere verificati per accertare che provengano effettivamente da quel provider. È necessario impostare VerificationLevel su uno dei seguenti valori:</p>
<p>AlwaysVerifiable. Tutti i messaggi che risultano inviati da questo provider verranno accettati. Se nel messaggio non viene rilevata alcuna intestazione di verifica, questa verrà aggiunta da Lync Server. Questo è il valore predefinito.</p>
<p>AlwaysUnverifiable. Tutti i messaggi che risultano inviati da un provider pubblico vengono considerati non verificati. Verranno recapitati solo se inviati da una persona inclusa nell'elenco contatti del destinatario. Se ad esempio Davide Garghentini è incluso nell'elenco contatti di un utente, tale utente potrà ricevere i messaggi inviati da Davide Garghentini. Se Luisa Cazzaniga non è inclusa nell'elenco contatti dell'utente, l'utente non sarà in grado di ricevere i relativi messaggi. Si noti che gli utenti di Lync 2013 possono sostituire manualmente questa impostazione, abilitando la ricezione di messaggi da persone non incluse nell'elenco contatti.</p>
<p>UseSourceVerification. Utilizza l'intestazione di verifica aggiunta al messaggio dal provider pubblico. Se mancano le informazioni di verifica, il messaggio verrà rifiutato. L'utilizzo di questo valore è deprecato in Lync Server 2013.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. Il cmdlet **Set-CsPublicProvider** accetta istanze inviate tramite pipe dell'oggetto provider pubblico.

## Tipi restituiti

Il cmdlet **Set-CsPublicProvider** non restituisce un valore o un oggetto. In realtà, il cmdlet configura istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)

