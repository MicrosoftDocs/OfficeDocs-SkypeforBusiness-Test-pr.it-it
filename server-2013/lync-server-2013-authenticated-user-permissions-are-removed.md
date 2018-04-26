---
title: 'Lync Server 2013: Rimozione delle autorizzazioni degli utenti autenticati'
TOCTitle: Rimozione delle autorizzazioni degli utenti autenticati
ms:assetid: 5fcd70a5-813a-4076-9bb6-5b0d47505038
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398425(v=OCS.15)
ms:contentKeyID: 49300719
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimozione delle autorizzazioni degli utenti autenticati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In un ambiente Active Directory bloccato le voci di controllo di accesso degli utenti autenticati vengono rimosse dai contenitori predefiniti di Active Directory, tra cui il contenitore degli utenti, della configurazione o di sistema, e dalle unità organizzative in cui sono archiviati gli oggetti utente e computer. La rimozione delle voci di controllo di accesso degli utenti autenticati impedisce l'accesso in lettura alle informazioni di Active Directory. La rimozione delle voci di controllo di accesso crea però problemi per Lync Server 2013, in quanto la possibilità o meno per gli utenti di eseguire la preparazione del dominio dipende dall'autorizzazione di lettura per questi contenitori.

In questa situazione l'appartenenza al gruppo Domain Admins, necessaria per la preparazione del dominio, per l'attivazione del server e per la creazione del pool, non concede più l'accesso in lettura alle informazioni di Active Directory archiviate nei contenitori predefiniti. È pertanto necessario concedere manualmente le autorizzazioni di accesso in lettura per diversi contenitori nel dominio radice della foresta per verificare il corretto completamento della procedura di preparazione della foresta, che costituisce un prerequisito.

Per consentire a un utente di eseguire la preparazione del dominio, l'attivazione del server o la creazione del pool in un qualsiasi dominio diverso dal dominio radice della foresta, è possibile scegliere tra le opzioni seguenti:

  - Utilizzare un account membro del gruppo Enterprise Admins per eseguire la preparazione del dominio.

  - Utilizzare un account membro del gruppo Domain Admins e concedere a tale account le autorizzazioni di accesso in lettura per ciascuno dei contenitori seguenti nel dominio radice della foresta:
    
      - Contenitore del dominio
    
      - Contenitore di sistema o della configurazione

Se non si desidera utilizzare un account membro del gruppo Enterprise Admins per eseguire la preparazione del dominio o altre attività di impostazione, è possibile concedere in modo esplicito l'accesso in lettura per i contenitori appropriati nel dominio radice della foresta all'account che si desidera utilizzare.

## Per assegnare agli utenti le autorizzazioni di accesso in lettura sui contenitori nel dominio radice della foresta

1.  Accedere al computer appartenente al dominio radice della foresta utilizzando un account membro del gruppo Domain Admins per il dominio radice della foresta.

2.  Eseguire adsiedit.msc per il dominio radice della foresta.
    
    Se le voci di controllo di accesso degli utenti autenticati sono state rimosse dal contenitore di sistema, del dominio o della configurazione, è necessario concedere autorizzazioni di sola lettura per il contenitore, come descritto nei passaggi seguenti.

3.  Fare clic con il pulsante destro del mouse sul contenitore e quindi scegliere **Proprietà** .

4.  Fare clic sulla scheda **Sicurezza** .

5.  Fare clic su **Avanzate** .

6.  Nella scheda **Autorizzazioni** fare clic su **Aggiungi** .

7.  Digitare il nome dell'utente o del gruppo cui si desidera assegnare le autorizzazioni utilizzando il formato `domain\account name` e quindi fare clic su **OK** .

8.  Nella scheda **Oggetti** fare clic su **Solo l'oggetto specificato** nell'elenco **Si applica a** .

9.  In **Autorizzazioni** fare clic sulla colonna **Consenti** per le seguenti voci di controllo di accesso: **Elenca contenuto** , **Leggi tutte le proprietà** e **Autorizzazioni di lettura** .

10. Fare due volte clic su **OK** .

11. Ripetere queste operazioni per ognuno dei contenitori rilevanti indicati nel passaggio 2.

