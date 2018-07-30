---
title: Configurazione di un proxy inverso per l'individuazione automatica
TOCTitle: Configurazione di un proxy inverso per l'individuazione automatica
ms:assetid: 1e3c3cc2-fe55-408b-99c4-c6e0a9252689
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945619(v=OCS.15)
ms:contentKeyID: 52062107
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di un proxy inverso per l'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2012-12-12_

L'individuazione automatica e il supporto dei client che utilizzano tale servizio richiede la modifica di una regola di pubblicazione Web esistente o la creazione di una nuova regola di pubblicazione Web per il proxy inverso. La modifica o la creazione di una nuova regola di pubblicazione non dipende dalla decisione di aggiornare o meno gli elenchi di nomi alternativi soggetto nei certificati del proxy inverso.

Se si decide di utilizzare HTTPS per le richieste iniziali del servizio di individuazione automatica di Lync Server 2013 e di aggiornare gli elenchi di nomi alternativi soggetto nei certificati del proxy inverso, sarà necessario assegnare il certificato pubblico aggiornato al listener SSL (Secure Sockets Layer) nel proxy inverso. L'aggiornamento richiesto del certificato esterno (pubblico) includerà la voce del nome alternativo soggetto (SAN) per lyncdiscover.\<nome dominio\>. Sarà quindi necessario modificare il listener esistente per i servizi Web esterni o creare una nuova regola di pubblicazione Web per l'URL del servizio di individuazione automatica esterno, ad esempio **lyncdiscover.contoso.com**. Se non si dispone già di una regola di pubblicazione Web per l'URL dei servizi Web di Lync Server 2013 esterni per il pool Front End e il pool di server Director (se sono stati distribuiti i Director), sarà necessario pubblicare una regola anche per questo.


> [!NOTE]
> Il listener e la regola di pubblicazione del proxy inverso possono essere utilizzati sia per i servizi Web esterni che per il servizio di individuazione automatica, purché il certificato assegnato al listener contenga il nome soggetto e i nomi alternativi del soggetto per entrambi. Per informazioni dettagliate sulla configurazione predefinita della regola di pubblicazione e del listener Web, vedere <A href="lync-server-2013-setting-up-reverse-proxy-servers.md">Configurare server proxy inversi per Lync Server 2013</A>.



Se si decide di utilizzare HTTP per le richieste iniziali del servizio di individuazione automatica in modo da non dover aggiornare i nomi alternativi soggetto per il proxy inverso, sarà necessario creare o modificare una regola di pubblicazione Web per la porta 80.

Nelle procedure incluse in questa sezione viene descritto come creare o modificare le regole di pubblicazione Web in Microsoft Forefront Threat Management Gateway 2010 per l'individuazione automatica.


> [!NOTE]
> Tali procedure partono dal presupposto che sia stata installata la Standard Edition di Forefront Threat Management Gateway (TMG) 2010. Se si sta utilizzando un altro proxy inverso, le procedure sono simili, ma devono essere associate alla documentazione del prodotto di terze parti.



## Per creare una regola di pubblicazione Web per l'URL del servizio di individuazione automatica esterno

1.  Fare clic sul pulsante **Start**, scegliere **Programmi**, **Microsoft Forefront TMG** e quindi fare clic su **Forefront TMG Management**.

2.  Nel riquadro sinistro espandere **NomeServer**, fare clic con il pulsante destro del mouse su **Criterio firewall**, scegliere **Nuovo** e quindi fare clic su **Regola di pubblicazione sito Web**.

3.  Nella pagina **Nuova regola di pubblicazione Web** digitare un nome visualizzato per la nuova regola di pubblicazione, ad esempio URLIndividuazioneLync.

4.  Nella pagina **Seleziona azione regola** selezionare **Consenti**.

5.  Nella pagina **Tipo di pubblicazione** selezionare **Pubblica un singolo sito Web o un sistema di bilanciamento del carico**.

6.  Nella pagina **Protezione connessione server** selezionare **Utilizzare SSL per connettersi al server Web pubblicato o alla server farm**.

7.  In **Nome sito interno** nella pagina **Dettagli pubblicazione interna** digitare il nome di dominio completo (FQDN) del pool di server Director, ad esempio lyncdir01.contoso.local. Se si desidera creare una regola per l'URL dei servizi Web esterni nel pool Front End, digitare l'FQDN del pool Front End, ad esempio lyncpool01.contoso.local.

8.  In **Percorso (facoltativo)** nella pagina **Dettagli pubblicazione interna** digitare **/\*** come percorso della cartella da pubblicare e quindi selezionare **Inoltra l'intestazione host originale e non quella effettiva**.

9.  Nella pagina **Dettagli nome pubblico** eseguire le operazioni seguenti:
    
      - In **Accetta richieste per** selezionare **Nome dominio**.
    
      - In **Nome pubblico** digitare **lyncdiscover.***\<dominiosip\>* (URL del servizio di individuazione automatica esterno). Se si desidera creare una regola per l'URL dei servizi Web esterni nel pool Front End, digitare l'FQDN dei servizi Web esterni nel pool Front End (ad esempio lyncwebextpool01.contoso.com).
    
      - In **Percorso** digitare **/\***.

10. In **Listener Web** nella pagina **Scegliere Listener Web** selezionare il listener SSL esistente con il certificato pubblico aggiornato.

11. Nella pagina **Delega autenticazione** selezionare **Nessuna delega, ma il client può eseguire l'autenticazione direttamente**.

12. Nella pagina **Gruppo di utenti** selezionare **Tutti gli utenti**.

13. Nella pagina **Completamento della Creazione guidata regola di pubblicazione Web** verificare che le impostazioni della regola di pubblicazione Web siano corrette e quindi fare clic su **Fine**.

14. Nell'elenco delle regole di pubblicazione Web di Forefront TMG fare doppio clic sulla nuova regola appena aggiunta per aprire **Proprietà**.

15. Nella scheda **Per** eseguire le operazioni seguenti:
    
      - Selezionare **Inoltra l'intestazione host originale e non quella effettiva**.
    
      - Selezionare **Le richieste sembrano provenire dal computer Forefront TMG**.

16. Nella scheda **Bridging** eseguire le operazioni seguenti:
    
      - Selezionare **Server Web**.
    
      - Selezionare **Reindirizza richieste alla porta HTTP** e digitare **8080** come numero di porta.
    
      - Selezionare **Reindirizza richieste alla porta SSL** e digitare **4443** come numero di porta.

17. Fare clic su **OK**.

18. Nel riquadro dei dettagli fare clic su **Applica** per salvare le modifiche e aggiornare la configurazione.

19. Fare clic su **Prova regola** per verificare che la nuova regola sia configurata correttamente.

## Per modificare una regola di pubblicazione Web esistente e aggiungere un nome SAN e un URL del servizio di individuazione automatica esterno

1.  Fare clic sul pulsante **Start**, scegliere **Programmi**, **Microsoft Forefront TMG** e quindi fare clic su **Forefront TMG Management**.
    
    > [!IMPORTANT]  
    > Ripetere la modifica per ogni listener e regola di pubblicazione disponibile. In genere sono disponibili una regola e un listener per i pool Front End e una regola e un listener per i pool di server Director o Server Director facoltativi, se sono stati distribuiti.

2.  Nel riquadro sinistro espandere **NomeServer**, fare clic con il pulsante destro del mouse su **Criterio firewall** e quindi scegliere la regola applicabile. Nella scheda **Attività** fare clic su **Modifica regola selezionata**.

3.  Nella scheda **Nome pubblico** in **Questa regola di applica a** selezionare **Richieste per i seguenti siti Web**.

4.  Fare clic su **Aggiungi**, digitare il nome del nuovo sito di individuazione automatica (ad esempio lyncdiscover.contoso.com) e quindi fare clic su **OK**.

5.  Nella scheda **Listener** fare clic su **Seleziona certificato** e assegnare il nuovo certificato con le voci SAN di individuazione automatica aggiunte. Chiudere le proprietà del listener e di pubblicazione Web.

6.  Nel riquadro dei dettagli fare clic su **Applica** per salvare le modifiche e aggiornare la configurazione.

7.  Fare clic su **Prova regola** per verificare che la nuova regola sia configurata correttamente.

## Per creare una regola di pubblicazione Web per la porta 80

1.  Fare clic sul pulsante **Start**, scegliere **Programmi**, **Microsoft Forefront TMG** e quindi fare clic su **Forefront TMG Management**.

2.  Nel riquadro sinistro espandere **NomeServer**, fare clic con il pulsante destro del mouse su **Criterio firewall**, scegliere **Nuovo** e quindi fare clic su **Regola di pubblicazione sito Web**.

3.  Nella pagina **Nuova regola di pubblicazione Web** digitare un nome visualizzato per la nuova regola di pubblicazione, ad esempio Individuazione automatica Lync (HTTP).

4.  Nella pagina **Seleziona azione regola** selezionare **Consenti**.

5.  Nella pagina **Tipo di pubblicazione** selezionare **Pubblica un singolo sito Web o un sistema di bilanciamento del carico**.

6.  Nella pagina **Protezione connessione server** selezionare **Utilizzare connessioni non protette per connettersi al server Web pubblicato o alla server farm**.

7.  In **Nome sito interno** nella pagina **Dettagli pubblicazione interna** digitare l'FQDN dei servizi Web interni per il pool Front End, ad esempio lyncpool01.contoso.local.

8.  In **Percorso (facoltativo)** nella pagina **Dettagli pubblicazione interna** digitare **/\*** come percorso della cartella da pubblicare e quindi selezionare **Inoltrare l'intestazione host originale e non quella effettiva specificata nel campo Nome sito interno nella pagina precedente**.

9.  Nella pagina **Dettagli nome pubblico** eseguire le operazioni seguenti:
    
      - In **Accetta richieste per** selezionare **Nome dominio**.
    
      - In **Nome pubblico** digitare **lyncdiscover.***\<dominiosip\>* (URL del servizio di individuazione automatica esterno).
    
      - In **Percorso** digitare **/\***.

10. In **Listener Web** nella pagina **Scegliere Listener Web** selezionare un listener Web oppure utilizzare la Creazione guidata definizione listener Web per crearne uno nuovo.

11. Nella pagina **Delega autenticazione** selezionare **Nessuna delega, ma il client può eseguire l'autenticazione direttamente**.

12. Nella pagina **Gruppo di utenti** selezionare **Tutti gli utenti**.

13. Nella pagina **Completamento della Creazione guidata regola di pubblicazione Web** verificare che le impostazioni della regola di pubblicazione Web siano corrette e quindi fare clic su **Fine**.

14. Nell'elenco delle regole di pubblicazione Web di Forefront TMG fare doppio clic sulla nuova regola appena aggiunta per aprire **Proprietà**.

15. Nella scheda **Bridging** eseguire le operazioni seguenti:
    
      - Selezionare **Server Web**.
    
      - Selezionare **Reindirizza richieste alla porta HTTP** e digitare **8080** come numero di porta.
    
      - Verificare che l'opzione **Reindirizza richieste alla porta SSL** non sia selezionata.

16. Fare clic su **OK**.

17. Nel riquadro dei dettagli fare clic su **Applica** per salvare le modifiche e aggiornare la configurazione.

18. Fare clic su **Prova regola** per verificare che la nuova regola sia configurata correttamente.

19. Verificare che l'URL del servizio di individuazione automatica esterno non sia definito in altre regole di pubblicazione Web.

## Vedere anche

#### Concetti

[Configurare server proxy inversi per Lync Server 2013](lync-server-2013-setting-up-reverse-proxy-servers.md)

