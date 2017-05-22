---
title: Clinical | Observation
keywords: usecase, observation
tags: [observation,fhir,rest,clinical]
sidebar: foundations_sidebar
permalink: restfulapis_clinical_observation.html
summary: Clinical Observation
---

{% include search.warnbanner.html %}
{% include profile.html content="[Care Connect Observation](http://www.interopen.org/candidate-profiles/care-connect/CareConnect-Observation-1.html)" %}

## Read ##

<div markdown="span" class="alert alert-success" role="alert">
GET /Observation/[id]</div>

Return a single `Observation` for the specified id

## Search Parameters ##

<div markdown="span" class="alert alert-success" role="alert">
GET /Observation?[searchParameters]</div>

Observation resource contains observation or event information for a patient. Fetches a bundle of all `Observation` resources for the specified patient.

{% include moscow.html content="[Observation](https://www.hl7.org/fhir/DSTU2/observation.html#search)" %}


| Name | Type | Description | SHALL | Path |
|------|------|-------------|-------|------|
| `code` | `token` | The code of the observation type | Y | Observation.code |
| `date` | `date` | Obtained date/time.<br>If the obtained element is a period, a date that falls in the period | Y | Observation.effective[x] |
| `patient` | `reference` | The identity of a patient to list observations for | Y | Observation.subject (Patient) |

{% include search.code.html content="Observation" %}

{% include search.date.html content="Observation" %}

<div class='highlighter-rouge'>
{% include search.patient.html content="Observation" %}
</div>



## Example ##

### curl Request ###

Return all Observation resources for Patient with a logical Id of 1, the format of the response body will be xml. Replace 'baseUrl' to the actual base Url of the FHIR Server.

```curl
curl --get http://[baseUrl]/Observation?patient=1&_format=xml
```

### Response Headers ###

| Status Code |
|----------------|
|200 |

| Header | Value |
|-----------------|---------|
| Content-Type  | application/xml+fhir;charset=UTF-8 |

### Response Body ###

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="ab49bf8e-a805-4b4c-871e-ff7cec75bcb5"/>
    <meta>
        <lastUpdated value="2017-05-18T12:06:52.948+01:00"/>
    </meta>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="http://127.0.0.1:8080/careconnect-dstu2-hapi-ui/Dstu2/Observation?patient=1"/>
    </link>
    <entry>
        <fullUrl value="http://127.0.0.1:8080/careconnect-dstu2-hapi-ui/Dstu2/Observation/4953"/>
        <resource>
            <Observation xmlns="http://hl7.org/fhir">
                <id value="4953"/>
                <meta>
                    <versionId value="1"/>
                    <lastUpdated value="2017-05-18T12:06:03.140+01:00"/>
                    <profile value="http://hl7.org/fhir/StructureDefinition/careconnect-observation-1"/>
                </meta>
                <identifier>
                    <system value="http://fhir.jorvik.nhs.uk/EPR/Observation"/>
                    <value value="878281"/>
                </identifier>
                <status value="final"/>
                <code>
                    <coding>
                        <system value="http://snomed.info/sct"/>
                        <code value="162864005"/>
                        <display value="Body mass index 30+ - obesity"/>
                    </coding>
                </code>
                <subject>
                    <reference value="Patient/1"/>
                </subject>
                <effectiveDateTime value="2012-09-17"/>
                <performer>
                    <reference value="Practitioner/4952"/>
                </performer>
            </Observation>
        </resource>
        <search>
            <mode value="match"/>
        </search>
    </entry>
</Bundle>
```