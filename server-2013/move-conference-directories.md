---
title: Spostare le directory conferenze
TOCTitle: Spostare le directory conferenze
ms:assetid: 71a28308-1f3b-4717-b535-2f4bfe3499a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204994(v=OCS.15)
ms:contentKeyID: 49300948
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare le directory conferenze

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Prima della rimozione delle autorizzazioni per un pool, è necessario eseguire la procedura seguente per ogni directory conferenze nel pool di Office Communications Server 2007 R2.

## Per spostare una directory conferenze in Lync Server 2013

1.  Aprire Lync Server Management Shell.

2.  Per ottenere l'identità delle directory conferenze nell'organizzazione, eseguire i comandi seguenti:
    
        Get-CsConferenceDirectory
    
    Dato che il cmdlet restituisce tutte le directory conferenze nell'organizzazione, può essere utile limitare i risultati solo al pool per cui si desidera rimuovere le autorizzazioni. Se si desidera rimuovere le autorizzazioni per un pool con il nome di dominio completo (FQDN) pool01.contoso.net, ad esempio, utilizzare il comando seguente:
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"}
    
    Questo cmdlet restituisce tutte le directory conferenze in cui l'ID di servizio contiene l'FQDN pool01.contoso.net.

3.  Per spostare le directory conferenze, eseguire il comando seguente per ogni directory conferenze nel pool:
    
        Move-CsConferenceDirectory -Identity <Numeric identity of conference directory> -TargetPool <FQDN of pool where ownership is to be transitioned>
    
    Ad esempio:
    
        Move-CsConferenceDirectory -Identity 3 -TargetPool pool02.contoso.net


> [!NOTE]
> Potrebbe verificarsi l'errore mostrato in basso, se lo Lync Server Management Shell necessita di un set aggiornato di autorizzazioni da Active Directory. Per risolvere l'errore, chiudere la finestra corrente e aprire lo Lync Server Management Shell, quindi eseguire nuovamente il comando.



![Output dell'errore di Move-CsConferenceDirectory](images/JJ204994.4748b9e8-9651-4527-afe1-cbdc6d5ce4a8(OCS.15).jpg "Output dell'errore di Move-CsConferenceDirectory")

