# Pseudonymisation as a Service
## Advisory services for pseudonymisation techniques and best practiceson, and shaping technology according to data protection and privacy provisions. 

### Taking a risk-based approach to pseudonymisation
Pseudonymisation techniques have their own well understood and intrinsic properties but this does not mean the selection and implementation of an appropriate technique is a trivial task. We provide a risk-based approach to assess the required protection level and consider relevant utility and scalability.

**Data controllers and processors need to carefully consider the implementation of pseudonymisation following a risk-based approach, taking into account the purpose and overall context of the personal data processing, as well as the utility and scalability levels they wish to achieve.**

**Producers of products, services and applications should provide adequate information to controllers and processors regarding their use of pseudonymisation techniques and the security and data protection levels that these provide.**

**Advanced Analytica can provide practical guidance to data controllers and processors with regard to the assessment of the risk, while advising on best practice in the field of pseudonymisation.**

# 1. INTRODUCTION TO THE PSEUDONYMISATION SERVICE

## 1.1 BACKGROUND
Pseudonymisation is a well-known de-identification process that has gained additional attention following the adoption of EU and UK GDPR, where it is referenced as both a security and data protection by design mechanism. **In addition, in the GDPR context, pseudonymisation can motivate the relaxation, to a certain degree, of data controllers’ legal obligations if properly applied.**

## 1.2 SCOPE AND OBJECTIVES

The overall scope of our service is to provide guidance and advise for best practices on the technical implementation of data pseudonymisation.

More specifically, the objectives of the report are as follows: 
  - Discuss different pseudonymisation scenarios and relevant actors involved. 
  - Identify possible pseudonymisation techniques in correlation with relevant adversarial and attack models. 
  - Analyse the application of pseudonymisation to specific types of identifiers, in particular IP addresses, email addresses, usernames and other types of structured data sets (use cases). 
  - Draw relevant conclusions and make recommendations for further work in pseudonymisation. 
  
It should be noted that uses case secenarios are generally based specific types of identifiers (IP addresses, email addresses, and username identifiers in structured data sets) that represent real-life scenarios. At the same time, use cases also reflect diverse requirements with regard to pseudonymisation, i.e. arising from the strict format of IP addresses to the more flexible structure of email addresses and the unpredictable nature of larger datasets. The target audience for our service are data controllers, data processors and producers of products, services and applications, and any other interested party in data pseudonymisation.

## 1.3 SERVICE OUTLINE

The outline of the setvice is as follows:
  - Establishing the terminology used with relevant explanatory remarks where needed.
  - Identifying the pseudonymisation scenario(s) that are or will be engaged in practice.
  - Detailing the adversarial and attack models with regard to pseudonymisation.
  - Selecting the pseudonymisation techniques and policies that are available today.
  - Analysing the application of different pseudonymisation techniques to identifiers (use cases).
  - Providing the conclusions and recommendations for all related stakeholders.

This service focuses on analysing technical solutions for the implementation of GDPR complaince programmes, privacy by design and security of personal data processing.

# 2. TERMINOLOGY 
We present a number of terms that we use as part of our service and are essential to project stakeholder. Some of these terms are based on GDPR, whereas others refer to technical standards or are explicitly defined for the purpose of service delivery.

**Personal Data** refers to any information relating to an identified or identifiable natural person (data subject); an identifiable natural person is one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or to one or more factors specific to the physical, physiological, genetic, mental, economic, cultural or social identity of that natural person (GDPR, art. 4(1)).

**Data Controller** or **Controller** is the natural or legal person, public authority, agency or other body which, alone or jointly with others, determines the purposes and means of the processing of personal data (GDPR, art. 4(7)).

**Data Processor** or **Processor** is the natural or legal person, public authority, agency or other body which processes personal data on behalf of the controller (GDPR, art. 4(8)).

**Pseudonymisation** is the processing of personal data in such a manner that the personal data can no longer be attributed to a specific data subject without the use of additional information, provided that such additional information is kept separately and is subject to technical and organisational measures to ensure that the personal data are not attributed to an identified or identifiable natural person (GDPR, art. 4(5)).

**Anonymisation** is a process by which personal data is irreversibly altered in such a way that a data subject can no longer be identified directly or indirectly, either by the data controller alone or in collaboration with any other party (ISO/TS 25237:2017).

**Identifier** is a value that identifies an element within an identification scheme. A unique identifier is only one element associated with personal data.

**Pseudonym**, also known as cryptonym or just nym, is a piece of information associated to an identifier of an individual or any other kind of personal data (e.g. location data). Pseudonyms may have different degrees of linkability (to the original identifiers). The degree of linkability of different pseudonym types is important to consider for evaluating the strength of pseudonyms but also for the design of pseudonymous systems where a certain degree of linkability may be desired (e.g. when analysing pseudonymous log files or for reputation systems).

**Pseudonymisation Function** , denoted *𝑃*, is a function that substitutes an Identifier *𝐼𝑑* by a Pseudonym *𝑝𝑠𝑒𝑢𝑑𝑜*. 

**Pseudonymisation secret**, denoted *𝑠* is an (optional) parameter of a pseudonymisation function *𝑃*. The function *𝑃* cannot be evaluated/computed if *𝑠* is unknown. Recovery function, denoted *𝑅*, is a function that substitutes a Pseudonym *𝑝𝑠𝑒𝑢𝑑𝑜* by the Identifier *𝐼𝑑* using the pseudonymisation secret *𝑠*. It inverts the pseudonymisation function *𝑃*. 

**Pseudonymisation Mapping Table** is a representation of the action of the pseudonymisation function. It associates each identifier to its corresponding pseudonym. Depending on the pseudonymisation function *𝑃*, the pseudonymisation mapping table may be the pseudonymisation secret or part of it. 

**Pseudonymisation Entity** is the entity responsible of processing identifiers into pseudonyms using the pseudonymisation function. It can be a data controller, a data processor (performing pseudonymisation on behalf of a controller), a trusted third party or a data subject, depending on the pseudonymisation scenario. It should be stressed that, following this definition, the role of the pseudonymisation entity is strictly relevant to the practical implementation of pseudonymisation under a specific scenario. The responsibility for the whole pseudonymisation process (and for the whole data processing operation in general) almost always rests with the controller. 

**Identifier Domain / Pseudonym Domain** refer to the domains from which the identifier and the Pseudonym are drawn. They can be different or the same domains. They can be finite or infinite domains. 

**Adversary** is an entity that tries to break pseudonymisation and link a pseudonym (or a pseudonymised dataset) back to the pseudonym holder(s). Re-identification attack is an attack to  performed by an adversary that aims to re-identify the holder of a Pseudonym.

**Re-identification Attack** is an attack to pseudonymisation performed by an Adversary that aims to re-identify the holder of a pseudonym.

# 3. PSEUDONYMISATION SCENARIOS
Pseudonymisation plays an important role in GDPR as a security measure (art. 32 GDPR), as well as in the context of data protection by design (art. 25 GDPR). The most obvious benefit of pseudonymisation is to hide the identity of the data subjects from any third party (i.e. other than the pseudonymisation entity) in the context of a specific data processing operation. Still, pseudonymisation can go beyond hiding real identities into supporting the data protection goal of unlinkability, i.e. reducing the risk that privacy-relevant data can be linked across different data processing domains. Furthermore, pseudonymisation (being itself a data minimisation technique) can contribute towards the principle of data minimisation under GDPR, for example in cases where the controller does not need to have access to the real identities of data subjects but only to their pseudonyms. Finally, another important benefit of pseudonymisation that should not be underestimated is that of data accuracy.

