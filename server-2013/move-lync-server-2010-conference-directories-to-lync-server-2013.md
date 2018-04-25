---
title: Spostare le directory conferenze di Lync Server 2010 in Lync Server 2013
TOCTitle: Spostare le directory conferenze
ms:assetid: 659867e0-ce91-4a95-9787-b1c1566460a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn727126(v=OCS.15)
ms:contentKeyID: 62388559
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare le directory conferenze

 

_**Ultima modifica dell'argomento:** 2014-05-28_

Prima della rimozione delle autorizzazioni per un pool, è necessario eseguire la procedura seguente per ogni directory conferenze nel pool di Lync Server 2010.

## Per spostare una directory conferenze in Lync Server 2013

1.  Aprire Lync Server Management Shell.

2.  Per ottenere l'identità delle directory conferenze nell'organizzazione, eseguire il comando seguente:
    
        Get-CsConferenceDirectory
    
    Il comando precedente restituisce tutte le directory conferenze nell'organizzazione. Per questo motivo potrebbe essere utile limitare i risultati solo al pool per cui è necessario rimuovere le autorizzazioni. Ad esempio, per rimuovere le autorizzazioni per un pool con il nome di dominio completo (FQDN) pool01.contoso.net, utilizzare il comando seguente per limitare i dati restituiti alle directory conferenze da tale pool:
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"}
    
    Questo comando restituisce solo le directory conferenze in cui la proprietà ServiceID contiene l'FQDN pool01.contoso.net.

3.  Per spostare le directory conferenze, eseguire il comando seguente per ogni directory conferenze nel pool:
    
        Move-CsConferenceDirectory -Identity <Numeric identity of conference directory> -TargetPool <FQDN of pool where ownership is to be transitioned>
    
    Ad esempio, per spostare la directory conferenze 3 utilizzare questo comando specificando un pool Lync Server 2013 come TargetPool:
    
        Move-CsConferenceDirectory -Identity 3 -TargetPool "pool02.contoso.net"
    
    Per spostare tutte le directory conferenze in un pool, utilizzare invece un comando simile al seguente:
    
        Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "pool01.contoso.net"} | Move-CsConferenceDirectory -TargetPool "pool02.contoso.net"

Per istruzioni complete e dettagliate sulla rimozione delle autorizzazioni per i pool di Lync 2010, vedere il documento relativo alla disinstallazione di Microsoft Lync Server 2010 e alla rimozione dei ruoli server scaricabile all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=246227](http://go.microsoft.com/fwlink/p/?linkid=246227).

Durante lo spostamento delle directory conferenze potrebbe verificarsi l'errore seguente:

    WARNING: Move operation failed for conference directory with ID "5". Cannot perform a rollback because data migration might have already started. Retry the operation.
    WARNING: Before using the -Force parameter, ensure that you have exported the conference directory data using DBImpExp.exe and imported the data on the target pool. Refer to the DBImpExp-Readme.htm file for more information.
    Move-CsConferenceDirectory : Unable to cast COM object of type 'System._ComObject' to interface type 'Microsoft.Rtc.Interop.User.IRtcConfDirManagement'. 
    This operation failed because the QueryInterface call on the COM component for the interface with SID '{4262B886-503F-4BEA-868C-04E8DF562CEB}' failed due to the following error: The specified module could not be found.

Questo errore si verifica in genere quando Lync Server Management Shell richiede un set aggiornato di autorizzazioni di Active Directory per completare un'attività. Per risolvere il problema, chiudere l'istanza corrente di Management Shell e quindi aprire una nuova istanza della shell ed eseguire di nuovo il comando per spostare la directory conferenze.

