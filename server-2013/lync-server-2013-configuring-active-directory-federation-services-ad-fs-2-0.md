---
title: Configurazione di Active Directory Federation Services (AD FS 2.0)
TOCTitle: Configurazione di Active Directory Federation Services (AD FS 2.0)
ms:assetid: 0ba8657f-55b8-41b3-960c-fdc5eeee6978
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308561(v=OCS.15)
ms:contentKeyID: 56269886
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Active Directory Federation Services (AD FS 2.0)

 

_**Ultima modifica dell'argomento:** 2013-07-03_

Nella sezione seguente viene descritto come configurare Active Directory Federation Services (AD FS 2.0) per il supporto dell'autenticazione a più fattori. Per informazioni su come installare AD FS 2.0, vedere le informazioni dettagliate sulle procedure relative ad AD FS 2.0 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=313374](http://go.microsoft.com/fwlink/p/?linkid=313374).


> [!NOTE]
> Quando si installa AD FS 2.0, non utilizzare Server Manager di Windows per aggiungere il ruolo Active Directory Federation Services, ma scaricare e installare il pacchetto Active Directory Federation Services 2.0 RTW dal sito <A href="http://go.microsoft.com/fwlink/p/?linkid=313375">http://go.microsoft.com/fwlink/p/?LinkId=313375</A>.




**Per configurare AD FS per l'autenticazione a due fattori**

1.  Accedere al computer ADFS 2.0 utilizzando un account di amministratore del dominio.

2.  Avviare Windows PowerShell.

3.  Dalla riga di comando di Windows PowerShell eseguire il comando seguente:
    
        add-pssnapin Microsoft.Adfs.PowerShell

4.  Stabilire una relazione con ogni Director, pool Enterprise e server Standard Edition di Lync Server 2013 con aggiornamenti cumulativi per Lync Server 2013: luglio 2013 che verrà abilitato per l'autenticazione passiva mediante il comando seguente sostituendo il nome del server esistente con il nome del server specifico della distribuzione in uso:
    
        Add-ADFSRelyingPartyTrust -Name LyncPool01-PassiveAuth -MetadataURL https://lyncpool01.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  Dal menu Strumenti di amministrazione avviare la console di gestione di AD FS 2.0.

6.  Espandere **Relazioni di attendibilità** \> **Trust della relying party**.

7.  Verificare che per il pool Enterprise o il server Standard Edition di Lync Server 2013 con aggiornamenti cumulativi per Lync Server 2013: luglio 2013 sia stato creato un nuovo trust.

8.  Eseguire i comandi seguenti per creare e assegnare una regola di autorizzazione al rilascio per il trust della relying party che utilizza Windows PowerShell:
    
    ```
    $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");'
    ```
    ```
    Set-ADFSRelyingPartyTrust -TargetName LyncPool01-PassiveAuth 
    -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    ```

9.  Eseguire i comandi seguenti per creare e assegnare una regola di trasformazione rilascio per il trust della relying party che utilizza Windows PowerShell:
    
    ```
    $IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
    ```
    ```
    Set-ADFSRelyingPartyTrust -TargetName LyncPool01-PassiveAuth -IssuanceTransformRules $IssuanceTransformRules
    ```

10. Nella console di gestione di AD FS 2.0 fare clic con il pulsante destro del mouse sul trust della relying party e scegliere **Modifica regole attestazione**.

11. Selezionare la scheda **Regole di autorizzazione rilascio** e verificare che la nuova regola di autorizzazione sia stata creata correttamente.

12. Selezionare la scheda **Regole di trasformazione rilascio** e verificare che la nuova regola di trasformazione sia stata creata correttamente.

