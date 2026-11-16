> **Hinweis / Notice:** Please read the [Disclaimer](#disclaimer) / [Haftungsausschluss](#haftungsausschluss) at the end of this README before using this software.

## Table of Contents

* [Introduction](#Introduction)
* [Requirements](#Requirements)
* [Pre-Configuration](#Pre-Configuration)
* [Error numbers](#Errors)
* [Revision History](#Revision-History)

<a name="Introduction"></a>

## Introduction

This is a library "mod_cfg" for reading and writing from a configuration file. The configuration file should be a plain text file with the following format

``` 
# ------------------------------------------------------------------------------
# Machine configuration
Password=topsecretpass
MaxSpeed=123
MinTemperature=1.234
```

The first value is the entry name followed by the data. The library reads and writes data as string. Number variables must be converted accordingly. The configuration file can be stored on the user partition on the PLC. The project also contains a sample task, config file and mappView visualization for demo purpose.

![](Logical/mappView/Resources/Media/screenshot_main.png)

The library contains only one function call "fct_cfg" that receives a pointer to a variable structure. The type of this structure is "cfg_typ". The structure includes all necessary parameters and has following members:

<table>
  <tr style="font-weight:bold" >
    <th>Name</th>
    <th>Level Description</th>
  </tr>
  <tr>
   <td>read</td>
   <td>Read a configuration entry</td>
  </tr>
  <tr>
   <td>write</td>
   <td>Write a configuration entry</td>
  </tr>
    <tr>
   <td>device</td>
   <td>File device name as pointer</td>
  </tr>
    <tr>
   <td>file_name</td>
   <td>File name as pointer</td>
  </tr>
    <tr>
   <td>entry</td>
   <td>Name of the entry as string</td>
  </tr>
    <tr>
   <td>data</td>
   <td>Entry data as string for read command or new data for write command</td>
  </tr>
    <tr>
   <td>option</td>
   <td>On write command create new entry if it does not exist</td>
  </tr>
    <tr>
   <td>internal</td>
   <td>Internal data structure</td>
  </tr>

</table>

<a name="Requirements"></a>

## Requirements

* Automation Studio 4.7
* Automation Runtime C4.73

Recommended task class is #8 with a 10ms cycle time.

<a name="Pre-Configuration"></a>

## Pre-Configuration
The sample can be pre-configured through the following constants located in 
mappFileExplorer->ExplorerVariables.var

| Constant | Default | Text |
|---|---|---|
| BUFFER_SIZE | 100000 | Maximum size of the buffer and therefore the limit for the file size |
| DATA_SIZE | 200 | Maximum length of one entry |
| ENTRY_SIZE | 50 | Size of the entry name string |

<a name="Errors"></a>
## Error
The function returns the status of the command. This is busy (65535) while the command is running and 0 when the command was finished succesful. The function generates the following error codes.

| No | Constant | Text |
|---|---|---|
| 50000 | ERR_DEVICE_EMPTY | Device name is empty |
| 50001 | ERR_ENTRY_EMPTY | Entry name is empty |
| 50010 | ERR_FILE_SIZE | Config file size exceeds buffer size, increase BUFFER_SIZE |
| 50011 | ERR_BUFFER_SIZE | New data exceeds the buffer size, increase BUFFER_SIZE |
| 50012 | ERR_DATA_SIZE | Read data exceeds the size of the data variable, increase DATA_SIZE |
| 50020 | ERR_ENTRY_NOT_FOUND | Entry was not found in file |

All other error numbers are generated from included libraries that can be found in the Automation Studio help.

<a name="Revision-History"></a>

## Revision History

#### Version 1.0

* Initial commit

# Disclaimer
* License: The source code for this software is provided in this repository under the MIT License—with the consent of the author and B&R Industrie-Elektronik GmbH, which, pursuant to Section 69b of the German Copyright Act (UrhG), is entitled to exercise the economic rights regarding the software. Third-party components are subject to their respective licenses. B&R products are not covered by this license and require a separate license.
* Not a Product: Neither the author, the repository owner, B&R Industrie-Elektronik GmbH, nor any other companies within the ABB Group sell the content provided here as a product. It is provided free of charge and not as part of any commercial business activity. The content of this repository is not maintained as a commercial software product and should not be regarded as such.
* No Support: No support is offered or provided for the program or the codebase. There is no maintenance, no ad-hoc bug fixing, no provision of updates (including security updates) or further development, and there are no guaranteed response times.
* No Warranty: The software is provided "as is"—without any express or implied warranties of any kind. The user is solely responsible for the use of the software.
* No Guarantee: No guarantees are made—specifically regarding fitness for a particular purpose, the absence of errors, the absence of third-party rights, or the completeness or accuracy of the code, its functionality, the documentation, or any other provided content.
* Liability: The liability disclaimer set forth in the MIT License applies to the fullest extent permitted by law. Mandatory statutory liability (e.g., for intent, injury to life, body, or health, or under the Product Liability Act) remains unaffected.
* Trademarks: B&R, Automation Studio, Automation Runtime, mappView, mappService, mappMotion, and Safety+ are trademarks of B&R Industrial Automation GmbH or a company within the ABB Group. No trademark rights are granted.
* In the event of any discrepancies between the German and the English version, the German version shall prevail.

# Haftungsausschluss
* Lizenz: Der Quellcode dieser Software wird in diesem Repository unter der MIT-Lizenz zur Verfügung gestellt – mit Zustimmung des Autors und der B&R Industrie-Elektronik GmbH, die gemäß § 69b UrhG zur Ausübung der vermögensrechtlichen Befugnisse an der Software berechtigt ist. Komponenten Dritter unterliegen ihren jeweiligen Lizenzen. Produkte von B&R sind nicht Gegenstand dieser Lizenz und bedürfen einer eigenen Lizenz.
* Kein Produkt: Weder der Autor, der Inhaber des Repositorys, noch die B&R Industrie-Elektronik GmbH oder andere Gesellschaften der ABB-Gruppe verkaufen die hier bereitgestellten Inhalte als Produkt. Die Bereitstellung erfolgt unentgeltlich und nicht im Rahmen einer Geschäftstätigkeit.  Die Inhalte dieses Repositorys werden nicht als kommerzielles Softwareprodukt gepflegt und sollten auch nicht als solches betrachtet werden.
* Kein Support: Für das Programm und die Codebasis wird kein Support angeboten oder geleistet. Es erfolgt keine Wartung, keine Fehlerbehebung auf Anfrage, keine Bereitstellung von Updates (einschließlich Sicherheitsupdates) oder Weiterentwicklung und es gibt keine garantierten Reaktionszeiten.
* Keine Gewährleistung: Die Software wird „wie besehen“ („as is“) bereitgestellt – ohne jegliche ausdrückliche oder stillschweigende Gewährleistung. Der Nutzer ist für die Verwendung der Software allein verantwortlich.
* Keine Garantie: Es wird keine Garantie übernommen, insbesondere nicht für die Eignung für einen bestimmten Zweck, Fehlerfreiheit oder Freiheit von Rechten Dritter, sowie die Vollständigkeit oder Richtigkeit – weder in Bezug auf den Code und dessen Funktionalität noch in Bezug auf die Dokumentation oder andere bereitgestellte Inhalte.
* Haftung: Es gilt der Haftungsausschluss der MIT-Lizenz, soweit gesetzlich zulässig. Zwingende gesetzliche Haftung (e.g. Vorsatz, Verletzung des Lebens, des Körpers oder der Gesundheit sowie nach dem Produkthaftungsgesetz)  bleibt unberührt.
* Marken: B&R, Automation Studio, Automation Runtime, mappView, mappService, mappMotion, Safety+ sind Marken der B&R Industrial Automation GmbH bzw. einem Unternehmen der ABB-Gruppe. Es werden keine Markenrechte eingeräumt.
* Im Falle von Abweichungen zwischen der deutschen und der englischen Fassung hat die deutsche Fassung Vorrang.
