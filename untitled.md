# Development of Advanced Knowledge, Data management tools and Capability 

- A hierarchy of best data-management and best-practice documents were developed from [policy](https://iplant.plantandfood.co.nz/project/datamgmt/Documents/PFR%20Data%20Management%20Policy%20based%20on%20Lincoln%20Hub%20Template.docx) through [principles](https://github.com/PlantandFoodResearch/BestPractices/blob/master/Best_Practice_Documents.md) to [practice](https://github.com/PlantandFoodResearch/BestPractices/blob/master/general/BestPracticesForData.md) and [specifics](https://github.com/PlantandFoodResearch/BestPractices/blob/master/general/best_practices_excel_data_file.md)
- The iRODS proof-of-concept instance has been created. Coupled with this is the Metalnx web interface for iRODS. 
- A Globus end-point has been created, also coupled with the iRODS proof-of-concept instance. An additional tool has been developed to allow new users to register for access to the iRODS instance.
- Data added to the file-system via iRODS is owned by the iRODS-server user. This will present a problem if this method is used to add data to the system. Hence adding data is best achieved via traditional file-system methods, after which the data can be added to the iRODS catalogue. The 2GB upload limit for the Metalnx interface is another good reason to use the file-system to add data. A best-practice should be created to cover this methodology.
- Metalnx metadata templates can be 'stacked' (much like the [CSS](https://www.w3.org/Style/CSS/Overview.en.html) philosophy) allowing generic templates and specific template to be combined in a logical manner.
- Globus file transfer is extremely efficient compared to traditional data transfer speeds via Plant and Food Research's internet connection. Globus is more than 100-times faster than the standard internet connection for file transfer.
- A decision has been made to allow read/write access to all storage data from iRODS. This will be further controlled via the iRODS user management itself, which will leverage the existing POSIX user/group permissions.
- Data stewards will need to be trained to use the iRODS metadata catalogue, both via the Metalnx interface, and via the iCommands (Linux command line).

**Milestone 7**

This milestone has become part of BAF during project lifetime. WE tehrefore describe this milestine in more detail

Milestone 7 is both a milestone within the Better Analysis Faster project, as well as a codename for PFR's powerPlant computational environment. As a purely IT infrastructure milestone, it does not depend on the development of management tools but rather on the adoption, configuration, administration, and coordination of multiple IT components.

In Milestone 7.1, we describe a vision for Computational Science in which users are able to access self-contained units of compute in the form of disposable Virtual Machines, on a self-service fashion. This effectively means adopting cloud type services, as well as moving powerPlant towards IaaS (Infrastructure as a Service).

With Milestone 7.2, the goal is to provide data analysis tools commonly used in powerPlant as containerised micro-services which can be built, versioned, shared, and re-used; with complete independence from the underlying Operating System. This would allow the scientific community to easily re-create and reproduce the computational environment used for a given research project, and would greatly simplify the peer-review process.

Multiple tools have been considered for exploration:

- Virtual computing provision platforms
 - VMware vCloud Suite
 - OpenStack
 - OpenNebula
- Containerisation
 - Docker
 - Singularity

They are explored in detail in the *Progress Towards Impact* section below.

**What have we learned?**

- Vendor support will be critical for the succesful implementation of either sub-milestone. This should translate not only in the adoption of IT best practices, but also in the avoidance of bespoke or custom-tailored solutions that would hinder portability and collaboration with external organisations.
- During our investigations, it became clear that scientists will require a mechanism to publish the versioned images of either Virtual Machines or Containers used during analysis. It is already common practice to submit the raw data to public databases to facilitate the peer-review process. Demanding the exact copy of the analysis environment as well,  is a natural extension of this idea.
- We have also discovered that it was imperative to upgrade powerPlant to a newer Operating System if we were to succesfully test some of the tools listed above. Container technologies are bleeding edge and call for newer Linux kernels than the one powerPlant was running on. A considerable amount of time and resources were spent during this period to make this upgrade happen.

# Progress Towards Impact 

- The largest impct of this project is the enhancement of communicatio between the research community and IKS. Particulalry the travel to North Carolina brought these two groups much closer together. A good sign was that Eric Burgeneo brought milestone 7 to the project which will make a big diference to how computational research ins done at PFR.
- WE also achieved an increased awareness of the importance of data and its efficient management to PFR. This item is hard to prove. WE have to rely on th feedback we get from the reearch community which has only been positive so far.
- Agreeing on, and formalising the principles and messages constitutes a major step forward.
- Following these pribicples will make it now possible to work with clear purpose towards implementing these guiding principles.
- The implementation of a Globus hub as well as powerPlant SE allows now to transfer data to/form PFR servers at much higher rates as from a user's desktop (up to 10-15MB/sec instead of 200-300KB/s).
- An iRODS instance has been created for better data management. We obtained hmhm of capabilities by dollborating with NeSI
- With the einstallation of Metalnx we can now creae metadata templates. These templates will help PFR to collect meta data for different disciplines.
- The testing phase for iRODS data cataloguing, metadata templating, and Globus data transfers is complete.
- The impact of the completion of this milestone will be a searchable metadata catalogue of powerPlant _input_ data. This has progressed as far as the proof-of-concept (see the [milestone 5.2 report](https://github.com/PlantandFoodResearch/BetterAnalysisFaster/tree/master/doc/milestones/milestone5/milestone_5.2_report.md)).
- A Best practice platform has been developed (bestprctices.pfr.co.nz) which can be dynamically extended.
- The integrationBoth sub-milestones have the potential to change the way Science is done, not just at PFR but also in the wider scientific community. Reproducibility is a hard problem to solve in computational science, particularly in a world with faster moving targets in terms of software delivery. By suggesting a working model that successfully contributes to simplify the problem, PFR would be in a leading position in the global community.

**Milestone 7**

**What progress have we made?**

#### VMware vCloud Suite

**URL:** https://www.vmware.com/products/vcloud-suite

PFR's Virtual Infrastructure uses the VMware Hypervisor. It made sense therefore to explore this vendor's offerings in the self-service space. VMware provides a suite called vCloud. VMware vCloud Suite features components for cloud services provisioning, cloud services monitoring and cloud services chargeback, a self-service portal, an IT service catalog, and a policy engine. It comes in Standard, Advanced and Enterprise versions.

Advantages:
- Knowledge within PFR with VMware's products
- Builds on top of existing PFR components
- Good vendor reputation and support paths

Disadvantages:
- High cost
- Locks users to the VMware Hypervisor only
- No public cloud integration

During PFR's implementation of our secondary DataCenter in Waikato, we had the opportunity to learn about both the cost and limitations of the vCloud Suite. While self-service was not explored as a requirement for that project, a decision was made against the Suite purely based on its high cost.

In the context of Milestone 7.1, vCloud Suite lacks multi-hypervisor support which we consider a highly desirable feature. VMware tackles this and other limitations with their next tier product (VMware vRealize). We decided against exploring vRealize as we considered it unlikely to be cost effective.

#### OpenStack

**URL:** https://www.openstack.org/

OpenStack is a free and open-source software platform for cloud computing, and a competing alternative to VMware's product portfolio. As is common in the open source software world, the product itself is free (both as in freedom and as in _free beer_) and multiple companies can provide support for it. The OpenStack Foundation is the non-profit organisation that manages the OpenStack product. Over 500 companies are currently part of this organisation.

Advantages:
- Knowledge within PFR of open-source solutions
- Can build on top of existing PFR components
- Good vendor reputation and support paths

Disadvantages:
- High complexity
- Heterogeneous solution which can lead to fragmentation
- Six-monthly release cycle

RedHat and Canonical both offer products based on OpenStack. Since PFR already has commercial relations with the RedHat we invited them to a meeting. On November 27th 2015, Ben Warren and Eric Burgueño met with Steven Ellis and Mike Hepburn. After discussing our environment, requirements, and future vision; RedHat suggested that OpenStack was too complex of a solution for PFR, and that we would require to at least double our FTE count (from 2 to 4 FTEs) to support it accordingly. RedHat suggested we look into another product of theirs: CloudForms. We decided to take their suggestion on board for further exploration.

#### OpenNebula

**URL:** http://opennebula.org/

OpenNebula is an alternative cloud computing platform to OpenStack, that is also free and open-source software. OpenNebula toutes itself as an open-source effort focused on user needs, while considering OpenStack a vendor-driven effort focused on the need of other vendors.

Advantages:
- Knowledge within PFR of open-source solutions
- Can build on top of existing PFR components
- Simpler setup and maintenance than OpenStack

Disadvantages:
- Fewer support alternatives
- Unknown market share

PFR deployed a PoC installation of OpenNebula using spare hardware with limited resources. The trial was operational for aproximately eight months, and allowed at least three staff members to explore its functionality in a "close to production" fashion.

### Milestone 7.2
#### Docker

**URL:** https://www.docker.com

Docker allows a user or an administrator to package an application with all of its dependencies, into a standardized unit which can be universally deployed. It does this by leveraging a combination of containerisation and resource management technologies present in modern Linux kernels. The quick speed of adoption of Docker by the IT industry can be attributed to the simplicity it brought to the management of containers.

Advantages:
- Knowledge within PFR of open-source solutions
- Can build on top of existing PFR components
- Good vendor reputation and support paths
- High market share

Disadvantages:
- Rapidly changing and still maturing technology
- Somewhat high complexity
- Security and Operational Management challenges
- Built by and for the Web Hosting industry

PFR has adopted Docker in a PoC basis to further investigate how best to adapt it to its needs. At the present, 17 PFR users have been running Docker containers. We expect this number to increase with the release of powerPlant SE.

#### Singularity

**URL:** http://singularity.lbl.gov/

Singularity is another container management toolkit, which can be used to encapsulate a system environment in such a manner to make it portable between systems. It distinguishes itself from Docker in that the two were created with different purposes in mind. From the [Singularity FAQ](http://singularity.lbl.gov/docs_faq.html)

> Docker has been used for a variety of purposes, but it is designed as a platform to provide replicatable, network service virtualation. Because of this basic assumption and design model, it makes it difficult to implement on shared HPC platforms (and thus Singularity was born). Additionally, Docker supports the notion of emulating full operating system enviornments including user context escalation.

> Singularity on the other hand does not support user escalation or context changes, nor does it have a root owned daemon process mananging the container namespaces. It also exec's the process workflow inside the container and seemlessly redirects all IO in and out of the container directly between the enviornments. This makes doing things like MPI, X11 forwarding, and other kinds of work tasks trivial for Singularity.

During our Docker trials, the issues of [privilege escalation](https://github.com/PlantandFoodResearch/powerPlant/issues/315) and [complexity for end users](https://github.com/PlantandFoodResearch/powerPlant/issues/422#issuecomment-214544621) came up. Singularity was discovered as a potential solution for these problems, but we only knew about its existence in May 23rd 2016. Further research should go into it.

## Communication, Connections and Extension Activities

- As mentioned above, we were in touch with RedHat to discuss the feasibility of OpenStack for our environment. We have also touched on the topic of containers with them but we subjected follow-up discussions to the upgrade of our powerPlant cluster.
- At the LCA 2016 conference, we touched base with Bruno Lago from Catalyst IT. He mentioned the existence of a proposal to create a nation-wide pan-institution research network based on OpenStack. While the details of his proposal are confidential, it was implied that it hadn't gain enough traction nor consideration.

# Communication, Connections and Extension Activities List activities during the reporting period directed towards your key stakeholders 

*   Liaised with other interested teams (e.g., [Achieving Collaborative Data Management](https://github.com/PlantandFoodResearch/CollaborativeDataManagement) and [biometrics](https://iplant.plantandfood.co.nz/biometrics)) and individuals
* Socialised the ideas informally and via tools such as [iPlant news](https://iplant.plantandfood.co.nz/bg/Pages/BestpracticesExceldatafiles.aspx)
- [Presentatation Science Forum](http://bit.ly/1T3ZjEb)
- [Presentation SISSG](https://www.swipe.to/8227ct)
- [Presentation Food Innovation](https://www.swipe.to/7988c)
- Meeting about Ways of Working Auckland
- Presentation at eResearch and lioaise with hmhmhm from Niwa, Nauman Maqbook from AgResearch, and Tatiana Lomasko form Scion. This provided a good echange of ideas around data management and resukted in a collaboration for an MBIE bid around nanao satellite data aquisition.
- Presenttaion on Roadshow June 2016 (6x) to socialise our ideas.
- Connections with UNCC bioinformatics and information technology staff were made during the research exchange last August 2015. This provided us with further expertise in the implementation of iRODS, and philosophies of data/metadata management.
- Vladimir Mencl (NeSI) was contracted to install the iRODS proof of concept instance, he remains a point of contact for technical expertise in this area.
- Ben Warren connected with Steve Worth and the Metalnx development team during the BioIT World 2016 conference in Boston (April 2016). I provided feedback to them directly regarding Metalnx features and development. This solidified our relationship, improving PFR's standing as an important customer for the delivery of the Metalnx software, and also as a resource for testing/development for Metalnx in future.
- I have communicated with Shannon Schlueter (UNCC bioinformatics) regarding implementation of the production iRODS instance, he offers expertise and further contacts with the iRODS development team.



# Next steps What are the next steps required to maximise impact?  

* Continue building the foundation of best-practices across multiple content area
* Training, dissemination and implementation, using the best-practices a the "back-end"
* Finalise deployment of git documents to a PFR-wide available webpage using [Jekyll](https://jekyllrb.com/)
* Investigate ways of making Excel datafiles discoverable (e.g., a PFR-wide experiment database, integrating with [iRODS](http://irods.org/), text-mining)
* On-going development of guidelines via the git model
* Investigation of Github Enterprise Edition
* [Milestone 5.3](https://github.com/PlantandFoodResearch/BetterAnalysisFaster/tree/master/doc/milestones/milestone5#milestone-53) embodies the next phase in this project. This entails the implementation of a production-level iRODS server instance, with the first official release of the Metalnx interface (version 1.0). We have yet to decide if the Globus end-point should reside on this iRODS instance, or be a separate entity.
* An ontology of data-types and associated concepts will be created to guide metadata management implementation, specifically metadat templates for the Metalnx interface.
* Complete the production implementation of iRODS+Metalnx, and possibly Globus.
* Initiate the ontology of powerPlant input data-types.
* Create and/or auto-generate metadata for existing data in powerPlant input data area. Beginning with the CHIPs team's _Malus domestica_ data.
- Continue exploring alternatives for hybrid-cloud adoption
  - Re-evaluate the feasibility of OpenStack
  - Consider exploring CloudForms
  - Continue testing OpenNebula
  - Start exploring pathways to adopt the public cloud
- Deepen the usage of Docker where appropriate in our research environment
- Explore the feasibility of Singularity


# Outputs for 2015-16 

*   Reshaping of the high performance compute environment at PFR to be compatible with the new vision (PowerPlant Release 2)
*   Presentations including the Software Carpentry workshops, Best-Practice workshops, and international collaboration such as was done with UNCC and NC-State University in the North Carolina Biotechnology Corridor, USA
*   The documents referenced in the first section above
*   A growing list of 'Best Practice" documents across multiple domains that is addressing the question of "How do we do that here at PFR?"
* Presentation at the UNCC Research Exchange covering metadata/data management, solutions and principles.
* Feedback from the CHIPs team on the Metalnx user interface, metadata management policies, and data types produced by PFR scientists.
* The [process](https://github.com/PlantandFoodResearch/BetterAnalysisFaster/blob/master/doc/milestones/milestone5/pfr-irods-test-setup-notes.md) developed for implementing iRODS server provided by Vladimir Mencl.
* A [summary of Milestone 5.2](https://github.com/PlantandFoodResearch/BetterAnalysisFaster/blob/master/doc/milestones/milestone5/summary_milestone_5.2.md), which includes decisions made and actions taken to complete this milestone.

-	Presentations
  - At UNCC: ["The Neolution of the Machines"](https://github.com/PlantandFoodResearch/BetterAnalysisFaster/blob/master/doc/presentations/eric/The%20Neolution%20of%20the%20Machines.pdf)
  - At LCA2016: ["The life of a sysadmin in a research environment"](http://sysadmin.miniconf.org/2016/lca2016-eric_burgueno-the_life_of_a_sysadmin_in_a_research_environment.pdf) ([Video](https://youtu.be/SiSY1b0am5w))
- [Reprodcible Research as a Service](http://www.plantandfood.co.nz/file/J005841_SP_WarrenBen)
- Meetings with Ben Warren an UNCC [Summary](https://gist.github.com/warrenson/7c745ed2a5b6700273cb)
- Meeting of Ben Warren with scientists at teh BioIT conference [Summary](https://gist.github.com/warrenson/add1e9c288371f93b0f5)
-	Proposal and Planning Documents
  - [powerPlant SE proposed Architecture](https://github.com/PlantandFoodResearch/powerPlant/blob/meta/proposals/CentOS%207%20architecture.md)
  - [Hybrid Cloud Support matrix](https://github.com/PlantandFoodResearch/powerPlant/blob/meta/proposals/Hybrid%20Cloud%20Support%20matrix.xlsx?raw=true)


### Presentations

- Data Management Workshop
- eResearch
- [Science Forum](http://bit.ly/1T3ZjEb)
- Health Science Forum
- Symposium at University North Carolina Charlotte

### Reports and Documentation

- Informatics White Paper 
- Travel report UNCC
- Proposal for DS
  - The K-Drive
  - hmhmhm
  - Blue Berry
- Data Steward Role Document
- Data Management Basics
- Data Management Plan Document
- Best practices documents
    - Excel Data
    - GitHub for analyses
    - Linux Command Line Interface (CLI)
    - RNAseq experiments
 
# Glossary

- iRODS: The Integrated Rule-Oriented Data System (iRODS) is open source data management software used by research organizations and government agencies worldwide. (http://irods.org/)
- GitHub: Source code verison management and moch more (github.com)
- jekyll: A website generator from texts like GitHub Readmes
- powerPlant: PFR's powerful computer cluster and more (powerplant.pfr.co.nz)
- RNAseq: RNA next generatino sequencing project including gene expression analyses
- 