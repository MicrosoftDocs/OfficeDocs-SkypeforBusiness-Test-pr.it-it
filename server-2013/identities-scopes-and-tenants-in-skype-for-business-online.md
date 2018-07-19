---
title: Identità, ambiti e tenant
TOCTitle: Identità, ambiti e tenant
ms:assetid: 7cfa194a-2d01-4370-9b48-ee13ff597fa5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362819(v=OCS.15)
ms:contentKeyID: 56269947
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Identità, ambiti e tenant

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Molti dei cmdlet di Windows PowerShell usati per la gestione di Skype for Business online richiedono molta precisione rispetto all'elemento da gestire. Ad esempio, quando si esegue il cmdlet [Set-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUserAcp), è necessario indicare quale utente si intende gestire. Questo comportamento è logico in quanto, in mancanza di un'indicazione specifica, il cmdlet **Set-CsUserAcp** non è in grado di determinare quale sia l'utente di cui modificare le impostazioni relative al provider di servizi di audioconferenza. Per questo motivo, ogni volta che si esegue il cmdlet **Set-CsUserAcp** è necessario includere il parametro Identity seguito dall'identità dell'account utente da modificare:

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

Se il termine *Identity* è sempre riferito all'identità di un account utente, esistono pochi motivi di confusione. Quando si gestiscono persone (utenti, contatti e così via), le identità fanno riferimento ai singoli utenti. Anche elementi diversi dagli account utente, tuttavia, possono disporre di un'identità. Quando si gestiscono componenti del servizio Skype for Business online, quali criteri, impostazioni di configurazione e così via, il termine Identity ha un significato leggermente diverso. Si consideri ad esempio il comando seguente:

    Get-CsMeetingConfiguration -Identity "global"

In questo caso, l'identità "global" fa riferimento all'ambito delle impostazioni di configurazione delle riunioni. *Ambito* è un termine usato in Skype for Business online e in Lync Server per designare le sfere di gestione. Per impostazione predefinita, i criteri e le impostazioni hanno sempre un ambito globale. Quando si configura per la prima volta il proprio account di Skype for Business online, per impostazione predefinita si disporrà di una raccolta di impostazioni e criteri globali, che include impostazioni globali di configurazione delle riunioni, criteri globali di accesso esterno, un dial plan globale e così via.

Tali impostazioni e criteri globali sono stati introdotti in Microsoft Lync Server 2010 per assicurare la possibilità di gestire sempre tutti gli utenti e tutti i componenti. In Microsoft Office Communicator 2007 R2 questo non sempre è possibile. In base al modo in cui si accede al sistema, infatti, si potrebbe finire in uno stato in gran parte non gestito, in genere perché non è stato possibile applicare Criteri di gruppo all'account utente. In Lync Server e in Skype for Business online, al contrario, nessun elemento viene mai lasciato in stato non gestito. Questo perché, in mancanza di altro, vengono sempre applicati i criteri e le impostazioni globali.

Cosa si intende per "in mancanza d'altro"? Nel caso di Skype for Business online è possibile creare criteri in *ambito tag*. I criteri creati nell'ambito tag, denominato anche *ambito per utente*, hanno la precedenza sui criteri creati nell'ambito globale. In altre parole, i criteri per utente hanno sempre la precedenza sui criteri globali. Si supponga ad esempio di disporre di due criteri di accesso degli utenti esterni. Il criterio globale proibisce agli utenti di comunicare con persone che dispongono di account con provider di messaggistica istantanea pubblici, come Windows Live. Il criterio per utente, AllowPublicIMCommunication, consente la comunicazione con i provider di messaggistica istantanea pubblici.

Si supponga inoltre che esistano due utenti. Il primo è Ken Myer, al quale è assegnato il criterio per utente, la seconda è Pilar Ackerman, alla quale non è assegnato alcun criterio per utente. Quest'ultima è quindi gestita dal criterio di accesso degli utenti esterni. La tabella seguente indica gli utenti autorizzati a comunicare con i provider di messaggistica istantanea pubblici.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazioni criteri</th>
<th>Ken Myer</th>
<th>Pilar Ackerman</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impostazione criteri globali per provider di servizi di messaggistica istantanea pubblici</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Impostazione criteri per utente per provider di servizi di messaggistica istantanea pubblici</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>L'utente può comunicare con provider di servizi di messaggistica istantanea pubblici</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


Come si può vedere, Ken Myer può comunicare con i provider di messaggistica istantanea pubblici, in quanto il criterio per utente che gli è assegnato prevale sulle importazioni del criterio globale. Pilar Ackerman non può invece comunicare con i provider di messaggistica istantanea pubblici, in quanto è gestita dal criterio globale, che vieta tali comunicazioni.

I criteri per utente devono essere creati dal supporto di Office 365. Dopo la creazione dei criteri, sarà possibile assegnarli agli utenti usando il cmdlet **Grant-Cs** appropriato, ad esempio [Grant-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsExternalAccessPolicy). I criteri per utente sono semplici da identificare, in quanto il parametro Identity del criterio inizia sempre con il **prefisso** tag. Ad esempio:

    Identity : tag:AllowPublicIMCommunication


> [!NOTE]
> Il <STRONG>prefisso</STRONG> tag risale agli albori dello sviluppo di Lync Server 2010. In precedenza infatti, i criteri per utente erano denominati <EM>criteri tag</EM> ed erano identificati dal <STRONG>prefisso</STRONG> tag. Tali criteri sono ora denominati con maggiore precisione <EM>criteri per utente</EM> e l'ambito tag è ora denominato con maggiore precisione <EM>ambito per utente</EM>. Per motivi tecnici, tuttavia, il <STRONG>prefisso</STRONG> tag non è stato mai modificato.



Un altro termine importante utilizzato nell'ambito di Skype for Business online e Windows PowerShell è *tenant*. Quando si configura un account di Skype for Business online, alla nuova distribuzione viene assegnato un numero di ID tenant, ovvero un identificatore univoco globale (GUID) simile al seguente:

    bf19b7db-6960-41e5-a139-2aa373474354

Alcuni cmdlet di Skype for Business online richiedono l'inserimento dell'ID tenant a ogni esecuzione. È necessario immettere l'ID tenant anche se si dispone di un unico tenant e vi si è già effettuato l'accesso. Non è necessario memorizzare l'ID tenant, che può essere recuperato in qualsiasi momento eseguendo il comando di Windows PowerShell seguente:

    Get-CsTenant | Select-Object TenantId

Conoscere la differenza tra ambito globale e ambito per utente (o ambito tag) non è sufficiente. È anche importante sapere quando, o persino se, è possibile usare tali ambiti. Lo stesso concetto vale per le identità e per il parametro tenant. Gli argomenti seguenti illustrano in che modo i diversi cmdlet di Skype for Business online usano le identità, gli ambiti e il parametro tenant:

  - [Cmdlet che usano solo l'ambito globale](cmdlets-in-skype-for-business-online-that-use-only-the-global-scope.md)

  - [Cmdlet che usano l'ambito globale e l'ambito tag](cmdlets-in-skype-for-business-online-that-use-the-global-scope-and-the-tag-scope.md)

  - [Cmdlet che usano l'identità di un utente](cmdlets-in-skype-for-business-online-that-use-a-user-identity.md)

  - [Cmdlet che usano un'identità utente e l'ambito tag](cmdlets-in-skype-for-business-online-that-use-a-user-identity-and-the-tag-scope.md)

  - [Cmdlet che usano il parametro Tenant](cmdlets-in-skype-for-business-online-that-use-the-tenant-parameter.md)

  - [Cmdlet che usano l'identità di un provider di servizi di conferenza](cmdlets-in-skype-for-business-online-that-use-a-conferencing-provider-identity.md)

  - [Cmdlet che non usano un ambito o un'identità](cmdlets-in-skype-for-business-online-that-do-not-use-a-scope-or-an-identity.md)

