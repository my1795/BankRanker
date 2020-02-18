# Abstract

        RESTful API architecture has been using widely for different type of web applications.In our case ExchangeRates application uses different banks&#39; REST web services in order to retrieve their instant currency rates and extract results on which bank has less volatility on currency rates. Then the system sends the result to user via REST web service interface. Therefore, many RESTful services are used and its responses combined in ExchangeRates which is also a web service along the calculation in the program. ExchangeRates is a composite web service since it is a combination of multiple web service and it has also a user API to provide this service to authenticated users. As a result of too many RESTful requests, there may be a lot of bugs and wrong results in the system. The system must be tested properly in order to reveal failures. Model-based testing and development approach fits to this needs since the system makes a lot of requests and includes different components. Thus, the system is a good candidate to use the development and testing approach. However, there was a critical issue on generating the test data to test ExchangeRates API. This step was the most crucial part to utilize model-based approaches&#39; benefits. There may be many banks which must be graded in our system. The key point is that bank web service&#39;s usually works  without any problem. Therefore, sequence of test cases must be combined with model-based testing architecture. The difference is that mock service generates data with many faults shaped by tester. Model-based testing aims to perceive parts of the system as states. The system is perceived as a state machine while states are components of a system and transactions are functionalities in the system. As a result of that, test model fulfills its duty to cause different transactions in system model. Test model considers the user&#39;s actions as states. Faulty and non-faulty user based data is generated in test suite randomly. Then, the model is run automatically instead of doing manual tests. This gives an opportunity of generating multiple test cases only by one model. As a result of that, this process becomes more efficient in terms of time.

To conclude, ExchangeRates service is a composite service that uses multiple web services. Also, the system must be tested with different usage scenarios. Model-based testing approach is embraced to reach these goals.



# Contents

| **INTRODUCTION        4** |
| --- |
| **BACKGROUND        5** |
| **PROBLEM STATEMENT        7** |
| **SOLUTION APPROACH        8** |
| **RESULTS AND DISCUSSION        21** |
| **RELATED WORK        22** |
| **CONCLUSION AND FUTURE WORK        23** |
| |
| |
| |

1. **I.**** Introduction**

        People tend to use online banking solutions in today&#39;s world. Individual investors make their investments on different currencies by using banks&#39; online pay-desks. There are many banks and the banks have various different spreads(sell rate and buy rate differences) on different currencies. These spreads may volatile especially if there is an unstable situation financially among different banks. The problem has become prominent here: investors cannot decide on the bank that they must to deposit their money for investment or savings. Different banks set quite different spreads on USD-TL  in Turkey [1] . These spreads may even much more various in unstable market conditions[2] in August 10th 2018 in Turkey for the sake of example.

ExchangeRates bring the solution by combining RESTful APIs of those banks to compare their currency rates and outputs less volatile bank as a RESTful web service. Briefly, our system composition of multiple web services. If the bank has the lowest spread on USD-TL our system sends the result to client as RESTful API. The second key part is to decide on the testing method and techniques on our system. The incoming data to our system has come from separate banks to our system and the data can be faulty or different format from as it is expected. Also, there are different types of users in the system with different authorization types. As a result, model-based testing and development considered necessary for the system since our model consists of different strict parts and the transactions between them are clear as it is discussed in Solution Approach section in detail.

        Apart from implementing the solution for investors, the second critical part is testing ExchangeRate. As it is stated, model based testing is used by utilizing modelJUnit library extended by JUnit test tool in Java programming language. There are multiple RESTful APIs in the system with different behaviors. This project separated in models. However, Users will interact just with UserAPI and Dataprovider services. Therefore , these APIs will be tested by test model. Unexpected results will be reported in the model.

1. **II.**** Background**

Tools and techniques and technologies are listed below in this project:

**REST:**  REST is abbreviation of Representational State Transfer; it is an architectural design for applications that runs over HTTP allows both XML and JSON type data transfer over HTTP with uniform design. However, JSON type is selected in the project.

**JSON:**  JavaScript Object Notation; it is lightweight format for data transferring in client-server systems. REST APIs use this format in our case.

**Intellij Idea IDE:**  IDE that is used to run the project on Java in our ExchangeRate and MockService components.

**Maven:**  Build automation tool that is used to easily connect our dependencies in our project. It is used mostly integrate related dependencies in the project.

**Apache Tomcat:** Provides HTTP web server in order to contain our RESTful web services ExchangeRate and MockService. _Jersey / JAX-RS_

**Jersey / JAX-RS:** It is a servlet container in order to view REST requests in our case. It is commonly used in early stages of development.

**ModelJUnit:** The library used to implement model-based testing and review the results. This is the key tool in our system for testing.

**Digital Ocean:** It is the cloud infrastructure that will allow us to store banks&#39; data daily, weekly, monthly. This project returns the results instantly for now. Digital Ocean will help to store the data and to process it in the next stages of the project. ExhcnageRates and MockService run on it.

**FileZilla:  ** infrastructural Used to upload WAR(web archive) files to digital ocean server.

**Asbru Connection Manager:** A user interface that helps organizing remote terminal sessions and automating repetitive tasks.

**ElasticSearch:** It is a preferred search engine for its performance capabilities, powerful and flexible features such as content search, data analysis, queries and suggestions.

**YapıKredi Bank Currency Rates API:** The API is in REST architectural form. This is the only bank API that runs on our system for now. The number of banks will be increased in the next stages.

**Spring Framework:** The framework is used to grab data from YKB API. This framework is not used any other part of the project since it was just necessary for YKB.

**Spring Boot Framework:** The project is converted to a Spring boot project from core Java implementations. Especially, REST based transactions are handled with spring boot framework

**OAuth 2.0:** The authorization method that YKB provides us as client of YKB API. It helps to bring security and simplicity to REST APIs.

**Gecko Driver:** Gecko driver is the link between Selenium and firefox browser. It is used sizably in model-based testing part. It automates requests to the system via modeljunit.

**Org.json:** JSON library to iterate over json files and process them in java.

**G.json:** Google&#39;s json library with different functionalities from org.json.

1. **III.**** Problem Statement**

        The project idea is taken from Ozyegin University faculty member Hasan Sözer. According to project, composition of multiple RESTful web services must be implemented as a new RESTful web service. Also, the system must be tested by model-based approach.The project mainly consists of two parts ExchangeRates and MockService both designed and developed by us. Individual investors may not give healthy decisions when they invest on USD-TL currency via online banking. They need to get information about which bank is more reliable on spreads. ExchangeRates solves this problem by ranking the banks. Thus individual investors can make their decisions via our solution. On the other this tool does not provide a helpful environment for big players in USD-TL investments since they generally use FOREX(Foreign exchange) with big amount of money. Forex traders use complex tools while trading different currencies. Therefore, the scope of this solution is limited by individual investors or people who want to save their money on USD-TL currency.

        The second challenge is testing the system in order to see whether the system can produce expected results when the inputs are unstable or wrong. Since most banks use RESTful APIs to send those results to users. The test logic must be capable of testing REST architecture and its file format JSON. Besides the method to solve this problem, the testing part must include an automated random data generation method to perform while implementing and executing tests. This is a crucial requirement for test part since there are multiple states among the exchangerates&#39; components. The service will be running with different components such as UserAPI, Dataprovider, Datacollector and Dataadapter. Also there is a test module named as exchangeratesMBT. The crucial components for user interaction is UserAPI and Dataprovider components. These components must be tested with various inputs. The problem is that classical unit test case preparation is quite time consuming and does not cover all the possibilities. Therefore, model-based testing is fitting for this kind of test case preparation. The components can be in multiple states and also a user who use that will be corresponding state for the components. The benefit is that there will be automated test cases which covers more than classical test methods and it is less time consuming.

**  Assumptions       **

**       ** The first assumption is that: users will demand USD-TL currency rankings of banks. Banks usually sends responses including multiple currencies such as EUR-TL, EUR-USD.... ExchangeRates is designed to response in format of USD-TL. The test generation method can easily produce fake data for EUR-TL and others too. However design of ExchangeRates cannot easily adapt to these needs. EUR-TL option can be added next feature of the tool.

**  Constraints       **

**       ** Bank APIs has some limitations of request numbers. It may differ across different banks. YKB API gives this limitations on number of calls on the API. YKB limits number of requests 5 per second. Detailed information can be found its API portal [3]. On the other hand, all banks do not have REST API service on currency rates. According to our research, Akbank, Yapı Kredi Bank, Kuveyt Türk and İŞ Bank have the service in Turkey. As a result of that, it affects system&#39;s coverage on information of currency rates.

1. **IV.**** Solution Approach**

In our project we have solved the problems defined in part III. The solution includes two main approach to solve the problem. We solved user needs by combining different web services. The second solution was on test part by developing an automated test logic via our tools. Advantages and disadvantages of it discussed below. The solution also explains how we used model based technique in our system. The banks will be ranked by their standard deviation of spreads. They will be graded by result of standard deviation intervals below in:

| Grade | Lower Bound | Upper Bound |
| --- | --- | --- |
| A | 0 | 0.05 |
| A- | 0.05 | 0.10 |
| B+ | 0.10 | 0.15 |
| B | 0.15 | 0.20 |
| B- | 0.20 | 0.30 |
| C+ | 0.30 | 0.50 |
| C | 0.50 | 0.70 |
| C- | 0.70 | 0.90 |
| D | 0.90 | 1 |
| F | 1 | 10 |

Table 1. Bank Rank Interval

According to interval table above the bank data will be ranked requested by users in the system. Ranks can be hourly, weekly and monthly according to user choice. The user choice can be sent dataprovider RESTul service in JSON format

**  Design Approach**

According to problem statement part, the project is decided to design on model-based approach and generic test case production method for bank RESTful services. These choice is made since composition of multiple web services fits a model-based design as each component of the system is a part of a model. Although the design approach has prominent advantages it has also some disadvantages that limits us to perform comprehensive test and development. The other method that we used is generic test case production method to see different behaviours of model with different data set that travels between components of the system via model based test cases. ExchangeRates is derived from a model as it is mentioned. The system has some advantages and disadvantages like every other design approach has. Therefore , the model of the project is extracted before it is started to implement due to our design decisions. Thus, we considered both implementation and testing part in model based perspective as it can be seen below:







**ExchaneRates Model:**
![Alt text](/screenshots/fig1.png?raw=true "Fig. 1 Composite Web Service Model(exchangerates)")

                                                

**                                               **



**       **

There must be collected rank data before processing it to rank banks. Datacollector component is designed to execute a cronjob to collect bank&#39;s currency rates every minute. Dataadapter component converts  different banks data in the same format to persist it elasticsearch repository.


![Alt text](/screenshots/fig2.png?raw=true "Fig. 2 Currency data persisted to elasticsearch repo by datacollector")

        Fig. 2 Currency data persisted to elasticsearch repo by datacollector

Dataadapter converts bank data in a format that is desired above. Banks services can send the data without unnecessary information or with different JSON key values. This component serves data to datacollector in a clear format. Datacollector takes the data and persist data to related indexes in elasticsearch repository. Elasticsearch keeps data with JSON format and it serves the data on RESTful API. This feature gives flexibility on project comparing to RDBMS since it is easy to process data again. All data flow happens in JSON format. ElasticSearch repository has &quot;rates&quot; index. There are also different types for different banks such as: YapıkrediBank -\&gt;   [http://167.172.160.222:9200/rates/ykb/\_search](http://167.172.160.222:9200/rates/ykb/_search) . Also, Denizbank -\&gt; dnz , IS Bankası -\&gt; isb. Besides that, there is another index as &quot;user&quot; for UserAPI to persist user data in the system. The next step after registering data to the system is retrieving them and rank banks according to that. Dataprovider component makes a RESTful connection to [167.172.160.222](http://167.172.160.222:9200/rates/ykb/_search) for port 9200 and gets related data to be ranked. Ranking logic is simply based on standard deviation of spreads as it is mentioned in Solution Approach section. The related request urls are shown at Tools and Techniques section. Users make REST requests  those urls. The request must include a REST request body as below:




![Alt text](/screenshots/fig3.png?raw=true "Fig. 3 Sample request body for dataprovider service")

                                                Fig. 3 Sample request body for dataprovider service
![Alt text](/screenshots/fig4.png?raw=true " Fig. 4 Sample request response for dataprovider service")
                                Fig. 4 Sample request response for dataprovider service



Dataprovider component retrieves requests as shown above and makes a request to UserAPI to check whether the request is made with correct authorization and authentication. For authentication it checks whether a user exist with given password in UserAPI. If there is , it checks request body. If there are more than two banknames request in the body for userRole of  &quot;STANDARD&quot; it returns an error code and does not authorize. There are three types of user in the system for a user &quot;ADMIN&quot;, &quot;STANDARD&quot; , &quot;PREMIUM&quot;. For admın and premium there cannot be added new specifications due to limited time. However, standard user restricted as it is described.

        As a result of the above statements, there must be a UserAPI to register users and make authentication and authorization to benefit from dataprovider  service. Related API urls are shown at Tools &amp; Techniques section. The sample request body for recording a user must be as below:


![Alt text](/screenshots/fig5.png?raw=true " Fig. 5 Sample user register request as REST request.")
        Fig. 5 Sample user register request as REST request.

        The working components is explained until these section. The second solution proposed was bringing a model based test generation solution to test the application. The test model which will be described below later is not a comprehensive test of all components in the system. The model focuses on user interactions with the system while incoming requests are made to Dataprovider service. The service also interacts with elasticsearch repository and datacollector inherently. However, these modules can be tested by unit tests. On the other hand, userapi and dataprovider has many interactions between them. This makes the model based test applicable on these components. ModelJUnit library will be used to generate test cases automatically and execute them. Our approach takes users to center of test cases. Model-based test logic is build as states and transitions. In our case rank requests, their results ,users and response can be in many states. Instead of preparing separate different test cases for each state and for each input, generating random inputs and running state machine for test purposes is quite efficient. There will be less test effort by this way. Also if there is an unexpected result while running state machine it will be reported by throwing an exception. The first step must be defining states and actions for UserAPI and Dataprovider service tests. The states and and actions explained below:

| **STATE** | **Explanation** |
| --- | --- |
| INITIAL | İnitial operations are done. Users are pre-loaded to UserAPI to test |
| ADMIN | If randomly picked user&#39;s role is ADMIN , this state is current state. |
| STANDART | If randomly picked user&#39;s role is STANDART, this state is current state. |
| PREMIUM | If randomly picked user&#39;s role is PREMIUM, this state is current state. |
| SUCCESS | After choosing role rank request is made by randomly generated rank request body and api url. If there is a response without error, current states changes as SUCCESS |
| FAIL | After choosing role rank request is made by randomly generated rank request body and api url. If there is a response with error, current states changes as FAIL. |
| NOT\_EXIST | If failure reason is unregistered username, this state is chosen. |
| WRONG\_PASSWORD | If failure reason is mismatched password, this state is chosen. |
| WRONG\_ROLE | If failure reason is restriction bank name number for STANDART user, this state is chosen. |
| WRONG\_BANKNAME | If failure reason is wrong bank name, this state is chosen. |

                                Table2 exchangeratesMBT States









| **ACTION** | **Explanation** |
| --- | --- |
| checkSuccess() | Checks if current state is Success. Then redirects to INITIAL |
| registerOrUpdate() | Registers or updates the users info randomly in INITIAL |
| changeRole() | changes  current user&#39;s role randomly in WRONG\_ROLE |
| makeRequest() | Makes request with randomly set request body to dataprovider in ADMIN,PREMIUM and STANDART |
| changeUserName() | Changes current user&#39;s name randomly in NOT\_EXIST |
| changePassword() | Changes current user&#39;s password randomly in WRONG\_PASSWORD |
| changeBankNames() | Changes current user&#39;s rank request&#39; bank list randomly in WRONG\_BANKNAME |

                                Table 3 exchangeratesMBT Actions



        The states and actions that may happen between them is stated above. After specifying them as a state machine model in exchangeratesMBT. ModelJUnit requires a test adapter class ,test model which is a state machine and a tester main class which test cases generated and results are printed. In the states if there is an unexpected result from dataprovider or UserAPI an exception thrown while tests are running. If there is not an error, the state changes by actions as given number of transaction limit A transaction happens via an action which changes the current state as (ADMIN, makeRequest, WRONG\_BANKNAME). The state machine model of test cases can be seen below:













**Test Model of ExchangeRates(exchangeRatesMBT):**

![Alt text](/screenshots/fig6.png?raw=true "  Fig 6. exchangeRatesMBT Test Model")
                                        Fig 6. exchangeRatesMBT Test Model

**       **

        ExchangeratesMBT model below can be run with specified iterattions. There is no upper range. However, there is an optimal number for each model. If there is an unexpected situation and exception thrown. Then the exception can be analyzed and root cause of the problem can be analyzed by looking at previous transactions.



According to our decisions and model behaviors we have listed advantages and disadvantages of our approach specific to the system  :

**Advantages:**

1. The system(ExchangeRates) can be divided into different sub-components to analyze easily and test them separately. Since our system is a combination of web service model-based approach will be helpful to detect where the problem happens easily.
2. If  one of the components depreciates or removed from by third parties, the system maintenance will be fairly fast. Thus, developers can adopt the changes according sub-modules of the system. To give an example; If a bank stops its web service, it can be removed system quickly.
3. Other systems can be integrated to the system, without making major changes in the system with RESTful architecture.
4. As it is stated in the 3rd advantage we integrated our test module(ExchangeRatesMBT) via REST urls to test the system.
5. Our generic test case generation method is used in ExchnageRatesMBT to deceive the system by manipulating user based request data.
6. This generic method allows us to manipulate the user data automatically with test model states

**Disadvantages:**

1. Model-based testing method cannot be divided in atomic parts line by line in the program. That can cause lack of test coverage in composite service(ExchangeRates).
2. Implementing unit tests are needed in some cases due to first disadvantage. Consequently, this can end with more work load which is not expected at the beginning.
3. Generic test data production method(ExchangeRatesMBT) may be ineffective since generated automated test cases do not traverse all components on the system i. e.  datacollector - elasticsearch repo transactions. The model considers user-based interactions as inputs.



**Tools &amp; Techniques**

**       ** First of all, this project is a RESTful web project and a server was a necessity to run the service. Spring boot framework is decided to be used in our system to build RESTful APIs on running an embedded Apache tomcat application server. In addition to that, it has a big community support in case of errors those we have faced. Datacollector, Dataprovider and UserAPI runs on the server. Apart from that, Maven build automation tool is used to fasten automation phase to load related libraries and JAR files such as ModelJUnit,tomcat… YKB API service is used to get currency rates. The other banks APIs have currency rates web service.İş Bankası and DenizBank web services also added in this part of project in order to get currency rates data.. Dataadapter works inside of Datacollector in order to convert data in same format in terms of buy and sell rates and currency rate names. Different banks use different data format on their RESTful APIs. The served data is converted via Dataadapter component inside of Datacollector. Datacollector persists the data to elasticsearch repository which runs on a ubuntu instance on Digital Ocean instance. The IP of instance is 167.172.160.222. Persisted data on database can be seen on the url: [http://167.172.160.222:9200/rates/\_search](http://167.172.160.222:9200/rates/_search) . Dataprovider serves result of rankings by request made from users on RESTful API named dataprovider. Dataprovider serves data to only registered users via UserAPI. UserAPI is a RESTful API in order to register users and serve the registered user data to Dataprovider. Dataprovider does not provide data to unauthorized or unregistered users by analyzing incoming rank requests.

| **HOST** | **REST API** | **ENDPOINT** | **METHOD** |
| --- | --- | --- | --- |
| localhost:8092 | /dataprovider/api/v1/ | /rank/{month} | POST |
| localhost:8092 | /dataprovider/api/v1/ | /rank/{month}/{currencyDayOfMonthValue} | POST |
| localhost:8092 | /dataprovider/api/v1/ | /rank/{month}/{currencyDayOfMonthValue}/{currencyHour} | POST |
| localhost:8092 | /dataprovider/api/v1/ | /rank/last6h | POST |
| localhost:8092 | /dataprovider/api/v1/ | /rank/last12h | POST |
| localhost:8092 | /dataprovider/api/v1/ |  /rank/last18h | POST |

                                Table. 4 Dataprovider Service (Exchange Rate URLs) on Tomcat Server and Digital Ocean

| **HOST** | **REST API** | **ENDPOINT** | **METHOD** |
| --- | --- | --- | --- |
| localhost:8093 | /userapi/api/ | /user | GET |
| localhost:8093 | /userapi/api/ | /registeruser | POST |
| localhost:8093 | /userapi/api/ | /user/{username} | PUT |
| localhost:8093 | /userapi/api/ | /user/resetpassword/{username} | PUT |
| localhost:8093 | /userapi/api/ | /user/{username} | DELETE |
| localhost:8093 | /userapi/api/ |  //user/deleteall | DELETE |
| localhost:8093 | /userapi/api/ |  //user/{username} | GET |

                                Table. 5 UserAPI Service  on Tomcat Server and Digital Ocean

        Our critical technique is to test the system is model-based testing. We have used ModelJUnit[4] test tool to test the system. ModelJUnit considers model of ExchangeRate as Finite State Machine. Users makes GET requests to urls on Table 1 to get rank of banks. Our main problem was whether system will behave correctly with different inputs to ExchangeRates. The inputs may vary by request body and URLs of Dataprovider.

        Automated test generation method is explained in Design Approach Section. ModelJUnit library is used to execute this method on exchangeratesMBT module. The library takes a Model the model is explained below. Then it , executes tests as follows on the code:

![Alt text](/screenshots/fig7.png?raw=true " Fig 7. exchangeRatesMBT main method")
                        Fig 7. exchangeRatesMBT main method

 UserTester class takes a model which is explained before. Then some coverage metrics added to tester. These are discussed in Result and Discussion section. generate() method length is 500. 500 iteration happens in this test model.

        **Technical, Operational and Financial Feasibility**

Financial Feasibility:

        There is a Digital Ocean Ubuntu VM instance. The instance has 2GB RAM 60 GB storage and 2CPU for datacollector component to collect data. This instance price is 15$. This is a feasible cost. However, they may be extra cost for other bank service if added. Some of banks sell currency rates services.

Operational Feasibility:

        The system is not stable for now since there is only one instance for datacollector. If there is an error case, data is lost. The problem can be solved by installing an alternative instance in case of error.

Technical Feasibility:

The system works properly with existing libraries. However, some libraries can seem unnecessary since version problems different libraries and drivers. Although it is feasible, some enhancements must be done to lighten the system.



**Knowledge &amp; Skill Set**

**       **  **CS102:** Helped us to use object oriented logic

**        CS201:** Helped us to different data structure to make the system high performance

        **CS222:** Helped us to clean code the program and adopt changes by refactoring

        **CS399:** Helped us to understand the basics of network via HTTP

**        CS468:** Using cloud based systems

**Engineering Standards**

- Data transfer format between components: JSON
- Web  service architecture: REST
- HTTP commands: GET,POST,DELETE,UPDATE
- Web service authentication: OAuth 2.0

**Limitations**

- YKB API limits the request traffic as 5 requests per second and 10000/day
- Our solution works only for USD-TL currency
- Different values cannot be manipulated from config structure provided





1. **V.**** Results and Discussion**



The composite service modules are explained in previous sections. Theses modules works properly except some of bank service. IS Bank and DenizBank service can have errors while persisting the data. They are unstable. The problems fixed. Dataprovider serves the data if there is no error in provided urls. Banks are graded with letter grades and they are returned as RESTful API response in JSON format. As it can be seen in Fig. 4. The components of the exchangerates works properly except for some urls in dataprovider component. If there is a monthly rank request is made to dataprovider, dataprovider fails to response since one month data is too large to process. This  kind of problems will be solved in future works.

Apart from the core part of the service, test generation method is enhanced via ModelJUnit. The model and test model work logic is explained before. Results of tests will be discussed in this section.

![Alt text](/screenshots/fig8.png?raw=true "Fig 8. Test coverage output of ModelJUnit after 500 iterations)
                Fig 8. Test coverage output of ModelJUnit after 500 iterations



The results show that all explored states are covered. Also actions are covered except changeRole(). If the test model is run again , other action is not covered. There may be a mistake in design. However, it can be covered running test again. Also , transitions are covered and no exceptions are encountered

1. **VI.**** Related Work**

In the project our main issue is Composite RESTful Web Service. The second issue is testing the system with model based approach. We implemented this method on banks&#39; exchange rates to compare them. Apart from RESTful approach on our system. There is a kind of solution to comparing banks exchange rates on some web sites[6]. This web sites do not have RESTful architecture. Secondly, the web sites only shows USD-TL and EUR-TL generally. However, our project have only one currency as USD-TL but it can be extended according to currencies supported by banks&#39; web service.

Core logic of ExchangeRates is discussed. Our main focus was composition of RESTful web services. We have applied this approach on banks&#39; web services. Rathod, Daria and Parikh(2015) SOAP architecure was used to composite web services[7]. However , composition of RESTful services rise by distributed systems. In light of this information, the approach is comparably new. Also, SOAP architecture was dominant in previous years. Therefore, we could not able to solve related problems in development stage rarely. Then, ModelJUnit is used to implement model based testing. There is an alternative for this GraphWalker [8]. It could be chosen instead of ModelJunit. In fact we have tried to implement this but it seemed a little bit complex. It is a great tool for large systems. Our system has a couple of  components so that model has a couple of states. Therefore, ModelJUnit is chosen for its simplicity.

The tools we used varied in this project. We had many problems with them since we have tried to combine a lot of tools. This causes a lot of versioning problems across the program. This happened, for Selenium and the browser drivers for them. Then , we switched it to REST API based modelJUnit tests instead of doing them on the browser. It is more efficient if there is only REST requests. Besides that, the whole project is converted to Spring boot project which is quite effective for building RESTful web services and deploying them into an embedded Spring boot application server.

The rest of tools and techniques are definitely critical for system due to tasks they have completed.





- **●●**** Future Work**

                We accomplished key parts of the projects. ExchaneRates works properly and returns its result. Also, UserAPI is running properly and authenticates and authorizes users properly. There are still some missing parts.

- Model testing is not sufficient. It is effective for overall the system. However, there can be added for a specific test case for UserAPI in ModelJUnit.

- Monthly rank request error will be fixed by implementing a solution on calculating standard deviation of large stream data.

**Acknowledgements**

We would like to thank our supervisor dear Hasan Sözer for his help to our project from the beginning and for his understanding and guidance. Secondly, we would like to thank software engineers where we both accomplished our internships and part time work at  NETAŞ. Also, we would like to thank to Furkan Kıraç for his contribution to understand the logic behind project process in CS402 lecture.

**References**

[1] Currencies and Stocks Information Web Site - Turkish Banks online pay-desk currencies(USD-TL), Retrieved May 19, 2019 from  [https://dovizborsa.com/banka/](https://dovizborsa.com/banka/) .

[2] Ege Haber - Spreads on USD-TL among several banks. [https://www.egehaber.com/ekonomi/bankalarda-dolar-alis-satis-fiyati-makas-farki-h238041.html](https://www.egehaber.com/ekonomi/bankalarda-dolar-alis-satis-fiyati-makas-farki-h238041.html)

The list of references that are cited in the text should be provided here.

[3] YKP API limitations - [https://apiportal.yapikredi.com.tr/api-catalog](https://apiportal.yapikredi.com.tr/api-catalog)

[4] ModelJUnit [https://github.com/ryanberckmans/modeljunit/tree/master/modeljunit](https://github.com/ryanberckmans/modeljunit/tree/master/modeljunit)

[5] Sample usage of selenium with ModelJUnit -

[http://www.cse.chalmers.se/edu/year/2015/course/DAT260/labs/modeljunit-tutorial.html](http://www.cse.chalmers.se/edu/year/2015/course/DAT260/labs/modeljunit-tutorial.html)

[6] Web site for exchange rate comparison - [https://dovizborsa.com/banka/](https://dovizborsa.com/banka/)

[7] Towards Composition of RESTful Web Services

[https://ieeexplore.ieee.org/document/7395237/references#references](https://ieeexplore.ieee.org/document/7395237/references#references)

[8] GraphWalker Model-Based Test Tool - [http://graphwalker.github.io/MBT\_How\_to/](http://graphwalker.github.io/MBT_How_to/)

[9] JSON file generators - [http://www.objgen.com/json](http://www.objgen.com/json) , [https://www.json-generator.com/](https://www.json-generator.com/)

**Appendix**

1-) ExchangeRates web service response if a user makes GET request to [http://167.99.209.254:8080/Composite/rest/getComposite/](http://167.99.209.254:8080/Composite/rest/getComposite/) (Digital Ocean remote server) or to [http://localhost:8080/Composite/rest/getComposite/getRates](http://167.99.209.254:8080/Composite/rest/getComposite/getRates) (localhost)
