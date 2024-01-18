# 

**About arc42**

arc42, the template for documentation of software and system
architecture.

Template Version 8.2 EN. (based upon AsciiDoc version), January 2023

Created, maintained and © by Dr. Peter Hruschka, Dr. Gernot Starke and
contributors. See <https://arc42.org>.

<div class="note">

This version of the template contains some help and explanations. It is
used for familiarization with arc42 and the understanding of the
concepts. For documentation of your own system you use better the
*plain* version.

</div>

<div style="page-break-after: always;"></div>

# Introduction and Goals

Alle relevanten Anforderungen, die Softwarearchitekten und Entwickler brücksichtigen sollen.

## Requirements Overview

<div class="formalpara-title">

**Main Features**

</div>

1. Die App soll 24/7 laufen und verwendbar sein. <br>
2. Nutzer sollen sich registrieren können. <br>
3. Nutzer sollen sich einloggen können. <br>
4. Nutzer sollen Bilder mit Beschreibungen hochladen können. <br>
5. Nutzer sollen Bilder kommentieren und liken können. <br>


## Quality Goals

<div class="formalpara-title">

**1.**

</div>
Quality: Benutzerfreundlichkeit<br>
Motivation: Für Benutzer einfach zu bedienen, für eine positive Benutzererfahrung<br>

<div class="formalpara-title">

**2.**
</div>
Quality: Leistung<br>
Motivation: Die App soll schnell laufen und nicht lange laden, flüssig Bilder hochladen <br>

<div class="formalpara-title">

**3.**

</div>
Quality: Datenschutz<br>
Motivation: Die Sicherheit und Privatsphäre der Benutzer erhalten, da persönliche Bilder geteilt werden<br>


## Stakeholders
<div class="formalpara-title">

**Form**

</div>

Table with role names, person names, and their expectations with respect
to the architecture and its documentation.

| Role/Name   | Contact        | Expectations       |
|-------------|----------------|--------------------|
| *Benutzer* | *\<Benutzer>* | *Individuen die in der App Bilder hochladen, kommentieren und liken.* |
| *Admin* | *\<Admin>* | *Verwalten das Projekt und haben Zugang zu administrativen Funktionen* |
| *Entwickler* | *\<Entwickler>* | *Das Team, das die App entwickelt und aufrechterhält.* |
| *Business Stakeholder* | *\<Stakeholder>* | *Unternehmensleiter, Manager die in den Erfolg der App investieren* |
| *Support Teams* | *\<Support>* | *Anfragen und Probleme von Kunden lösen* |

<div style="page-break-after: always;"></div>

# Architecture Constraints

- Microservices Architektur:
<br> Skalierbare und flexible Architektur, je nach Nutzernzahl und Beliebtheit erweiterbar
- Implementierung in Java und Swift:
<br> Damit Software auf iOS und Android Geräte zugeschnitten ist
- Lizenzierung von Drittanbieter Software:
<br> Integrierung der Pixlr-Bildbearbeitung in die App
- Datenschutz:
<br> App speichert sensible Daten, die von Dritten nur beschränkt sichtbar sein sollen, Profile können privat sein (nur von Freunden sichtbar)
- Datenverschlüsselung:
<br> Sensible Daten zwischen den Kommunikationsschnittstellen gehören verschlüsselt, HTTPS-Verschlüsselung für die Kommunikation zwischen der mobilen App und dem Server

<div class="formalpara-title">

**What are constraints**

</div>
Any requirement that constrains software architects in their freedom of design and implementation decisions or decision about the development process


<div style="page-break-after: always;"></div>

# System Scope and Context

<div class="formalpara-title">

**Inhalt**

</div>

Systemumfang und Kontext grenzen das System von seinen 
Kommunikationspartnern (benachbarte Systeme und Benutzer, = Kontext des Systems) ab. 
Sie spezifizieren dabei die externen Schnittstellen.

Wenn nötig, unterscheidet man den Geschäftskontext (domänenspezifische Eingaben und Ausgaben) 
vom technischen Kontext (Kanäle, Protokolle, Hardware).


## Business Context


<div class="formalpara-title">

**Was stellt es dar?**

</div>

Alle Daten, die mit dem System ausgetauscht werden
<img src="business_context.png">
- Benutzer (Zielgruppe 18-35 Jahre alt) verwenden und interagieren mit der App, um Bilder hochzuladen oder anzusehen
- Über den App Store wird die App heruntergeladen und installiert
- Pixlr wird in die App zur Bildbearbeitung integriert
- Transaktionen, Datenschutz, Abonnements



## Technical Context

<div class="formalpara-title">

**Was stellt es dar?**

</div>

Das System und seine Umgebung, mit der es über technische Schnittstellen verbunden ist.

<img src="technical_context.png">

-   App selbst mit User Interface, Verarbeitung der hochgeladenen Bilder, Zahlung für das Abonnement
-   Benötigt Backend Services um mit dem Server zu verbinden und Datenbank zu verwenden
-   Auch verbunden mit externen Services, wie der Pixlr Bildbearbeitung, die integriert ist in der App


<div style="page-break-after: always;"></div>

# Solution Strategy

<div class="formalpara-title">

**Contents**

</div>

-   Skalierbarkeit: Es wird eine Notwendigkeit geben, große Nutzerzahlen zu bewältigen. Durch Microservices können einzelne Komponenten der Anwendung unabhängig voneinander skaliert werden. 

-   Kontinuierliche Bereitstellung und Auslieferung: Wenn eine neue Funktion im Community-Bereich der Anwendung hinzugefügt wird, kann sie bereitgestellt werden, ohne die gesamte Anwendung erneut bereitstellen zu müssen.


-   Widerstandsfähigkeit: Wenn ein Dienst ausfällt, bedeutet das nicht zwangsläufig, dass die gesamte Anwendung abstürzt.



<div style="page-break-after: always;"></div>

# Building Block View

<div class="formalpara-title">

**Content**

</div>
TODO: fix building block view, add <br>

The building block view shows the static decomposition of the system
into building blocks (modules, components, subsystems, classes,
interfaces, packages, libraries, frameworks, layers, partitions, tiers,
functions, macros, operations, data structures, …) as well as their
dependencies (relationships, associations, …)

This view is mandatory for every architecture documentation. In analogy
to a house this is the *floor plan*.

<div class="formalpara-title">

**Motivation**

</div>

Maintain an overview of your source code by making its structure
understandable through abstraction.

This allows you to communicate with your stakeholder on an abstract
level without disclosing implementation details.

<div class="formalpara-title">

**Form**

</div>

The building block view is a hierarchical collection of black boxes and
white boxes (see figure below) and their descriptions.

![Hierarchy of building blocks](images/05_building_blocks-EN.png)

**Level 1** is the white box description of the overall system together
with black box descriptions of all contained building blocks.

**Level 2** zooms into some building blocks of level 1. Thus it contains
the white box description of selected building blocks of level 1,
together with black box descriptions of their internal building blocks.

**Level 3** zooms into selected building blocks of level 2, and so on.

See [Building Block View](https://docs.arc42.org/section-5/) in the
arc42 documentation.

## Whitebox Overall System

Here you describe the decomposition of the overall system using the
following white box template. It contains

-   an overview diagram

-   a motivation for the decomposition

-   black box descriptions of the contained building blocks. For these
    we offer you alternatives:

    -   use *one* table for a short and pragmatic overview of all
        contained building blocks and their interfaces

    -   use a list of black box descriptions of the building blocks
        according to the black box template (see below). Depending on
        your choice of tool this list could be sub-chapters (in text
        files), sub-pages (in a Wiki) or nested elements (in a modeling
        tool).

-   (optional:) important interfaces, that are not explained in the
    black box templates of a building block, but are very important for
    understanding the white box. Since there are so many ways to specify
    interfaces why do not provide a specific template for them. In the
    worst case you have to specify and describe syntax, semantics,
    protocols, error handling, restrictions, versions, qualities,
    necessary compatibilities and many things more. In the best case you
    will get away with examples or simple signatures.

***\<Overview Diagram>***

Motivation  
*\<text explanation>*

Contained Building Blocks  
*\<Description of contained building block (black boxes)>*

Important Interfaces  
*\<Description of important interfaces>*

Insert your explanations of black boxes from level 1:

If you use tabular form you will only describe your black boxes with
name and responsibility according to the following schema:

| **Name**         | **Responsibility** |
|------------------|--------------------|
| *\<black box 1>* |  *\<Text>*         |
| *\<black box 2>* |  *\<Text>*         |

If you use a list of black box descriptions then you fill in a separate
black box template for every important building block . Its headline is
the name of the black box.

### \<Name black box 1>

Here you describe \<black box 1> according the the following black box
template:

-   Purpose/Responsibility

-   Interface(s), when they are not extracted as separate paragraphs.
    This interfaces may include qualities and performance
    characteristics.

-   (Optional) Quality-/Performance characteristics of the black box,
    e.g.availability, run time behavior, ….

-   (Optional) directory/file location

-   (Optional) Fulfilled requirements (if you need traceability to
    requirements).

-   (Optional) Open issues/problems/risks

*\<Purpose/Responsibility>*

*\<Interface(s)>*

*\<(Optional) Quality/Performance Characteristics>*

*\<(Optional) Directory/File Location>*

*\<(Optional) Fulfilled Requirements>*

*\<(optional) Open Issues/Problems/Risks>*

### \<Name black box 2>

*\<black box template>*

### \<Name black box n>

*\<black box template>*

### \<Name interface 1>

…

### \<Name interface m>

## Level 2

Here you can specify the inner structure of (some) building blocks from
level 1 as white boxes.

You have to decide which building blocks of your system are important
enough to justify such a detailed description. Please prefer relevance
over completeness. Specify important, surprising, risky, complex or
volatile building blocks. Leave out normal, simple, boring or
standardized parts of your system

### White Box *\<building block 1>*

…describes the internal structure of *building block 1*.

*\<white box template>*

### White Box *\<building block 2>*

*\<white box template>*

…

### White Box *\<building block m>*

*\<white box template>*

## Level 3

Here you can specify the inner structure of (some) building blocks from
level 2 as white boxes.

When you need more detailed levels of your architecture please copy this
part of arc42 for additional levels.

### White Box \<\_building block x.1\_\>

Specifies the internal structure of *building block x.1*.

*\<white box template>*

### White Box \<\_building block x.2\_\>

*\<white box template>*

### White Box \<\_building block y.1\_\>

*\<white box template>*

<div style="page-break-after: always;"></div>

# Runtime View

<div class="formalpara-title">

**Inhalt**

</div>
Verhalten und Interaktionen der Blöcke des Systems

## Szenario: Benutzer lädt Bild hoch 

<img src="Runtime_view.png"></img>

-   Ein Bild wird hochgeladen, indem der eingeloggte Nutzer auf dem
Interface den Button zum Hochladen tippt. Dann wird vom Client eine Anfrage an den
Server geschickt, der dann eine Datenbankabfrage auslöst. Dann wird eine Bestätigung über den Upload weitergereicht.

## Szenario: Benutzer registriert einen Account

<img src="Runtime_view2.PNG"></img>

-   Ein Nutzer muss sich registrieren. Dabei werden eingegebene Daten vom Client
entgegengenommen und an den Server gesendet, wo diese validiert werden. Falls die Daten nicht gültig sind, sendet der Server einen Fehler an den Client, was der Nutzer auf seinem Interface sieht. Ansonsten werden die Daten in der Datenbank gespeichert und eine Bestätigung über die erfolgreiche Registrierung zurückgeschickt.


<div style="page-break-after: always;"></div>

# Deployment View
<div class="formalpara-title">

**Inhalt**

</div>
Wie die Software-Teile des Systems auf der Hardware verteilt sind und
wie sie miteinander interagieren, um die App in Betrieb zu setzen.
<div class="formalpara-title">

**CAP-Theorem**

</div>
Die App erfüllt die Partitionstoleranz und Verfügbarkeit, da selbst bei Unterbrechungen die App weiterläuft und immer für Benutzeranfragen verfügbar ist, selbst bei Fehlern des Servers. <br>
Dabei kann die Konsistenz nicht immer erfüllt sein, da nicht garantiert ist, dass alle Nutzer immer die neuesten Daten sehen.

## Diagramm

<img src="deployment_view.PNG"></img>
Das Deployment enthält ein Smartphone, was über eine Mobile App mit Integration der Bildbearbeitungssoftware "Pixlr" zum Server und Backup Server verbunden ist. Diese beiden sind mit der Datenbank verbunden, und halten so das gesamte System aufrecht.

<div style="page-break-after: always;"></div>

# Cross-cutting Concepts
<div class="formalpara-title">

**Inhalt**

</div>
Lösungen und Regulierungen die in mehreren Teilen des Systems wichtig sind, also zu verschiedenen Blöcken gehören.

## *Development Concept*

- Agiles Development: <br>
Verwendung agiler Entwicklungsmethoden, um auf Änderungen der Anforderungen flexibel reagieren zu können.

## *Architecture and Design Patterns*

- Microservice Architektur: <br>
Anwendung unabhängiger Mikrodienste, damit das Projekt skalierbar und flexibel bleibt.
Da die Firma international vertreten ist, hat sie genug Ressourcen, um mit Mikrodiensten zu entwickeln.

## *Safety and Security Concepts*

- Authentifizierung und Authorisation: <br>
Registrierte Benutzer können sich über ihre Benutzerdaten in ihren Account einloggen.

- Automatische regelmäßige Sicherungen: <br>
Die App sichert automatisch regelmäßig alle Benutzerdaten, hochgeladenen Bilder und relevanten Metadaten,
um Datenverlust zu verhindern.

## *User Experience Concepts*

- Intuitive Navigation: <br>
Die App soll intuitiv und einfach bedienbar sein, damit neue Benutzer
auch bei unserer App bleiben und nicht frustriert sind.

<div style="page-break-after: always;"></div>

# Architecture Decisions

- Bildspeicherung und -lieferung <br>
Alternative: Bilder in einem Cloud-basierten Speicherdienst (AWS, Google cloud..) lagern<br>
Entscheidung: Bilder in einer Datenbank speichern (Daten selbst managen) <br>

- Integration Software Drittanbieter (Pixlr)<br>
Alternative: Eigene Bildbearbeitungssoftware entwickeln<br>
Entscheidung: Integration in die Pixlr-API, damit Benutzer die Anwendung nicht verlassen zur Bildbearbeitung<br>

- Umsetzung des Abonnementmodells<br>
Alternative: Umsetzung eines Abonnementmodells von Drittanbietern<br>
Entscheidung: Eigenes benutzerdefiniertes Abonnementmodell entwickeln<br>



<div style="page-break-after: always;"></div>

# Quality Requirements

<div class="formalpara-title">

**Inhalt**

</div>
Alle Qualitätsanforderungen mit einem Baum und Szenarien.


## Quality Tree
<div class="formalpara-title">

**Inhalt**

</div>
Klare und messbare Qualitätsziele, um die gewünschten Eigenschaften des Systems zu definieren.
Mit dem Baum werden diese übersichtlich visualisiert.
<img src="quality_tree.png"></img>

## Quality Scenarios

<div class="formalpara-title">

**Inhalt**

</div>
Qualitätsanforderungen konkretisiert: <br>
Was mit dem System passiert, wenn ein Reiz im System ankommt. Geordnet nach Priorität (oben ist das wichtigste).<br>


- Datenschutz: <br> Der Teamleiter will den Schutz der User gewährleisten, da es sonst zu rechtlichen Problemen kommen könnte. Dies geschieht mittels implementierung der dazu passenden Liabraries und Funktionen bis zum Ende des Projektes.

- Benutzerfreundlichkeit: <br> Ein User will das beim öffnen der App direkt alle wichtigen Features sehen und benutzen können.

- Fehlerbehandlung: <br> Ein Bildupload schlägt aufgrund von Netzwerkausfällen fehl. Die App sollte dem Benutzer eine klare und verständliche Fehlermeldung anzeigen und den Uploadprozess fortsetzen, wenn die Verbindung wiederhergestellt ist.

- Leistung: <br> Ein Benutzer öffnet die App. Die App soll alle neuen Bilder und Daten nach einer so kurzen Ladezeit wie möglich anzeigen.

- Skalierbarkeit: <br> Die Nutzerzahl steigt plötzlich um das Zehnfache an. Die App sollte in der Lage sein, diese zusätzlichen Nutzeranforderungen zu bewältigen, ohne die Leistung oder Antwortzeiten erheblich zu beeinträchtigen.



<div style="page-break-after: always;"></div>

# Risks and Technical Debts
- Datenkonsistenz: Daten sind auf verschiedene Dienste verteilt, weshalb die Sicherstellung von Datenkonsistenz eine Herausforderung darstellen kann.
- Netzwerklatenz: Dienste müssen über ein Netzwerk kommunizieren, was zu geringfügigen Verzögerungen führen kann und sich auf die Leistung der Anwendung auswirken kann.
- Komplexität: Die Verwaltung mehrerer Dienste ist komplex: Überwachung, Protokollierung und Benachrichtigungssysteme sind erforderlich, um einen reibungslosen Betrieb sicherzustellen.


<div style="page-break-after: always;"></div>

# Glossary
TODO: add important terms
<div class="formalpara-title">

**Contents**

</div>

The most important domain and technical terms that your stakeholders use
when discussing the system.

You can also see the glossary as source for translations if you work in
multi-language teams.

<div class="formalpara-title">

**Motivation**

</div>

You should clearly define your terms, so that all stakeholders

-   have an identical understanding of these terms

-   do not use synonyms and homonyms

A table with columns \<Term> and \<Definition>.

Potentially more columns in case you need translations.

See [Glossary](https://docs.arc42.org/section-12/) in the arc42
documentation.

| Term        | Definition        |
|-------------|-------------------|
| *\<Term-1>* | *\<definition-1>* |
| *\<Term-2>* | *\<definition-2>* |
