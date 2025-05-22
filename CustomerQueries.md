## 📘 Frequently Asked Questions
---

### The data that Caplight has used is missing the 'valuation' figures for the funding rounds
Valuation is based on the availability of data in the media articles for all the geographies. In case, we do not have the data, this will not be covered Secondly, very limited geographies (India, UK, Denmark) have information in the documents based on which the valuation is calculated from our end. If the geography is not a part of the coverage or the information in the documents is insufficient, we will not have valuation mapped or reported.

### Captables API was not working for them
Issue with Endpoint, wrong endpoint used

### How can I understand the response provided by the Financials API?
The Financials API response is structured as a key-value mapping, where each field represents a financial metric and its corresponding value. However, the specific data points are not standardized and can vary significantly across different companies and industries. As a result, not all fields will be available for every company. For clarity on the available fields and their values, it is recommended to refer to the platform interface for a visual reference.

### Client has highlighted that our Angel Investor data coverage is poor They have mentioned considering switching to other data providers where coverage is better Client's expectation is to improve the data coverage. The data points where the coverage is expected to be improved : Work Experience Investment Portfolio Client is considering co-working to improve coverage
Shared the list to My Analyst for curation

### Client wants to get the data curated for 153 company domains Client wants to get the data updated for the below points: Funding Details Founder & Key People Contact Details Basic Details Company Sector
Shared the list to My Analyst for curation

### Wants to check response field which denotes when was a company added in Tracxn Database
Exposing "created date" field in companies API

### Required total number of companies related to News API
Used aggregation in News API

### Can I retrieve all legal entity names and their CIN numbers by searching with a company name?
Yes, you can retrieve legal entity names and their corresponding Corporate Identification Numbers (CIN) by searching with a company domain. The API supports filtering using the domain under the associationsName field. Use the following endpoint to search for related legal entities: : /api/3.0/legalentities Example request using domain: { "filter": { "associationsName": \["vrajtmt.in"\] // company domain } } You can also retrieve details directly using a CIN number by filtering with the entityId field. Example request using CIN: { "filter": { "entityId": \[""\] } }

### Identification of IT companies offering Product solutions
Sector Specialist team was looped in on call with client Curated the links basis their requirement and shared

### Company with Valuations - Same query returns 3K companies in Tracxn, whereas they return 9K in Pitchbook This query is described as: location: all countries except China, Russia, Iran last round post-money valuation: At least $70m investor type: Venture Capital or Accelerator / Incubator It yields only ~3000 results. We are quite a bit disappointed here since we expected at least 9,000 companies to have valuation data (based on a similar query in Pitchbook). Can you extend our API so we can at least pull data for these 3000 companies (we likely already queried for a large % of these but I'm not sure what the overlap is)
The difference maybe due to the valuation availability on our platform, we capture valuation from media or captables. We do not use models or assume valuation, this may be one of the reasons

### In the Financials API response, does the amountInBaseCurrency under latestAnnualRevenue convert exactly to the amount in USD if the base currency is SGD?
Tracxn captures a company’s revenue in its base currency (e.g., SGD) and also records the equivalent USD value using the exchange rate applicable on the source publication date. For example, if a company reported revenue of 100K SGD as of April 1, 2024, Tracxn converts and stores the corresponding USD value based on the exchange rate on that date. The platform consistently retains the USD value internally and uses the exchange rate from the capture date to convert between the base currency and USD (or other currencies, if required). As a result, minor differences may exist due to currency fluctuations and the specific timing of the conversion.

### Also in JSON the legal entity names are missing?
We’ve shared the company profile information with you. Just to clarify Legal Entity Name is part of our Legal Entity database and not part of the company database. Within the company database, we provide access only to the fields that are included in its defined scope. You can access the fields which are part of the companies database by clicking on Link.

### API to get transactions for AutoDesk and Avery Dennison. Could you please share a python based code in the below format.
Shared the below body to client // import requests import json url = "https://platform.tracxn.com/api/2.2/acquisitiontransactions" payload = json.dumps({ "filter": { "acquirerListDomain": \[ "autodesk.com" \] } }) headers = { 'accessToken': 'Access token of BCG', 'Content-Type': 'application/json' } response = requests.request("POST", url, headers=headers, data=payload) print(response.text) //

### What is the common identifier for a company in both the Companies Database and the Live Deal platform?
The common identifier for a company across both the Companies Database and the Live Deal platform is the id. This unique identifier ensures consistency when referencing a company in both platforms.

### Data query related to sectorList
Client can look in the object key "sectorlist" and get the defined response

### The client is looking for businessmodel as a filter to avoid credits consumption, have reverted back by saying the list of fields which they are looking for will consume API credits
As per Tracxn’s credit system, querying the /companies API will consume tokens, as that is how the system is designed. Unfortunately, retrieving only the company name, domain, and ID using the businessModel filter will still incur credit consumption for unique companies. API Credit Consumption Overview: Tracxn charges API customers based on the unique companies queried by the client. Whenever a client refreshes or updates a company profile via API, credits will be deducted, but the client will not be charged again for the same company. Charges apply only for unique companies called. Once the client exhausts their credits, our system analyzes the unique companies queried and replenishes the credits accordingly. For API queries that return null or void responses, there is no credit deduction.

### How can I query the Companies API to analyze a company's revenue and net profit in terms of CAGR?
Currently, the Companies API does not support a filter to directly query Revenue and Net Profit figures in terms of Compound Annual Growth Rate (CAGR). However, you can analyze a company's revenue growth over the last 12 months using the following filter for revenue growth percentage: latestRevenueGrowthPercent: { "min": 0, "max": 100 } For a more detailed analysis of revenue and net profit over time, you can use the Time Series API. This allows users to retrieve historical data and analyze trends over a specific period, enabling you to calculate CAGR manually from the time-series data.

### In marqueecustomermentions on the platform, we get the list of names also, but in API response we only receive the no of mentions. Possible to add names and the domains also?
To identify the foreign parent legal entity (LE) of a company, you can track the parent-child relationship based on entity associations, such as subsidiaries or holdings. Relationships to consider: Joint Venture: Shared ownership and operations. Subsidiary: Majority stake with operational involvement. Holding: Majority stake but no operational involvement. Associate: Minority stake. To identify the foreign parent entity, we focus on the "subsidiary" or "holding" relationship, along with the location to filter out non-Indian parent entities. How to retrieve the data from the API: Use the following endpoint to search for related legal entities: : /api/3.0/legalentities Example request: { "filter": { "associationsName": \["vrajtmt.in"\] // Company name } } In the API response, look for the relatedLegalEntities field. If the relationship type is "holding" or "subsidiary" and the country name in the response.location is not "India", then the legalEntityId within relatedLegalEntities will be the unique identifier of the foreign parent legal entity.

### For employeefilings monthly data, we are getting stale data upto 2018. Can we get for last 3 years? PFA sample response output for paytm.com
The Tracxn API returns only 20 responses in the API, In order to get all the details please paginate through the API response to get all the required data. - \[Reference Link\]

### For Investor information 9Query by instrutuonalinvestordoma filter of Company API, we get the complete details of startups, instead of just a list as mentioned in the API reference. Any way we can just get the names and domains? Thanks.
The companies API returns all the fields mentioned in the Companies API reference, in order to get the name and domain of the company that can be fetched from the Companies API response as only name and domain won't be available in the API response.

### In competition API response, along with name and domain, can we pls get city and state also? Also the count= 427 below – does it mena TRACXN has data of 427 of its competitors?
In the Competitors API only name domain and ID can be fetched from API responses, in order to fetch the state and city please pass the domain as a filter in Companies API to get the state and city of the required competitor. --> Additionally in order to fetch all the Competitors of a company the below Sample body can be used in the Companies API to get all the competitors as the Competitors API will return only top 20 Competitors. Sample Body: { "filter": { "competitorOf": \[ "tracxn.com" \] } } --> Please Note while using the above filter it will consume the Unique Companies Profile as it is queried using Companies API, in order to avoid the unique company consumption the Competitors API can be used as it will not charge any unique companies profile.

### How can I find the foreign parent entity of a company when it is a subsidiary, using the API?
--\> Please refer to the below workflow to get the Foreign Parent LE: Relationships: Joint Venture Subsidiary - Majority stake and also involved in operations Holding - Majority stake but not involved in operations Associate - Minority stake From the above relationships, we can track the holding / subsidiary relationship to track the parent-child association, and determine the foreign parent using location. How to get the data from the API: Endpoint: /api/3.0/legalentities SR: { "filter": { "associationsName":\["vrajtmt.in"\] // company name } } In the response, fetch the key 'relatedLegalEntities'. If relatedLegalEntities.relationType == 'holding or subsidiary' && 'response.location.countryName != India', then relatedLegalEntities.legalEntityId is the unique identifier of the foreign parent LE.

### For some companies such as netmeds.com, we don’t get the section totalValuation in the output. Any reason?
For the companies such as companies such as netmeds.com the totalValuation details are not available due to which it is not available in the API response.

### Does the relatedLegalEntities.legalEntityId in the Legal Entity API correspond to the id in the acquirerList/latestAcquiredInfo/partOf section of the Company API output?
Yes, the relatedLegalEntities.legalEntityId in the Legal Entity API corresponds to the id field in the Company API output. It represents the unique identifier of the related legal entity, which you can query using the domain or CIN number in the Legal Entity API. To map the related legal entities: Use the following endpoint in the Companies API: Endpoint: https://platform.tracxn.com/api/2.2/companies Example request: { "filter": { "companyLegalEntityId": \[ "5ab10860e4b06a6b427cf3c8" \] } } Pass the legalEntityId in the companyLegalEntityId filter. The response will include the associated companies, allowing you to map the related legal entities.

### How can I derive the CIN from the ID provided in the response, as the ID appears to be in a raw format?
The ID provided in the response is a raw identifier, which does not directly correlate to the CIN. To derive the CIN, you will need to use the company's legal entity information. This might involve making a secondary API call to retrieve the company's details, which should include the CIN number. You can query the Legal Entity API or other relevant endpoints where the CIN is typically provided alongside other company identifiers.

### What is the formula for calculating the CAGR percentage?
The Compound Annual Growth Rate (CAGR) is calculated using the following formula: Case 1: Both values are positive Condition: arduino CopyEdit begin > 0 AND final > 0 Formula: arduino CopyEdit CAGR = (final / begin) ^ (1 / years) - 1 Case 2: Both values are negative Condition: arduino CopyEdit begin &lt; 0 AND final < 0 Formula: sql CopyEdit CAGR = (-1) * ((ABS(final) / ABS(begin)) ^ (1 / years) - 1) For a more practical example, you can refer to the attached sample calculation for the company shown in the image. You can access the calculation by navigating to PayPhi &gt; Financials > Net Profit / Loss. Note: The CAGR is calculated based on the company’s base currency.

### Do you identify which investors have been advised by facilitators, such as azbpartners.com and trilegal.com, who advise both startups (sell side) and investors (buy side)?
Currently, there is no curation of funding rounds for azbpartners.com in the system. Facilitators are typically mapped at the funding round level, rather than directly to investors. There is no direct mapping available between each investor and a facilitator. For a clearer understanding of what facilitators do and how they are involved, please refer to this \[link\].

### Do you cover other deal types such as Venture Debt, Buyouts, M&A, etc.?
Yes, we do cover a variety of deal types including Buyouts and M&A. These are available through the Acquisitions API. To access Buyouts and M&A deals, use the following endpoint: Endpoint: https://platform.tracxn.com/api/2.2/acquisitiontransactions Sample Request: { "filter": { "acquisitionType": \[ "Leveraged Buyout", "Acqui-Hired", "Business Acquisition", "Management Buyout", "Management Buy-In" \] } } For more details, you can refer to the \[Acquisitions API Documentation\].

### Which property indicates when a company was first included in the Tracxn database? Is it ‘createDate’ or ‘domainRegistryDetails.registeredDate’? What are the differences between these two dates?
The createDate is the date when a company was first added to the Tracxn database.

### Is there seasonality in funding and acquisition data on the platform?
Yes, funding and acquisition data often exhibit seasonality, as the data is based on the actual dates of transactions. These patterns can be influenced by several factors, including: Budget Cycles: Investment activity may align with quarterly, half-yearly, or annual budgeting schedules. Holiday Periods: A noticeable slowdown is often observed during major holidays. Incubation Cycles (especially in Accelerators & Incubators): Funding activity may increase around the end of quarterly or half-yearly incubation programs. Global Events: Broader trends, such as the significant dip in activity during the COVID-19 pandemic, also contribute to seasonal fluctuations. These factors combined result in observable peaks and troughs in funding and acquisition trends throughout the year.

### There is a strong outlier in the number of IPO cases for July 2013. Is this expected?
Yes, the spike in IPO cases during July 2013 is expected and can be attributed to a structural change in Japan’s stock exchanges. During this period, the Osaka and Tokyo Stock Exchanges merged, and as part of the merger, all companies previously listed exclusively on the Osaka Exchange were transferred to the Tokyo Stock Exchange. This resulted in a one-time increase in the number of listings recorded for that month. We are currently reviewing ways to present this data more clearly to account for such events and avoid misinterpretation.

### What is the difference between ‘Seed’ and ‘Angel’ funding rounds?
Seed Round: This round includes at least one institutional investor, such as a venture capital firm or accelerator. Angel Round: This round is composed exclusively of individual investors (angels) and does not involve any institutional investors. The key distinction lies in the type of investors participating in the funding round.

### How does Tracxn ensure early and broad coverage of companies, especially for private market investors?
We aim to track companies as early as possible to maximize value for private market investors. Our data is sourced from a diverse range of channels, including: Domain Registrars: Monitoring newly registered company domains to identify early-stage businesses. Client Requests: Prioritizing the addition of companies based on direct client interest and feedback. News and Media Coverage: Scanning public sources for mentions of emerging companies and startups. Company Registrars: Integrating verified legal entity data from official government and regulatory registries. This multi-channel sourcing strategy enables us to maintain comprehensive and timely company coverage.

### What factors influence the prioritization of companies for deeper curation and scoring on Tracxn?
While we aim for comprehensive coverage, the depth and timing of a company’s curation and scoring are influenced by several key factors: Client Mandates: High priority is given to companies explicitly requested by our existing clients. Potential Client Interest: Companies aligned with industry trends or sectors of interest to prospective clients are prioritized. Media and Market Signals: Companies gaining visibility through funding rounds, acquisitions, or notable media coverage are fast-tracked for deeper analysis. As a result, the time it takes for a company to be curated in detail can vary. Some are added early due to strong external signals, while others may take longer based on data availability and strategic relevance.

### What criteria does Tracxn use to update company descriptions?
Company descriptions are updated by our analyst team based on a detailed review of publicly available information. This includes: The company’s official website Updates in product offerings or business models Press releases, blogs, or other credible public sources To maintain neutrality and avoid copyright issues, we do not alter or modify descriptions sourced from third-party content providers.

### How frequently are company descriptions updated on Tracxn?
Company descriptions are updated based on the following triggers: Proactive Updates: Initiated by our analyst team when there are significant developments such as changes in business model, product launches, or major announcements. Client Requests: Updates are made upon request from clients, such as the revisions done in April 2024 and October 2024. There is no fixed update cycle, but companies with high visibility or frequent activity are reviewed more regularly to ensure data remains current.

### Do you process information in languages other than English? If so, which languages are supported?
Yes, we process information in multiple languages based on the source of the data. While English is the primary language, we also incorporate data in various other languages depending on the region and availability of filings. Below is an overview of the languages we process across different geographies: English: India, UK, Singapore, Australia, USA, Ireland, New Zealand, Malaysia, South Africa French: France, Luxembourg, Belgium German: Germany, Austria, Switzerland Spanish: Spain, Mexico Mandarin Chinese: China, Taiwan Russian: Russia Portuguese: Brazil, Portugal Dutch: Netherlands, Belgium Arabic: Israel, UAE, Saudi Arabia, Jordan Italian: Italy Swedish: Sweden Danish: Denmark Polish: Poland Czech: Czech Republic, Czechia Korean: South Korea Japanese: Japan Hebrew: Israel Turkish: Turkey Indonesian: Indonesia Thai: Thailand Greek: Greece Hungarian: Hungary Romanian: Romania Finnish: Finland Norwegian: Norway Ukrainian: Ukraine Bulgarian: Bulgaria Latvian: Latvia Lithuanian: Lithuania Slovenian: Slovenia Afrikaans: South Africa Filipino: Philippines Urdu: Pakistan Swahili: Kenya We ensure comprehensive coverage across global markets by processing data in these languages, depending on regional filings and publicly available information.

### Why are the number of acquisition and funding cases in China lower than in regions like the US and Europe? Is this due to limited availability of data in China?
The lower number of acquisition and funding cases for China compared to regions like the US and Europe can be explained by the following factors: Lower Overall Coverage: Our platform currently has comparatively lower coverage of China-based transactions. As a result, the representation of acquisition and funding deals in China appears less prevalent than in the US and Europe. Media-Based Data Limitations: While we capture a majority of publicly reported transactions from global news sources, some China-based deals may not receive widespread international media coverage. Many of these transactions might only be reported in local or restricted-access sources that are not fully integrated into our dataset. In contrast, US and European transactions benefit from well-integrated, widely accessible media sources, making it easier to capture data. Additionally, shared language support in these regions contributes to more comprehensive coverage.

### What are the main sources of your data, and can you provide the percentage of information sourced from each? Do these percentages change over time?
We source data from multiple channels, and below are the current statistics for funding rounds, acquisitions, and company-related information across various data sources: rfc822msgid:CAKDS2ikfAhEr-bUKM9umT+dZdXj9FWrQO_1i99zRhVBehdVdDg@mail.gmail.com These percentages reflect our current data sourcing approach. They may change over time based on evolving data collection methods and shifts in available information from each source.

### How is the data for IPO events distributed?
The distribution of IPO event data is as follows: 95% of the data is sourced directly from IPO exchanges. The remaining 5% comes from news coverage that reports on IPO events. This ensures that the data we provide is comprehensive and reliable, with a primary focus on official IPO exchanges.
