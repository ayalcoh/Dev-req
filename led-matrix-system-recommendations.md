# LED Matrix Control System


---

## 1. Executive Summary


---

## 2. System Requirements Analysis

### 2.1 Key Requirements

- **Offline Operation:** LightBox must work without internet connectivity
- **Local Communication:** Mobile app needs direct connectivity to LightBox via Bluetooth LE/WiFi
- **Scalability:** System needs to support deployment from small to large user bases
- **Real-time Control:** MQTT for immediate LED matrix control and updates
- **Firmware Updates:** Ability to remotely update LightBox software
- **Cross-Platform Support:** Flutter app for iOS and Android

### 2.2 Deployment Scenarios

From the PRD, three deployment models were identified:

- **Local Server Mode:** Self-hosted on local network with direct LightBox communication
- **Cloud Server Mode:** AWS EC2 deployment with remote access
- **Hybrid Mode:** Primary local operation with cloud backup/failover

---

## 3. Architecture Approaches

### 3.1 AWS Full Cloud Approach

**Architecture:**
- AWS EC2 for application logic
- AWS RDS for PostgreSQL database
- AWS ElastiCache for Redis
- AWS S3 for file and firmware storage
- EMQX MQTT broker hosted on EC2

### 3.2 Hybrid Approach (Recommended)

**Architecture:**
- Lightweight local server on LightBox
- Local SQLite database and Mosquitto MQTT broker
- AWS services for synchronization and remote access
- S3 for firmware storage and distribution
- Reduced AWS footprint compared to full cloud approach

**Advantages:**
- Works offline with full functionality
- Lower cloud costs
- Better user experience (lower latency)
- Scales effectively
- Future-proof design

**Disadvantages:**
- More complex initial development
- Requires synchronization logic
- Higher local processing requirements

**Monthly Cost Estimates:**
- Small Scale (100 devices): $60-80
- Medium Scale (1,000 devices): $140-160
- Large Scale (10,000 devices): $500-600

---

## 4. Recommended Architecture: Hybrid Approach


### 4.1 Architecture Components


#### 4.1.2 Cloud Components (AWS)
- **EC2 Instances:** Node.js with Express for remote access and administration
- **RDS:** PostgreSQL database for user management and analytics
- **ElastiCache:** Redis for performance optimization
- **S3:** Firmware storage and distribution
- **CloudFront:** Content delivery for web dashboard and firmware

#### 4.1.3 Communication Components
- **Local Communication:** Direct Bluetooth LE/WiFi between mobile app and LightBox
- **Remote Communication:** HTTP/MQTT over the internet when local not available
- **Synchronization:** Periodic state sync between local and cloud when online

### 4.2 Key AWS Services Explained

#### 4.2.1 AWS S3 for Firmware
AWS S3 (Simple Storage Service) provides a scalable, secure system for storing and distributing firmware updates:

**Firmware Storage Process:**
1. You upload new firmware versions to S3 buckets
2. Multiple firmware versions can be maintained (current, previous, beta)
3. Access controls ensure only authorized systems access firmware files
4. Metadata stores information about each version

**Firmware Distribution Process:**
1. When a LightBox needs to update, it downloads firmware from S3
2. S3 can handle thousands of simultaneous downloads
3. The update process includes verification and installation
4. Update success/failure is reported back to the backend

**Benefits for Your System:**
- Cost-effective storage (~$0.023/GB/month)
- 99.999999999% durability for firmware files
- Built-in security features
- Scalability to handle any number of devices
- Global availability

#### 4.2.2 Other Key AWS Services

**EC2 (Elastic Compute Cloud):**
- Provides virtual servers in the cloud
- Hosts your backend application logic
- Scalable to match user demand
- Can be configured for high availability

**RDS (Relational Database Service):**
- Managed PostgreSQL database
- Stores user accounts, LightBox registrations, settings
- Automated backups and maintenance
- Scaling options as user base grows

**ElastiCache:**
- Managed Redis service
- Improves performance through caching
- Reduces database load
- Enables real-time features

---

## 5. Implementation Strategy

### 5.1 Phased Implementation

#### Phase 1: Core LightBox Functionality
- Implement local communication (Bluetooth/WiFi)
- Develop local MQTT controls
- Create basic mobile app interface
- Build local processing logic

#### Phase 2: Cloud Integration
- Set up AWS infrastructure
- Implement user authentication
- Enable device registration
- Create firmware update mechanism via S3

#### Phase 3: Enhanced Features
- Develop synchronization system
- Add analytics and monitoring
- Implement web dashboard
- Optimize performance

### 5.2 Development Priorities

1. **Connectivity First:** Ensure robust local connectivity
2. **Core Features:** Implement essential LED control functionality
3. **Online/Offline Sync:** Develop synchronization between local and cloud
4. **Advanced Features:** Add additional capabilities after core system is stable

---

## 6. Cost Optimization Strategies

### 6.1 Immediate Cost Controls
- **Start Small:** Begin with minimal cloud infrastructure
- **Reserved Instances:** For predictable workloads, use reserved instances (40-60% savings)
- **Reduce Communication Frequency:** Batch updates, implement delta sync (30-40% savings)

### 6.2 Scale-Based Optimizations
- **Tiered Storage:** Store recent data in fast storage, archive older data (20-30% savings)
- **Regional Deployments:** Deploy in regions closer to users
- **Auto-scaling:** Implement auto-scaling to match demand

### 6.3 Long-term Cost Management
- **Regular Monitoring:** Set up cost alerts and dashboards
- **Performance Tuning:** Optimize queries and processing
- **Rightsize Resources:** Regularly review and adjust resource allocation

---

## 7. Conclusion

The hybrid architecture combining local processing on the LightBox with cloud synchronization offers the optimal balance of functionality, cost, and scalability for the LED Matrix Control System. This approach ensures:

1. Full functionality in offline environments
2. Low-latency direct control of LED matrices
3. Scalable cloud integration for remote access
4. Cost-effective operation at all scales
5. Future-proof design that can evolve with requirements

By implementing this architecture in phases and following the recommended cost optimization strategies, you can build a robust, scalable system that meets both current requirements and future needs.

---

## 8. Next Steps

1. Finalize the LightBox hardware specifications
2. Develop a detailed technical specification for the local server component
3. Create a proof-of-concept for the local-cloud synchronization
4. Set up a development AWS environment
5. Begin implementation of the Phase 1 components

---

**Document Prepared: March 9, 2025**
