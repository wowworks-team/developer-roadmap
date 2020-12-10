# Nonfunctional Requirements (NFRs)
## Contents

## Runtime
### Availability
* [NFR101] Maximum allowable system downtime is 2 seconds.

* [NFR102] Releasing incompatible versions of the backend app and the client apps is prohibited.

* [NFR103] The backend app should support both the old and the new version of clients (frontend and mobile) during transition periods. Releasing backend app versions that make any user-side functionality unavailable even for out-of-date clients is prohibited.

* [NFR104] Long-term migrations which cause database lock for more than 60 seconds are prohibited (see the settings/schema/data migrations rules for more info).

* [NFR105] Database rollback should be available during (or after) any scheme migration.

### Reliability
* [NFR206] System should meet all the reliability requirements.

* [NFR207] All system modules should recover automatically after restart.

  * All technical data and the system launch process is fully prescribed in the init scripts of the third-party software which is used ‘as is’ (Nginx, PostgreSQL, etc).

  * Docker containers should start automatically.

  * All required scripts should be described in crontabs.

* [NFR208] All business data should have a backup.

* [NFR209] Each event that affects a business or technical process should be logged. While reviewing system logs, a specialist should be able to look up through the entire sequence of actions in the stacktrace and restore the reasons that led to any of the events.

* [NFR210] User shouldn’t face issues such as internal server error or mobile app crash. No errors in the browser console are allowed. All issues reported by users should be handled properly.

### Data storage
* [NFR301] All business data should be stored in PostgreSQL with unlimited storage time.

* [NFR302] Business logs should have unlimited retention time.

* [NFR303] Nginx log storage rules are established on hosting servers.

* [NFR304] All error logs should be collected and stored in Sentry.

* [NFR305] Debug logs/technical info should be stored in TXT/ELK formats only. Such data should be stored for no longer than 3 days. 

### Scalability
* [NFR401] System should be vertically and horizontally scalable.

* [NFR402] Stateful programming is unwanted. All the code base that’s being added to the project should be stateless.

* [NFR403] Application and databases should be ready to use sharding.

* [NFR404] Frontend and mobile apps should not depend on any certain server address and should support access to different servers.

### Usability
* [NFR501] The interface is easy to learn and navigate; buttons, headings, and help/error messages/notifications are simple to understand.

* [NFR502] Goals are easy to accomplish quickly and with few or no user errors.

More at Design Nonfunctional Requirements (NFRs).

## Security
### Access control
* [NFR601] The system should apply identity and access management.

* [NFR602] Access control is achieved through identification, authentication, authorization, and audit trail.

* [NFR603] The admin role should have maximum rights.

* [NFR604] Other roles should have required minimum of rights.

### Personal data
* [NFR605] Access to personal data should be restricted and secured.

* [NFR606] The volume of requestable personal data should be minimized.

* [NFR607] Personal data should be grouped in one location for easier handling/more safety/deletion/transition to other locations.

* [NFR608] Personal data should be handled in accordance with juridical regulations of countries like the Russian Federal Law on Personal Data (No. 152-FZ)/GDPR/European Union (Withdrawal) Act 2018 and their analogs.

### Reducing external attack risks
* [NFR609] Public access to the services without authorization is strictly limited. All users should pass the identification and be tracked by IP address, user agent, and mobile device ID. The system should have a botnet protection.

* [NFR610] The OWASP top ten security risks should be eliminated or minimized, especially:

* [NFR611] no XSS use cases left;

* [NFR612] no SQL injections use cases left;

* [NFR613] no file injection use cases left.

### Networking
* [NFR614] Opening new ports on the server is not permitted.

* [NFR615] All connections must be authenticated and authorized.

* [NFR616] SSL usage is required.

## Configurability
* [NFR701] All settings should be stored in project parameters and their setup should be provided by dependency injection mechanism. Settings in the project code are prohibited. 

* [NFR702] Frequently changed settings must be configured through the tool in the administrative section of the site.

## Performance
* [NFR801] Page response time should be as short as possible, but less than 3 seconds.

* [NFR802] The system should not show a decrease in overall performance when the number of simultaneously unique users is up to 1000 people.

* [NFR803] RAM usage limit for the system is 128 MB.

* [NFR804] Maximum API request execution time is 10 seconds.

* [NFR805] Maximum database storage increase is 1GB per month.

* [NFR806] Maximum log storage increase is 1GB per month.

## Design & architecture
### Reusability requirements
* [NFR901] The ready-to-publish codebase should be uploaded to Github https://github.com/wowworks-team. 

* [NFR902] Any method used more than 3 times must be moved to a common class.

* [NFR903] A code class should not depend on any framework used in the project when it is possible.

* [NFR904] DRY development pattern should be followed by all developers.

* [NFR905] SOLID design principles should be followed by all developers.

* [NFR906] KISS & YAGNI patterns should be followed by all developers.

* [NFR907] All project components should be ready to be moved to a composer / yarn / gradle package.

### Extensibility
* [NFR1001] Any project functionality in general should be extensible.

### Portability
* [NFR1101] The codebase should be ready for porting to another system/platform/framework.

  * The project code must be consistent with the Onion architecture and meet the Domain-driven design principles.

  * The mobile app dependence on the iOS/Android platform specifics must be as minimum as possible.

  * The backend code should be ready for porting to the symfony framework.

### Interoperability
* [NFR1201] REST API is the software architecture style that defines a set of constraints that will be used to create web services in the project.

* [NFR1202] ISO 8601 standard is used for all the dates in the project.

* [NFR1203] In all other cases, common protocols and industry standards are used.

### Supportability
* [NFR1301] The solution must be backup-ready.

* [NFR1302] The codebase should be easy to read and review.

* [NFR1303] The code should be self-documenting.

* [NFR1304] The code should meet the codestyle.

* [NFR1305] All code used in the project must be in English only.

* [NFR1306] Usage of the current technology stack is preferable. New technologies (e.g. programming languages, software, frameworks) are used only in case of strong need.

  * New dependencies (e.g. in composer/yarn/gradle) should not be added unless absolutely necessary.

  * New libraries (in mobile/frontend/backend) should not be added unless absolutely necessary.

  * New technologies may be implemented only through ansible/dockerfile and package managers (composer/yarn/gradle).

* [NFR1307] All errors/crashes must be tracked by an issue management system.


### Modularity
* [NFR1401] All project modules should be considered as standalone components integrated into one consistent solution.


### Testability
* [NFR1501] The application complex should be testable with all required test methods outlined in the company test plan, which is particularly relevant to unit, integration, functional and acceptance tests.

* [NFR1502] The application complex should be testable in any relevant environment which meets the general requirements for the project.

### Localizability
* [NFR1601] Any user-side information must be translated into the supported project languages, which are:

  * Russian

  * English

  * German

  * Polish

* [NFR1602] Date format must also be localized in all cases.

* [NFR1603] Time zones should be taken into account when the project is running and user information is displayed.

## Useful links
1. https://habr.com/ru/post/231961/ Non-functional requirements to software. Part 1

1. https://maisqual.squoring.com/wiki/index.php/ISO/IEC_SQuaRE ISO/IEC SQuaRE

1. https://en.wikipedia.org/wiki/ISO/IEC_9126 ISO/IEC 9126

1. https://en.wikipedia.org/wiki/List_of_system_quality_attributes
