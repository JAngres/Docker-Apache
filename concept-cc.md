## Unterrichtseinheit Cloud Computing
### Verwendete Betriebssysteme für die Hosts
|OS|Version|
|---|---|
|Windows|10 Pro|
|Ubuntu|22 LTS|

### Grobplanung
1) Grundbegriffe Cloud Computing 
   * Präsentation AZ900:1
   * **AB_1: Multiple Choice Fragen**
   * _optional_: Azure Rechenzentrum erkunden
   * **AB_1a: Rechenzentrum, USV**
2) Software as a Service (SaaS)
   * Pizza as a Service, Auto as a Service
   * **AB_2: Software as a Service**
3) Azure Portal Struktur
   * Login am [Portal][az-portal], Navigation
   * Subscriptions, Ressourcengruppen, Ressourcen
4) Migrationsplanung **Gf Store** 
   * Planung der Topologie (_Packet Tracer_)
   * Kostenschätzung mit [Preisrechner][az-preisrechner]
   * **AB_3: Preisrechner**
5) Virtuelle Maschinen als Ressource anlegen
   * Exkurs: _JSON_
   * Template für eine VM anlegen
   * **AB_4: Azure VM erstellen**
   * **AB_5: Azure CLI verwenden, JSON**
6) Migration **Gf Store**
   * Domänencontroller anlegen und konfigurieren
   * Backup DC erstellen (ohne GUI)
   * **AB_6: Domäne in Azure erstellen**
   * _optional_: Azure Active Directory 
   Synchronisation
   * **AB_6a: Azure AD Integration**
7) Webshop anlegen
   * Funktionalitäten eines Webshops
   * _OpenCart packaged by Bitnami_
   * **AB_7: Webshop Deployment mit Azure**
8) Website des **Gf Store**
   * Konzept Continuous Integration / Continuous Delivery
   * Docker Container vs. Virtuelle Maschine
   * Website entwickeln
   * **AB_8: Azure CI/CD**
   * Bereitstellen eines Tauschordners
   * **AB_9: Azure File Share**
   * Anlegen einer SQL Datenbank. Verknüpfung mit einer Web App.
   * **AB_10: Azure SQL Datenbank**
   
9) _Optional_: 
   * Entwicklung eines Chatbots für die Website von **Gf Store**. 
    

[az-preisrechner]: https://azure.microsoft.com/de-de/pricing/calculator/
[az-portal]: https://portal.azure.com
