*This guide explains how to properly fill out a JSON file in the European Cloud Industry repository. It contains both content and syntax errors to avoid and enumerates the elements of JSON files, the syntax, and the correct format to follow. In the first two sections the guideline explains the do's and don'ts  and the list of elements that needs to be clarified when writing compliant JSON files. The last sections specifies JSON files according to FDL standard.*

### 1. List of unclear elements

* category_list and category: how to ensure that a software or a hardware category is correct and how to find the correct information
* Can a solution have multiple categories
* licence_list: what to do when we don't find a license for a solution
* source_code_profile: how to find the source code if it's not on Github.

### 2. List of errors to avoid

Common syntax errors: 

* Ending each entry with a semicolon
* Putting a comma in front of a closed bracket},{ or }]
* Putting brackets when there is no element
* Putting spaces between numbers in KPIs
* Putting geographical coordinates between quotation marks (" ")
* JSONlint doesn't recognise duplicates

Here's a Python script you can run to check the syntax of the json files:

```
#!/usr/bin/env python3

import glob, json, os

for fn in glob.glob("*.json"):

    try:
        d = json.load(open(fn))
    except:
        print(fn)
```

Content errors: 

* Confuse success_cases and references 
* Copy information, notably KPIs from unreliable websites
* Not mentioning the company type
* Not adding company coordinates
* Not mentioning any success case

## 3- Guidelines for a high quality JSON file

* Make sure to understand JSON language and how it works (read https://www.json.org/json-en.html)
* Please refer to the example on Github (https://github.com/Fonds-de-Dotation-du-Libre/european-cloud-industry/blob/master/example/empty.json) to start from a correct JSON syntax
* Define the creation date of the JSON file in "created" input with ISO standard (YYYY-MM-DD)
* Define industry type (see industry type below)
* Define all company information such as title, address, postal_code, city, country, phone_contact, mail_contact, coordinate_list, subsidiary_list, website_url
* Define company KPIs from a reliable website (List of validated sources for financial data below)
* Define at least 50% of companies' solutions (software, hardware)
* Define solution_category for every solution, it must have the same categories as "similar_solutions_list" 
* Find at least an alternative solution for each solution described (use Openhub and Google)
* Define a solution license by referring to Github or Openhub (see the licence syntax below)
* Define a source_code_download using Github, Gitlab or an equivalent for every solution
* Define a source_code_profile (code analysis including the language, line numbers, date, etc.) by referring to Openhub 
* Add references; a list of the company client names including client name, industry, country, and solution 
* Add logo URL if it's available
* Add success cases; list of company clients that published an article about the successful implementation of the solution including the title of the article, a brief description of the article, image_url, industry, customer, country, language, and a sucess_case_url
* At least one reference or success case for every solution
* A success case without an article is a reference, a reference with an article is a success case
* Do not duplicate success cases in references
* Before saving a JSON file, check it with jsonlint (https://jsonlint.com/).

## Classification of values 

For industry types (type) :

* Company;
* NGO;
* Government;
* Individual;
* Other.

For license types: use "licence keywords" from Github (https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository) 

* afl-3.0
* apache-2.0
* ...

List of validated sources for financial data:

* verif.com (FR); 
* societe.com (FR);
* bundesanzeiger.de '(DE);
* find-and-update.company-information.service.gov.uk (GB).

Possible solution_category 

* Storage and database 
* Compute virtualisation 
* Desktop virtualisation
* vRan 
* Operation management 
* Service lifecycle automation
* Networking
* Identity
* Cybersecurity
* Application
* Workspace
* Developer environment 
* Developer API
* Communication 
* IoT and industrial 
* Big Data Hub
* Server
* Switch
* Router
* Rack
* Cooling
* CPU
* Radio

Industrial categories 

- Academia and Research
- Agriculture and Food
- Associations and NGOs
- Aviation and Aerospace
- Automotive
- Banking and Finance
- Chemicals
- Commerce and Retail
- Construction
- Consulting and Training
- Defense
- Education
- Energy and Utilities
- Health and Life Sciences
- Housing and Real Estate
- Insurance
- Information Technology
- Manufacturing
- Media and Entertainment
- Public Administration and Government
- Telecommunication
- Transport
- Travel and Tourism

ISO Standards

Country codes: https://www.ncbi.nlm.nih.gov/books/NBK7249/

Language codes: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes

International telephone codes list: https://fr.wikipedia.org/wiki/Liste_des_indicatifs_t%C3%A9l%C3%A9phoniques_internationaux_par_pays

Currency codes : https://fr.iban.com/currency-code


## Syntax

Telephone Contact
| |phone_contact |  
| :------------- | :-----|  
| Format | "+", followed by the country's international telephone code, followed by " ", followed by the phone number in the country, all between quotation marks.|  
| Example | "+33 629 02 44 25"
|Guide|[List of international telephone codes by country](https://fr.wikipedia.org/wiki/Liste_des_indicatifs_t%C3%A9l%C3%A9phoniques_internationaux_par_pays)  [UIT-T E.123](https://www.itu.int/rec/dologin_pub.asp?lang=e&id=T-REC-E.123-198811-S!!PDF-F&type=items) 


GPS Coordinates

| |coordinate_list |  
| :------------- |:-----|  
| Format | Geographic coordinates in square brackets, without quotation marks inside.|  
| Example |[50.64449017329376, 3.077437939381641]
|Guide|  Right click on the icon designating the location of the company in google maps


Headquarters location

|         |country            |
| :------------- |:-----|
| Format     | ISO country code in upper case between quotation marks |
| Example      | "FR" ou "LU"       |
|Guide |[ISO country codes list](http://www.ncbi.nlm.nih.gov/books/NBK7249/)|

Company performance indicators
|         |KPI            |
| :------------- |:-----|
| Format     | Value followed by a space, followed by currency code of the country in upper case, all between quotation marks |
| Example      | "1000 EUR"       |
|Guide |[List of ISO currency codes by country](https://fr.iban.com/currency-codes)|

Categories list
|         |category_list            |
| :------------- |:-----|
| Format     | A category in quotation marks, followed by a comma, followed by another category or more, all between brackets. |
| Example      | ["Cybersecurity", "Application"]       |
| Guide | See possible values for solution_category. A solution can have one or more categories |

License list

|         |license_list           |
| :------------- |:-----|
| Format     | One license between quotation marks, followed by a comma, followed by one or more licenses, all in square brackets |
| Example      | ["afl-3.0", "apache-2.0"] |
| Guide | [License Keyword of Github](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)      |

Solution source code (for solutions that publish their source code)

|         |source_code_download            |
| :------------- |:-----|
| Format     | Github repository URL |
| Example      | "[https://lab.nexedi.com/nexedi/erp5.git](https:/lab.nexedi.com/nexedi/erp5.git)"
|Guide| Search source codes on [Github](https://github.com/)       |

Satistics of source code (for open source solutions)

|         |source_code_profile            |
| :------------- |:-----|
| Format     | Openhub repository URL |
| Example      | "[https://www.openhub.net/p/erp5](https:/www.openhub.net/p/erp5)"
|Guide| Search source code profile on [Openhub](https://www.openhub.net/)       |

Free Libre Open Source software
|         | FLOSS software             |
| :------------- |:-----|
| Format     | Possible values includes true or false must not be put between quotation marks and must not include upper case letters |
| Example      | true or false
|Guide| Research on the company's website if the commercial support section is available       |

Commercial support open source version, if it exists
|         | commercial_support_open_source_version             |
|:------------- |:-----|
| Format     | Possible values includes true or false must not be put between quotation marks and must not include upper case letters |
| Example      | true or false |
|Guide| Research on the company's website if the commercial support section is available       |

commercial support available

|         | commercial_support_available  |
|:------- |:-------|
| Format  | Possible values that include yes or no must not be put between quotation marks and must not include upper case letters |
| Example | true or false |                          
| Guide   | Research on the company's website if the commercial support section is available       |
