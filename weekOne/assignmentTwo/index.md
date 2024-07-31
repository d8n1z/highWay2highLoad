# Assignment Two

## Task

- Quoting from the assignment doc, the given task is as follows:

```
Aşağıdaki projelerden bir tanesini seçiniz ve belirtilen fonksiyonel gereksinimlere uygun mimari gereksinimleri belirleyinioz 
```

- Project Selection:
    - [x] Smart Home
    - [ ] Online Whiteboard
    - [ ] Teach Me AnyThing

## Functional Requirements

- Quoting from the assignment doc, the functional requirements, for the selected project, are already given as below:

```yaml
- Cihaz Kontrolü 
    - Kullanıcıların akıllı ev aletlerini açma, kapatma ve ayarlarını değiştirme yeteneği. 
- Uzaktan Erişim 
    - Kullanıcıların mobil cihazlarını kullanarak herhangi bir yerden akıllı ev aletlerine erişim sağlayabilmesi. 
    - Uzaktan izleme ve kontrol özelliği ile ev aletlerini mobil uygulama üzerinden etkinleştirme veya devre dışı bırakma.
Mimari Gereksinimler 
- Otomasyon ve Senaryolar 
    - Kullanıcıların belirli senaryoları veya otomasyon kurallarını tanımlayarak akıllı ev aletlerini belirli koşullara göre otomatik olarak kontrol etmelerini sağlama. 
    - Örneğin, belirli bir saatte ışıkların otomatik olarak kapanması veya belirli bir sıcaklıkta klimanın otomatik olarak açılması gibi. 
- Enerji Verimliliği 
    - Enerji tüketimini izleme ve raporlama yeteneği. 
    - Kullanıcılara enerji tasarrufu yapmalarına yardımcı olacak öneriler sunma. 
- Çoklu Cihaz Desteği 
    - Birden fazla akıllı cihazın tek bir mobil uygulama üzerinden yönetilebilmesi. - Farklı üreticilerin cihazlarını destekleme yeteneği (örneğin, farklı marka akıllı prizler veya ampuller). 
- Uyarılar ve Bildirimler 
    - Kullanıcılara cihazlarla ilgili güncellemeler, hata bildirimleri ve uyarılar gönderme yeteneği. 
- Kullanıcı Kimlikleri ve Yetkilendirme 
    - Kullanıcıların mobil uygulamaya giriş yapması ve akıllı ev cihazlarını kontrol etmek için yetkilendirilmesi için kullanıcı kimlikleri ve güvenli oturum yönetimi. 
- Entegrasyonlar 
    - Diğer akıllı ev cihazları veya platformlarla entegrasyon yeteneği, kullanıcıların çeşitli cihazları tek bir arayüzden kontrol etmelerini sağlar. 
- Güvenlik 
    - Cihazlara ve kullanıcı verilerine yönelik güvenlik önlemleri, şifreleme ve kimlik doğrulama gibi koruma önlemleri alınmalıdır.
- Kullanıcı Arayüzü 
    - Kullanıcı dostu bir mobil uygulama arayüzü, kullanıcıların cihazları kolayca kontrol edebilmeleri için önemlidir. 
- Veri Saklama ve Geçmiş 
    - Kullanım geçmişi ve cihaz verilerini saklama ve raporlama yeteneği. 
- Mobil Uyumluluk 
    - İOS ve Android gibi farklı mobil işletim sistemlerini destekleme yeteneği. 
```


## Work Done

### Non-Functional Requirments (NFRs)

1. **Performance:**
- **Requirement:** The system should respond to user actions within an acceptable timeframe.
- **Architectural Requirement:** 
    - Implement efficient data processing and retrieval mechanisms.
    - Optimize network communication for real-time updates.
- **Technology:** 
    - **Backend:** Use an asynchronous processing framework (e.g., Node.js, Spring Boot with reactive programming).
    - **Database:** Use a time-series database (e.g., InfluxDB, TimescaleDB) for time-stamped data.
    - **Frontend:** Implement efficient state management in the mobile app (e.g., Redux for React Native).

2. **Reliability:**
- **Requirement:** Ensure high availability and minimal downtime.
- **Architectural Requirement:** 
    - Implement redundancy and failover mechanisms.
    - Design for fault tolerance in microservices.
- **Technology:** 
    - **Cloud Services:** Use cloud infrastructure with high availability (e.g., AWS EC2 Auto Scaling, Azure Availability Zones).
    - **Database:** Use a replicated setup for the time-series database (e.g., InfluxDB clustering).

3. **Scalability:**
- **Requirement:** Scale horizontally to support an increasing number of devices and users.
- **Architectural Requirement:** 
    - Design microservices to scale independently.
    - Use containerization and orchestration for scalability.
- **Technology:** 
    - **Containerization:** Docker.
    - **Orchestration:** Kubernetes.
    - **Load Balancing:** AWS Elastic Load Balancing (ELB), Nginx.

4. **Maintainability:**
- **Requirement:** Ensure the system is easy to maintain and update.
- **Architectural Requirement:** 
    - Use a modular microservices architecture.
    - Implement CI/CD pipelines for continuous integration and deployment.
- **Technology:** 
    - **CI/CD:** Jenkins, GitLab CI/CD, CircleCI.
    - **Microservices Framework:** Spring Boot, Express.js.

5. **Usability:**
- **Requirement:** Ensure the mobile app is intuitive and easy to navigate.
- **Architectural Requirement:** 
    - Design a user-friendly interface with clear navigation.
    - Implement user feedback mechanisms.
- **Technology:** 
    - **Mobile Framework:** React Native, Flutter.
    - **UI Design Tools:** Figma, Adobe XD.

6. **Interoperability:**
- **Requirement:** Ensure the system can integrate seamlessly with various smart home devices and third-party platforms.
- **Architectural Requirement:** 
    - Design RESTful APIs and use standard communication protocols.
    - Use standard or to-the-spec messages (if there are any, I know in automotive they have vehicle message/signal specification).
    - Implement adapters for different devices.
- **Technology:** 
    - **API Management:** Swagger/OpenAPI for API design.
    - **Communication Protocols:** MQTT, HTTP/REST, CoAP.

7. **Security:**
- **Requirement:** Regularly update security protocols to protect against new threats.
- **Architectural Requirement:** 
    - Implement robust authentication and authorization mechanisms.
    - Encrypt data in transit and at rest.
- **Technology:** 
    - **Authentication:** OAuth2, JWT.
    - **Encryption:** TLS/SSL for data in transit, AES-256 for data at rest. Or mTLS if 'client verification' is critical.
    - **Security Tools:** OWASP ZAP, Snyk for vulnerability scanning.

## Detailed Architectural Requirements and Design Hints

1. **Microservices Architecture:**
- **Hint:** Design services to be loosely coupled with clear domain boundaries.
- **Key Point:** Each microservice should have a single responsibility and communicate via APIs, each must have fallback scenarios (fail-fast, fail-safe mechanisms), retry mechanisms, fault tolerance, explicable/intpreteable logging/feedback mechaisms.
- **Technology:** Spring Boot, Express.js.

2. **API Gateway:**
- **Hint:** Use an API gateway to centralize API management.
- **Key Point:** Handle authentication, routing, and rate limiting at the gateway level.
- **Technology:** AWS API Gateway, Kong.

3. **Real-Time Communication:**
- **Hint:** Use WebSockets or MQTT for real-time communication.
- **Key Point:** Ensure low latency and efficient message handling.
- **Technology:** MQTT broker (e.g., Mosquitto), WebSocket with Socket.IO.

4. **Data Storage:**
- **Hint:** Use a time-series database for time-stamped data, the maintenance/archiving/deep-freezing/compression also implicitly required.
- **Key Point:** Optimize for high write and read throughput, proactively monitor, apply data retention policies, automated archiving, and scalable storage solutions.
- **Technology:** InfluxDB, TimescaleDB, DruidDb, minIO, S3, DynamoDB

5. **Load Balancing:**
- **Hint:** Implement load balancing to distribute traffic and ensure high availability.
- **Key Point:** Use both application-level and network-level load balancers.
- **Technology:** AWS ELB, Nginx, Citrix

6. **Monitoring and Logging:**
- **Hint:** Implement centralized logging and monitoring.
- **Key Point:** Use tools like Prometheus and Grafana for real-time monitoring, and ELK stack for log management.
- **Technology:** Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana).

7. **Mobile Application Framework:**
- **Hint:** Use a cross-platform framework for consistent user experience.
- **Key Point:** Optimize for performance and ensure the app is responsive and intuitive.
- **Technology:** React Native, Flutter (just in case some one desires to maintain a 'dropped-by-google' framework)

8. **Encryption:**
- **Hint:** Encrypt data in transit (using TLS) and at rest.
- **Key Point:** Regularly update and audit encryption protocols.
- **Technology:** TLS/SSL, any other syymetric/assymetric encryption combos and/or hashing schemes.

9. **DevOps Practices:**
- **Hint:** Implement CI/CD pipelines for automated testing, deployment, and monitoring.
- **Key Point:** Use container orchestration for consistent deployments.
- **Technology:** Jenkins, GitLab CI/CD, Kubernetes.

10. **Cloud Infrastructure:**
- **Hint:** Use cloud services for scalable and reliable infrastructure.
- **Key Point:** Leverage managed services to reduce operational overhead.
- **Technology:** AWS, Azure, GCS.


### The Elephants In The Room
 1. **Real-Time Data Processing and Communication:**
   - **Problem:** Ensuring low-latency, high-throughput communication between millions of devices and the central system.
   - **Challenge:** Handling the variability and unpredictability of network conditions while maintaining real-time performance.
   - **Solution Considerations:** Efficient protocols like MQTT, optimized data serialization formats (e.g., Protocol Buffers), edge computing to reduce latency.
   - **Some Ready Tech to Go Just For This One:** Eclipse Zenoh

 2. **Scalability:**
   - **Problem:** Designing a system that can scale horizontally to accommodate a growing number of users and devices.
   - **Challenge:** Ensuring the system remains responsive and reliable as load increases.
   - **Solution Considerations:** Microservices architecture, container orchestration (e.g., Kubernetes), load balancing, and efficient database sharding.

 3. **Interoperability:**
   - **Problem:** Integrating and supporting a wide range of devices from different manufacturers with varying communication protocols.
   - **Challenge:** Creating a unified interface for device management while dealing with heterogeneous protocols and standards.
   - **Solution Considerations:** Developing adapters for different protocols, using standard communication frameworks (e.g., Zigbee, Z-Wave), and implementing a flexible API architecture.

 4. **Security and Privacy:**
   - **Problem:** Protecting user data and ensuring secure communication between devices and the central system.
   - **Challenge:** Addressing threats like unauthorized access, data breaches, and privacy violations.
   - **Solution Considerations:** End-to-end encryption, secure authentication mechanisms (e.g., OAuth2, JWT), regular security audits, and compliance with privacy regulations (e.g., GDPR).

 5. **Energy Efficiency:**
   - **Problem:** Optimizing the energy consumption of devices and the system itself.
   - **Challenge:** Balancing performance with energy efficiency, especially for battery-powered devices.
   - **Solution Considerations:** Energy-efficient algorithms, dynamic power management, and providing actionable insights to users for reducing energy consumption.

 6. **Reliability and Fault Tolerance:**
   - **Problem:** Ensuring high availability and reliability of the system, even in the face of failures.
   - **Challenge:** Designing robust failover mechanisms and minimizing downtime.
   - **Solution Considerations:** Redundant system architecture, distributed databases, automated failover, and real-time monitoring with alerting.

 7. **User Experience:**
   - **Problem:** Creating an intuitive and seamless user interface for controlling and monitoring devices.
   - **Challenge:** Designing a consistent experience across different devices and platforms (e.g., iOS, Android).
   - **Solution Considerations:** User-centric design principles, thorough usability testing, and responsive design techniques.

 8. **Data Management and Analytics:**
   - **Problem:** Storing, processing, and analyzing large volumes of time-series data generated by devices.
   - **Challenge:** Ensuring efficient data retrieval and real-time analytics while managing storage costs.
   - **Solution Considerations:** Using time-series databases (e.g., InfluxDB, TimescaleDB), implementing data compression techniques, and leveraging big data analytics platforms (e.g., Apache Kafka, Spark).

 9. **Automation and Machine Learning:**
   - **Problem:** Developing intelligent automation rules and predictive models to enhance user convenience and energy efficiency.
   - **Challenge:** Ensuring accuracy and relevance of automation scenarios and predictions.
   - **Solution Considerations:** Machine learning algorithms for pattern recognition, user behavior analysis, and implementing feedback loops to continuously improve automation rules.

 10. **Edge Computing:**
   - **Problem:** Processing data locally on devices to reduce latency and bandwidth usage.
   - **Challenge:** Ensuring consistent performance and security across diverse hardware platforms.
   - **Solution Considerations:** Developing lightweight edge computing frameworks, balancing local and cloud processing, and implementing robust synchronization mechanisms.

 11. **Integration with Third-Party Services:**
   - **Problem:** Seamlessly integrating the system with other smart home platforms and services.
   - **Challenge:** Managing API compatibility, data consistency, and security across different services.
   - **Solution Considerations:** Using standardized APIs, developing middleware for integration, and ensuring data synchronization and security.

 12. **Compliance with Standards and Regulations:**
   - **Problem:** Ensuring the system complies with industry standards and government regulations.
   - **Challenge:** Keeping up with evolving regulations and standards.
   - **Solution Considerations:** Regular compliance audits, staying informed about regulatory changes, and designing the system to be adaptable to new requirements.

### Honorable Mentions Of Free Open Source Tech

From Eclipse:
- Eclipse Zenoh: Zero Overhead Network Protocol. (this is the real deal, in my hometown)
- Eclipse Kapua: Eclipse Kapua™ is a modular integration platform for IoT devices and smart sensors that aims at bridging Operation Technology with Information Technology
- Eclipse Kura: Eclipse Kura™ is an extensible open source IoT Edge Framework based on Java/OSGi. Kura offers API access to the hardware interfaces of IoT Gateways
- Eclipse Hono (Not Actively Maintained): Eclipse Hono™ provides remote service interfaces for connecting large numbers of IoT devices to a back end and interacting with them in a uniform way regardless of the device communication protocol.
- Eclipse Ditto (Not Actively Maintained): Eclipse Ditto™ is a framework for providing the "Digital Twin" pattern for IoT applications in order to interact with IoT devices.

Other FOSS solutions:
- Postgres, Mongo: Both have support and some quality benchmarks for high frequency near-real time, time-series data (afaik)
- k3s, kubeEdge
- All Pivotal Spring projects and/or NestJS for microservices backend.

From 'my brief time in Grid Software':
- Apache Druid (handling the data), backed by Apache Kafka bundled with Apache Superset (visualizing said data) backed my minIO (object storage: data deepfreeze) running in k8s.

Or in a galaxy far far away:
- WasmEdge: Bring the cloud-native and serverless application paradigms to Edge Computing. (this is an out-of-spectrum suggestion, i would like to complement it with WebAssembly as we are kind of 'dreaming' in this bullet point)


### A Probable Sprint Zero Topology

>*Believe me sir, I tried to reflect and populate but then again 'time' has been proven to be the scarcest resource*