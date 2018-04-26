---
title: Get-CsWebServiceConfiguration per la gestione della rubrica
TOCTitle: Get-CsWebServiceConfiguration per la gestione della rubrica
ms:assetid: 0b223733-5224-47d1-9b47-2109e6f135c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429692(v=OCS.15)
ms:contentKeyID: 49299639
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWebServiceConfiguration per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Chi può eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet Get-CsWebServiceConfiguration i membri dei gruppi seguenti: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di Controllo dell'accesso basato sui ruoli (RBAC) a cui tale cmdlet è stato assegnato, inclusi i ruoli RBAC personalizzati creati personalmente, al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsWebServiceConfiguration"}

Get-CsWebServiceConfiguration restituisce le informazioni relative alla configurazione dei servizi Web attualmente in uso nell'organizzazione. Per i servizi Rubrica è interessante lo stato della funzione Distribution List Expansion. Se l'attributo EnableGroupExpansion è True, l'organizzazione attualmente consente l'espansione dei gruppi.

Ad esempio:

    Get-CsWebServiceConfiguration -Identity site:Redmond

Per una descrizione dettagliata del comando completo, vedere l'argomento seguente nella guida di riferimento principale ai cmdlet RTC di Windows PowerShell di Lync Server.

## Vedere anche

#### Ulteriori risorse

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)

