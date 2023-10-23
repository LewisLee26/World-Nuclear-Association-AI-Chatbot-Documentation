# World Nuclear Association AI Chatbot Documentation
*This is documentation for the World Nuclear Association AI Chatbot. Databases and Code used for the project are owned by World Nuclear Association and are not available in this repository.*

World Nuclear Association AI Chatbot is able to have conversations about nuclear energy and the nuclear energy industry. It stays up to date and accurate by drawing from the World Nuclear Association's articles, reports and databases. World Nuclear Association AI Chatbot allows users to quickly find information, help users better understand complex nuclear energy related topics, and access information across mutliple different formats. 

*The full report is currently in progress.*

## Methodology
### Overview
World Nuclear Association AI Chatbot uses a Large Language Model Autonomous Agent with Retrival Augmented Generation. The system is able to decide whether a search is needed, what source is best suited and the required search parameters. 

### Data
The system has access to four sources:
- [World Nuclear Association Information Library](https://www.world-nuclear.org/information-library.aspx)
- [World Nuclear News](https://www.world-nuclear-news.org)
- [World Nuclear Association's Reports and Publications](https://www.world-nuclear.org/our-association/publications.aspx)
- [World Nuclear Association's Reactor Database](https://www.world-nuclear.org/information-library/facts-and-figures/reactor-database-data/reactor-database-search.aspx?source=%7B"query"%3A%7B"match_all"%3A%7B%7D%7D%2C"size"%3A25%2C"sort"%3A%5B%7B"index.sort_name.exact"%3A%7B"order"%3A"asc"%7D%7D%5D%7D)

Text based sources such as World Nuclear Association Information Library, World Nuclear News, and World Nuclear Association's Reports and Publications are converted into vector databases using Text-embedding-ada-002 and ChromaDB on AWS. This allows the agent to search for related information more accurately. World Nuclear Association's Reactor Database is stored as a series of CSV files and requires a different method for the agent to search.

### Large Language Model
World Nuclear Association AI Chatbot uses GPT-4 16k. This is due to its high accuracy across many agent based benchmarks, easy to implement API, low running costs, and function calling which prevents parsing errors. 

### Agent Framework
The Agent uses two Langchain agents: 
- A custom multi-parameter OpenAI funcation calling agent to allow detailed searches across the text based sources 
- The Langchain CSV agent to access World Nuclear Association's Reactor Database 

## Examples
### Example 1

**Assistant:** How can I help you?

**User:** What news was there last week?

**Assistant:**
**Searching World Nuclear News for:** from 22/28/2023 to 29/8/2023
Here are some of the nuclear-related news from last week:
1. [OPG ad campaign recasts nuclear](https://www.world-nuclear-news.org/Articles/OPG-ad-campaign-recasts-nuclear) (24 August 2023): Ontario Power Generation (OPG) has launched a new public education campaign that uses the power of movies to tackle misperception of nuclear power. The Recast Nulcear campaign presents the unique benefits of nuclear power through a series of themed film posters and trailers, digital and radio adverts.

2. [Supply chain must expand to meet new build plans, report warns](https://www.world-nuclear-news.org/Articles/Supply-chain-must-expand-to-meet-new-build-plans,) (22 August 2023): Consistent policies to incentivize investment are needed to ensure that a fast global nuclear expansion can be supported by the nuclear supply chain, without bottlenecks, and build in resilience against potential supply chain shocks, according to World Nuclear Association. 

3. [UK funding to ensure Ukrainian nuclear fuel supplies](https://www.world-nuclear-news.org/Articles/UK-funding-to-ensure-Ukrainian-nuclear-fuel-suppli) (23 August 2023): Since the start of the invasion, Urenco has provided support to its customer, Energoatom, and its employees, and increase its supply of nuclear enrichment services to help provide energy independence and security of supply in Ukraine.

4. [Studsvik considers SMR deployment at Nyköping site](https://world-nuclear-news.org/Articles/Studsvik-considers-SMR-deployment-at-Nykoping-site) (24 August 2023): Swedish nuclear technical services provider Studsvik has signed a memorandum of understanding with small modular reactor (SMR) project development company Kärnfull Next, which is investigating the possibility of constructing and operating SMRs on the Studsvik industrial site near Nyköping ib Swedeb's east coast.

Please note that the summaries are directly quoted from the articles

### Example 2

**Assistant:** How can I help you?

**User:** Make a search on the World Nuclear News for new reactor technology for this year and then last year. Use the results to give an analysis of how it has changed. I only want your analysis. Use statistics and facts from your searches to back the points in your analysis. Your response must be three paragraphs long and provide links to sources.

**Assistant:** 
**Searching World Nuclear News for:** new reactor technologies from 1/1/2023 to 31/12/2023
**Searching World Nuclear News for:** new reactor technologies from 1/1/2022 to 31/12/2022
Based on the information gathered from the World Nuclear News, there has been significant advancements in new reactor technology in 2022 and 2023.

In 2022, there was a focus on the development of small, lead-cooled fast reactors (LFRs) and 3D printing for reactor components. Newcleo, a UK-based innovative reactor developer, collaborated with ENEA, the Italian nation agency for new technologies, energy, and sustainable economic development, to develop small LFRs. They planned to build an electrical prototype of the LFR system, which would not use radioactive materials or nuclear fuel, to study thermo-dynamic, mechanical, and functional performances ([source](https://www.world-nuclear-news.org/Articles/Newcleo,-ENEA-to-cooperate-on-advanced-reactors)). Furthermore, Ultra Safe Nuclear Corporation (USNC) licensed a novel method to 3D print components for nuclear reactors, developed by the US Department of Energy's Oak Ridge Nation Laboratory (ORNL). This method was ideal for manufacturing components for USNC's advanced nuclear reactor designs ([source](https://www.world-nuclear-news.org/Articles/ORNL-developing-3D-printed-nuclear-microreactor)). 

In 2023, the advancements in new reactor technology continued with a focus on microreactors and the use of nuclear propulsion in shipping. NANO Nuclear developed Zeus and Odin microreactors, which represented the leading edge of advanced nuclear microreactor technology ([source](https://www.world-nuclear-news.org/Articles/US-micro-reactor-company-sets-up-HALEU-subsidiary)). Additionally, studies explored the use of nuclear propulsion in shipping, with Newcleo signing an agreement with Fincantieri and RINA to carry out a feasibility study for nuclear applications to the shipping industry ([source](https://www.world-nuclear-news.org/Articles/Studies-explore-use-of-nuclear-propulsion-in-shipp)).

In conclusion, the advancements in new reactor technology from 2022 to 2023 have shown a shift from the development of small LFRs and 3D printing for reactor components to the development of microreactors and the exploration of nuclear propulsion in shipping. These advancements have the potential to revolutionize the nuclear industry by making nuclear energy more efficient, safer, and more versatile.
