---
layout: page
title: FITARA Common Baseline Publishing Schema
permalink: /schema/
filename: schema.md
---

| WARNING: Management.cio.gov is planned to be deprecated by September 30, 2022. In the future, please refer to OMB Memo M-15-14 for implementation guidance. Archived content of management.cio.gov can be accessed at its [GitHub repository](https://github.com/WhiteHouse/CIOmanagement). If you have any concerns regarding the deprecation of management.cio.gov, please email ofcio@omb.eop.gov before September 30, 2022. |
| --- |

## Sections
* [Tips for Working with JSON](#tips)
* [Agency FITARA Milestones](#FITARA)
* [DCOI Strategic Plans](#DCOI)
* [Bureau IT Leadership Directory](#bureaus)
* [CIO Governance Board Membership List](#governance)
* [IDC Realized Cost Savings and Avoidance](#savings)

## Tips for Working with JSON <a id="tips"></a>

#### JSON File Format
JSON is a lightweight data-exchange format that is very easy to read, parse and generate. Based on a subset of the JavaScript programming language, JSON is a text format that is optimized for data interchange. JSON is built on two structures: (1) a collection of name/value pairs and (2) an ordered list of values.

Where optional fields are included in a catalog file but are unpopulated, they may be represented by a `null` value. They should not be represented by an empty string (`""`).

The JSON schemas listed on this page are case sensitive. The schemas uses a camel case convention where the first letter of some words within a field are capitalized (usually all words but the first one). While it might seem subtle which characters are uppercase and lowercase, it is necessary to follow the exact same casing as defined in the schema documented here. For example:

* Correct: `firstName`
* Incorrect: `FirstName`
* Incorrect: `firstname`
* incorrect: `FIRSTNAME`

#### Tools for Working with JSON Formats

The following resources contain helpful tools for working with JSON data format:

* [OFCIO General JSON User Guide](/schemaexamples/JSON%20User%20Guide_v6_09_14_16.pdf)

* [Tabular to JSON Converter](http://www.csvjson.com/csv2json): to add a new "row" of data to your agency’s JSON file, first ensure that all of the columns have the correct field names and are arranged in the correct order. In Microsoft Excel: highlight and copy the new data you wish to add to your JSON file, making sure to include the column headings, and paste that data into the box on the left side of the page and click the button saying “Convert”. The right side window will show your data in a basic JSON structure. In order to conform with the schemas below, you might need to make adjustments as necessary to mimic the spacing, indentation, brackets, colons, and quotation markings in the sample.

* [JSON Validator](http://jsonlint.com/): Copy and paste the contents of your updated JSON file into the window and click the “Validate” button. The tool will check whether the data is written correctly. If any brackets, quotation marks, colons, or other markings are missing from your file, these issues will be shown to you in error messages beneath the window.

* [JSON Schema Validator](https://www.liquid-technologies.com/online-json-schema-validator): Using the link to the schema provided on this page, copy and paste the schema text into the window on the left side of the page. Then, copy and paste your valid JSON file in the window on the right. Any errors or missing information will be shown immediately in the space below your JSON file.

## Agency FITARA Milestones <a id="FITARA"></a>

Post a "fitaramilestones.json" file to "agency.gov"/digitalstrategy with the following contents.

First, each milestones JSON document must include a "milestoneDocument" section providing the overall date of last update to the milestones items.

|Field Name| Data Type| Required? | Notes|
| -------- | -------- | --------- | ---- |
| **updatedDate** | String (yyyy/mm/dd) | Yes | |

Then, create an entry for each of your agency's FITARA milestones, providing the following information for each:


|Field Name                        | Data Type                                           | Required? | Notes
--------------                     | --------------                                      | ----------| --------------
**milestoneID**                    | Int (3)                                             | Yes       |
**milestoneDesc**                  | String (500)                                         | Yes       |
**milestoneTargetCompletionDate**  | String (yyyy/mm/dd)                                 | Yes       | JSON doesn't have a "date" type so use a string, but format as 2016/12/25
**milestoneStatus**                | Select: NotStarted, InProgress, Complete, Deferred  | Yes       |
**milestoneStatusDesc**            | String (500)					 | Yes        | Describe in detail agency responses to status (e.g. ongoing actions, dependencies, partial milestones).
**commonBaselineArea**             | Select: budgetFormulation, budgetExecution, acquisition, organizationAndWorkforce,  nonCommonBaseline                                        | Yes        | Common Baseline-related milestones should be associated with one of these areas of the Common Baseline. Data center-related milestones should have commonBaselineArea equal to "nonCommonBaseline".
**dcoiArea**			   | Select: optimization, closures, costSavings, sharedServices, cloudMigration, CIOLeadership, other, nonDataCenter  | Yes  | Data center-related milestones should be associated with one of these concepts from the Data Center Optimization Initiative. The "nonDataCenter" response should be used for milestones that are purely related to the Common Baseline.

#### Agency FITARA Milestones JSON Syntax Example

~~~json
{
  "updatedDate": "2016/07/20",
  "milestones": [
    {
      "milestoneID": 1,
      "milestoneDesc": "Finalize adoption of revised department-wide policy for IT Investment Review Boards",
      "milestoneTargetCompletionDate": "2016/09/01",
      "milestoneStatus": "InProgress",
      "milestoneStatusDesc": "The revised policy is currently under the review of general counsel, expected to clear this stage by the end of May 2016",
      "commonBaselineArea": "acquisition",
      "dcoiArea": "nonDataCenter"
    },
    {
      "milestoneID": 2,
      "milestoneDesc": "Conduct training for department budget officers to share new budget formulation rules including CIO staff",
      "milestoneTargetCompletionDate": "2016/02/01",
      "milestoneStatus": "Complete",
      "milestoneStatusDesc": "65 budget officer staff attended the training, including representatives from 12 agencies.",
      "commonBaselineArea": "budgetFormulation",
      "dcoiArea": "nonDataCenter"
    },
    {
      "milestoneID": 3,
      "milestoneDesc": "Fully install automated monitoring software on all servers in our tiered data center.",
      "milestoneTargetCompletionDate": "2017/02/01",
      "milestoneStatus": "InProgress",
      "milestoneStatusDesc": "Procurement for additional licenses has been finalized with the provider. Installation will begin on-site next month.",
      "commonBaselineArea": "nonCommonBaseline",
      "dcoiArea": "optimization"
    }
  ]
}

~~~

*[Agency FITARA Milestones JSON Schema File](https://management.cio.gov/schemaexamples/FITARAmilestones_schema.json)*

*[Agency FITARA Milestones JSON Example File](https://management.cio.gov/schemaexamples/FITARAmilestones_exampleFile.json)*

## DCOI Strategic Plan Schema <a id="DCOI"></a>

To refresh the Data Center Optimization Initiative (DCOI), OMB is providing updated instructions and schema to agencies.

The DCOI Strategic Plan has the following six required elements:

  1. Planned and achieved performance levels for each optimization metric, by year;
  2. Planned and achieved closures, to be expressed as cumulative values by year;
  3. An optional field to provide an explanation for any optimization metrics and closures for which the agency did not meet the planned level in a previous Strategic Plan;
  4. Planned cost savings on data centers, to be expressed as annual values by year, including:
   a. A description of any initial costs for data center consolidation and optimization; and
  b. Life cycle cost savings and other improvements (if applicable);
  5. Historical costs, cost savings, and cost avoidances due to data center consolidation and optimization through fiscal year 2015; and
  6. A statement from the agency CIO stating whether the agency has complied with all reporting requirements in this memorandum and the data center requirements of FITARA. If the agency has not complied with all reporting requirements, the agency must provide a statement describing the reasons for not complying.

Parts **1 – 5** above are required to be posted publicly in machine-readable JSON format at **[agencyhomepage].gov/digitalstrategy/datacenteroptimizationstrategicplan.json**. NOTE: In order to assist agencies with compiling these plans, OGP and OMB have developed a tool to convert agencies’ text-based plans to a JSON format for this purpose. This can be found at [https://datacenters.cio.gov/reporting/strategic-plan-generator](https://datacenters.cio.gov/reporting/strategic-plan-generator). **DCOI Strategic Plans are due during the spring IDC.**

Part **6** of agencies’ DCOI Strategic Plans may be fulfilled using the template labeled "CIO DCOI Certification Statement Templates" provided below. This statement must be filled out, signed by agencies’ CIOs, and submitted via email to the OFCIO@omb.eop.gov inbox, CC’ing the OMB Agency Liaisons, **Submitted during the spring IDC.**

The DCOI further requires that agencies’ public FITARA Milestones files are updated at their current **[agencyhomepage].gov/digitalstrategy/FITARAmilestones.json** pages to include a minimum of five (5) milestones per fiscal year to be achieved in accordance with the DCOI. The schema and test files associated with the FITARA Milestones collection (located at the top of this webpage) have been updated to reflect this requirement.

[CIO DCOI Certification Statement Templates](https://management.cio.gov/assets/docs/DCOI_StrategicPlans_part6_cioStatement.docx)

**DCOI Strategic Plan Schema:**

| Field Name                          | Data Type                       | Required? | Notes |
--------------                        | --------------                  | ----------| --------------
**optimizationMetrics**                        |                        |           |
**energyMetering**                        |                        |           | Total count of valid data centers with advanced energy metering installed.
fy19Planned                    |  Numeric, 0 - 1000               | Yes       |
fy19Achieved                    |  Numeric, 0 - 1000               | Yes       |
fy20Planned                    |  Numeric, 0 - 1000               | Yes       |
fy20Achieved                    |  Numeric, 0 - 1000               | Yes       |
fy21Planned                     |  Numeric, 0 - 1000               | Yes       |
fy21Achieved			|  Numeric, 0 - 1000		   | Yes       |
fy22Planned                     |  Numeric, 0 - 1000               | Yes       |
fy22Achieved			|  Numeric, 0 - 1000		   | Yes       |
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
**virtualization**                        |                        |           | Total count of virtual hosts (servers + mainframes). Agencies may report systems under their cloud investments towards this total count to more accurately reflect the state of their virtualized portfolio.
fy19Planned                    |  Numeric, 0 - 100000               | Yes       |
fy19Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy20Planned                    |  Numeric, 0 - 100000               | Yes       |
fy20Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy21Planned                     |  Numeric, 0 - 100000               | Yes       |
fy21Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy22Planned                     |  Numeric, 0 - 100000               | Yes       |
fy22Achieved                    |  Numeric, 0 - 100000               | Yes       |
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
**underutilizedServers**                        |                        |           | Total count of underutilized servers.
fy19Planned                    |  Numeric, 0 - 100000               | Yes       |
fy19Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy20Planned                    |  Numeric, 0 - 100000               | Yes       |
fy20Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy21Planned                     |  Numeric, 0 - 100000               | Yes       |
fy21Achieved                    |  Numeric, 0 - 100000               | Yes       |
fy22Planned                     |  Numeric, 0 - 100000               | Yes       |
fy22Achieved                    |  Numeric, 0 - 100000               | Yes       |
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
methodology 			|  String, 0 - 10000              | No      | Optional field to explain the methodology your agency used to arrive at the underutilized servers metric. If the methodology is different between data centers, please explain in the inventory comments field.
**availability**                        |                        |           | (Total Planned Hours Availability - Total Hours of Total Downtime) / Planned Hours of Availability * 100
fy19Planned                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy19Achieved                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy20Planned                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy20Achieved                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy21Planned                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy21Achieved                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy22Planned                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
fy22Achieved                    |  Decimal, 0 - 100               | Yes       | Round to 3 digits to the right of the decimal point (e.g., maximum = 99.999)
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
**closures**                        |                        |           | Total count of valid facilities marked as "closed."
fy16Planned                    	|  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy16Achieved                    	|  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy17Planned                     |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy17Achieved                    	|  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy18Planned                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy18Achieved                    	|  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy19Planned                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy19Achieved                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy20Planned                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy20Achieved                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy21Planned                     |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy21Achieved                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy22Planned                     |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
fy22Achieved                    |  Numeric, 0 - 100000               | Yes       | Must be expressed as cumulative values
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
**costSavings**                        |                        |           | Total cost savings, by year.
fy16Planned                    	|  Decimal, 0 - 100               | Yes       | Must be total amount for **2016 only** expressed in MILLIONS of dollars.
fy16Achieved                    	|  Decimal, 0 - 100               | Yes       | Must be total amount for **2016 only** expressed in MILLIONS of dollars.
fy17Planned                     |  Decimal, 0 - 100               | Yes       | Must be total amount for **2017 only** expressed in MILLIONS of dollars.
fy17Achieved                    	|  Decimal, 0 - 100               | Yes       | Must be total amount for **2017 only** expressed in MILLIONS of dollars.
fy18Planned                    |  Decimal, 0 - 100               | Yes       | Must be total amount for **2018 only** expressed in MILLIONS of dollars.
fy18Achieved                    	|  Decimal, 0 - 100               | Yes       | Must be total amount for **2018 only** expressed in MILLIONS of dollars.
fy19Planned                    |  Decimal, 0 - 100               | Yes       | Must be total amount for **2019 only** expressed in MILLIONS of dollars.
fy19Achieved                    |  Decimal, 0 - 100               | Yes       | Must be total amount for **2019 only** expressed in MILLIONS of dollars.
fy20Planned                    |  Decimal, 0 - 100               | Yes       | Must be total amount for **2020 only** expressed in MILLIONS of dollars.
fy21Planned                     |  Decimal, 0 - 100               | Yes       | Must be total amount for **2021 only** expressed in MILLIONS of dollars.
fy22Planned                     |  Decimal, 0 - 100               | Yes       | Must be total amount for **2022 only** expressed in MILLIONS of dollars.
explanationForUnmetPlannedValue |  String, 0 - 10000              | No      |
costsOfClosures |  String, 5 - 10000              | Yes      |
costsOfOptimization |  String, 5 - 10000              | Yes      |
historicalCostSavings |  String, 5 - 10000              | Yes      |


#### DCOI Strategic Plan JSON Syntax Example

~~~json
{
	"optimizationMetrics": {
		"energyMetering": {
			"fy19Planned": 18,
			"fy19Achieved": 0,
			"fy20Planned": 20,
			"fy20Achieved": 0,
			"fy21Planned": 21,
			"fy21Achieved": 0,
			"fy22Planned": 22,
			"fy22Achieved": 0
		},
		"virtualization": {
			"fy19Planned": 110,
			"fy19Achieved": 0,
			"fy20Planned": 120,
			"fy20Achieved": 0,
			"fy21Planned": 121,
			"fy21Achieved": 0,
			"fy22Planned": 122,
			"fy22Achieved": 0,
			"methodology": "OPTIONAL TEXT"
		},
		"underutilizedServers": {
			"fy19Planned": 100,
			"fy19Achieved": 0,
			"fy20Planned": 25,
			"fy20Achieved": 0,
			"fy21Planned": 21,
			"fy21Achieved": 0,
			"fy22Planned": 22,
			"fy22Achieved": 0
		},
		"availability": {
			"fy19Planned": 99.9,
			"fy19Achieved": 0,
			"fy20Planned": 99.99,
			"fy20Achieved": 0,
			"fy21Planned": 99.99,
			"fy21Achieved": 0,
			"fy22Planned": 99.99,
			"fy22Achieved": 0
		}
	},
	"closures": {
		"fy16Planned": 35,
		"fy16Achieved": 36,
		"fy17Planned": 45,
		"fy17Achieved": 44,
		"fy18Planned": 55,
		"fy18Achieved": 56,
		"fy19Planned": 66,
		"fy19Achieved": 0,
		"fy20Planned": 77,
		"fy20Achieved": 0,
		"fy21Planned": 78,
		"fy21Achieved": 0,
		"fy22Planned": 79,
		"fy22Achieved": 0
	},
	"costSavings": {
		"fy16Planned": 78,
		"fy16Achieved": 79,
		"fy17Planned": 36,
		"fy17Achieved": 37,
		"fy18Planned": 12,
		"fy18Achieved": 13,
		"fy19Planned": 20,
		"fy19Achieved": 0,
		"fy20Planned": 35,
		"fy21Planned": 21,
		"fy22Planned": 21,
		"costsOfClosures": "REQUIRED TEXT",
		"costsOfOptimization": "REQUIRED TEXT",
		"historicalCostSavings": "REQUIRED TEXT"
	}
}

~~~

*[DCOI Strategic Plan JSON Example File](https://management.cio.gov/schemaexamples/DCOI_StrategicPlan_fy2021examplefile.json)*

## Bureau IT Leadership Directory <a id="bureaus"></a>
Each agency is expected to post a JSON file for their Bureau IT Leadership Directory to the following URL path: [agency.gov]/digitalstrategy/bureaudirectory.json

Each dataset should include one record for each agency employee with the title of “chief information officer” or who performs the duties and responsibilities of a CIO but does not necessarily have the title of “CIO.”

| Field Name                          | Data Type                       | Required? | Notes |
--------------                        | --------------                  | ----------| --------------
**bureauCode**                        | Int (2)                         | Yes       |
**firstName**                         | String (50)                     | Yes       |
**lastName**                          | String (50)                     | Yes       |
**employmentType**                    | Select: GS, SES, SL, ST, Other  | Yes       |
**employmentTypeOther**               | String (500)                    | No        | If employmentType "Other" is used, describe the employment type.
**typeOfAppointment**                 | Select: career, political    | Yes       |
**otherResponsibilities**             | String (500)                    | No        |
**evaluationRatingOfficialTitle**     | String (500)                    | Yes       |
**evaluationReviewingOfficialTitle**  | String (500)                    | No        | If a "reviewing official" is used, describe their title.
**keyBureauCIO**                      | Select: Yes, No                 | Yes       | Indicate whether this position is designated by the agency CIO as a “key bureau CIO.” Agency CIOs must provide key bureau CIOs’ rating officials input into the agency-wide critical element(s) described in N1 of the FITARA Common Baseline.

#### Bureau IT Leadership Directory JSON Syntax Example

~~~json
{
    "leaders" : [
        {
            "bureauCode" : "12",
            "firstName" : "Jane",
            "lastName" : "Smith",
            "employmentType" : "GS",
            "typeOfAppointment" : "career",
            "otherResponsibilities": "Optional description of other responsibilities here.  Max length is 500 characters.",
            "evaluationRatingOfficialTitle" : "CIO",
            "evaluationReviewingOfficialTitle" : "Optional Reviewing Official Title here.  Max 500 characters",
            "keyBureauCIO" : "Yes"
        },
        {
            "bureauCode": "33",
            "firstName": "John",
            "lastName": "Doe",
            "employmentType": "SES",
            "typeOfAppointment": "political",
            "evaluationRatingOfficialTitle": "CFO",
            "keyBureauCIO": "No"
        }
    ]

}
~~~

*[Bureau IT Leadership Directory JSON Schema](https://management.cio.gov/schemaexamples/bureauITLeadershipSchema.json)*

## CIO Governance Board Membership List <a id="governance"></a>

Each agency is expected to post a JSON file for their CIO Governance Board Membership List to the following URL path: [agency.gov]/digitalstrategy/governanceboards.json

Include all governance boards the CIO is a member of. Agencies shall keep this list up to date at least annually beginning in April 2016.


| Field Name                          | Data Type                       | Required? | Notes |
--------------                        | --------------                  | ----------| --------------
**governanceBoardName**               | String (100)                    | Yes       | Name of governnance board
**programCodeFPI**                    | String (7)                      | No        | Code of Program that board is related to (Federal Program Inventory), if available
**bureauCode**                        | Int (2)                         | Yes       | Bureau that board is a part of, if at bureau-level or within-bureau board. Otherwise indicate “00”
**cioInvolvementDescription**         | String (500)                    | No        | Brief description of CIO involvement

#### CIO Governance Board Membership List JSON Syntax Example

~~~json
{
    "boards" : [
        {
            "governanceBoardName" : "Committee for Naming Oversight",
            "programCodeFPI" : "005-001",
            "bureauCode" : "12",
            "cioInvolvementDescription" : "Optional Reviewing Official Title here.  Max 500 characters"
        },
        {
            "governanceBoardName" : "Committee of Planning",
            "bureauCode" : "10"
        }
    ]

}
~~~

*[CIO Governance Board Membership JSON Schema](https://management.cio.gov/schemaexamples/governanceBoardSchema.json)*

## IDC Realized Cost Savings and Avoidance <a id="savings"></a>

On October 23, 2015 agency points of contact were sent their ITOR strategies already converted to JSON format.

OMB asks agency submitters to:

1. Check the information in the file for accuracy;
2. Update it with any new savings strategies;
3. Fill-out any missing information in the required “strategyId” and “ombInitiatives” fields;
4. Fill-out the “netOrGross” field for all savings amounts, indicating whether each year’s amount is “Net” of costs (equal to gross cost savings/avoidance achieved minus implementation costs required to achieve the savings) or “Gross” (meaning, ignoring any costs of implementation); and
5. Post your finished file on your agency’s [agency.gov]/digitalstrategy/costsavings.json

Before the close of the IDC quarter, identifying the JSON dataset as “[Agency] IT Reform Cost Savings/Avoidance” in your Enterprise Data Inventory and Public Data Listings. Your agency should update this data on a rolling basis as savings are realized, and must ensure that the file is updated with all savings realized in a given quarter during the week prior to the IDC collection deadline.




| Field Name                        | Data Type                                                                 | Required? | Notes |
--------------                      | --------------                                                            | ----------| --------------
**strategyID**                      | Int (3)                                                                   | Yes       | The unique identifier for the strategy
**strategyTitle**                   | String (100)                                                              | Yes       | The title of the strategy
**decisionDate**                    | Date (MM/DD/YYYY)                                                         | Yes       | The date the agency decided to use this strategy
**ombInitiative**                   | Select: Data Center, Digital Services, Commodity IT, PortfolioStat, Software License Management, Other | Yes       | The primary OMB initiative that categorizes this strategy
**relatedUIIs**                     | String (200)                                                              | No        | Related investments to the strategy, identified as their Unique Investment Identifiers (UIIs)
**useOfSavingsAvoidance**           | String (500)                                                              | No        | Explain what the resultant savings will be used for, or how it will be repurposed
**amountType**                      | Select: Cost-savings, Cost-avoidance, Both                                | Yes       | Indicate whether the amounts given for each strategy are cost-savings, cost-avoidance, or both as defined in [OMB Circular A-131](https://www.whitehouse.gov/omb/circulars_a131).
**fy2012**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY12, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                        | Yes       | Indicate whether the FY 12 amount is net of costs, or gross
**fy2013**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY13, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                        | Yes       | Indicate whether the FY 13 amount is net of costs, or gross
**fy2014**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY14, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                        | Yes       | Indicate whether the FY 14 amount is net of costs, or gross
**fy2015**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY15, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                         | Yes       | Indicate whether the FY 15 amount is net of costs, or gross
 **fy2016**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY16, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                         | Yes       | Indicate whether the FY 16 amount is net of costs, or gross
 **fy2017**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY17, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                         | Yes       | Indicate whether the FY 17 amount is net of costs, or gross
  **fy2018**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY18, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                         | Yes       | Indicate whether the FY 18 amount is net of costs, or gross
 **fy2019**                          |                                                                           |           |
 *amount*                           | Numeric, 1-1000                                                           | Yes       | _Realized_ total savings for each strategy for FY19, **in MILLIONS of dollars**
 *netOrGross*                       | Select: Net, Gross                                                         | Yes       | Indicate whether the FY 19 amount is net of costs, or gross

#### IDC Cost Savings and Avoidance JSON Syntax Example

~~~json
{
	"strategies": [{
		"strategyId": 5,
		"strategyTitle": "Blanket Purchase Agreement",
		"decisionDate": "04/12/2011",
		"ombInitiative": "PortfolioStat",
		"useOfSavingsAvoidance": "These savings will be reinvested in existing major investments, as determined by business needs.",
		"amountType": "Cost-Avoidance",
		"relatedUIIs": [
			"099-000002345",
			"099-000000123"
		],
		"fy2012": {
			"amount": 4,
			"netOrGross": "Net"
		},
		"fy2013": {
			"amount": 2.17,
			"netOrGross": "Net"
		},
		"fy2014": {
			"amount": 5,
			"netOrGross": "Gross"
		},
		"fy2015": {
			"amount": 0.25,
			"netOrGross": "Net"
		},
		"fy2016": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2017": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2018": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2019": {
			"amount": 0,
			"netOrGross": "Net"
		}
	}, {
		"strategyId": 6,
		"strategyTitle": "Document Management System (DMS)",
		"decisionDate": "12/01/2012",
		"ombInitiative": "Commodity IT",
		"amountType": "Cost-Savings",
		"fy2012": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2013": {
			"amount": 0.79,
			"netOrGross": "Net"
		},
		"fy2014": {
			"amount": 0.699,
			"netOrGross": "Net"
		},
		"fy2015": {
			"amount": 0.667,
			"netOrGross": "Gross"
		},
		"fy2016": {
			"amount": 2,
			"netOrGross": "Net"
		},
		"fy2017": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2018": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2019": {
			"amount": 0,
			"netOrGross": "Net"
		}
	}, {
		"strategyId": 3,
		"strategyTitle": "Legacy System Upgrade",
		"decisionDate": "12/01/2012",
		"ombInitiative": "Digital Services",
		"useOfSavingsAvoidance": "To be determined in forthcoming review board meeting.",
		"amountType": "Cost-Avoidance",
		"relatedUIIs": [
			"099-000003000"
		],
		"fy2012": {
			"amount": 1.2,
			"netOrGross": "Net"
		},
		"fy2013": {
			"amount": 1.2,
			"netOrGross": "Net"
		},
		"fy2014": {
			"amount": 1.2,
			"netOrGross": "Net"
		},
		"fy2015": {
			"amount": 1,
			"netOrGross": "Net"
		},
		"fy2016": {
			"amount": 0.25,
			"netOrGross": "Net"
		},
		"fy2017": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2018": {
			"amount": 0,
			"netOrGross": "Net"
		},
		"fy2019": {
			"amount": 0,
			"netOrGross": "Net"
		}
	}]
}
~~~

*[IDC Cost Savings and Avoidance JSON Schema](https://management.cio.gov/schemaexamples/costSavingsAvoidanceSchema.json)*

*[IDC Cost Savings and Avoidance JSON Example File](https://management.cio.gov/schemaexamples/IDC%20Cost%20Savings%20Example%20FY%202017.txt)*

*[OFCIO JSON User Guide for Realized Cost Savings](https://management.cio.gov/schemaexamples/JSON%20User%20Guide_v6_09_14_16.pdf)*
