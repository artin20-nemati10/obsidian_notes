# Waterfall Model
#Waterfall_model
1. Analysis
2. Design
3. Implementation
4. Testing
5. Maintenance

- A traditional approach of software development.
- Development happens in a step by step manner
### Waterfall model Disadvantages:
- A huge gap inside the coding and agreement
- Takes a very long time for developing codes
- It's difficult to deploy & give feedback of testing
- Any new requirements will restart the cycle
- If client is unhappy with product again cycle will restart
- Until all requirements are not clear project can't start
# Agile Model
#Agile_model
- Programmers create prototypes to clear customer requirements
- Customer provides a feedback & List of changes to be made
It makes the Waterfall model model in small pieces.

==***Agile* X**== or ***==Scrum==*** is one of the most famous model of Agile that companies use it
a lot. In Agile X we have a pieces in two weeks that called ***==Sprints==***. 

### How ==Agile== model works:
1. Requirements
2. Design
3. Develop
4. Test
5. Deploy
6. Review
7. Launch
8. Requirements
9. Design
10. Develop
11. Test
12. Deploy
13. Review
14. Launch
15. Repeats
### How Scrum(Agile X) works:
#Scrum
Sprint 1
1. Plan
2. Design
3. Build
4. Test
5. Review
6. Release
Sprint 2
7. Plan
8. Design
9. Build
10. Test
11. Review
12. Release
13. Repeats

| _Advantages_                                                           |
| ---------------------------------------------------------------------- |
| Customer requirements are more clear beacause of the constant feedback |
| Product is delivered much faster as compared to Waterfall model        |

| _Disadvantages_                                                            |
| -------------------------------------------------------------------------- |
| Product get tested only on developer computers & not on production systems |
| Developers  & Operations team-work will be broken                          |

# Devops

#DevOps

<span style="font-size:15px;">Client + Requirements _-----Agile-----_ Development +Testing _-----DevOps-----_  Operation + infrastucture</span>
---
**Agile addressed the gap between Customers & Developers**

**DevOps addressed the gap between Developers & Operation**


| ***Develop***  | ***DevOps*** | ***Infrastructure*** |
| :------------: | :----------: | :------------------: |
|   *Frontend*   |    *SRE*     |      *SysAdmin*      |
|   *Backend*    |   *DevNet*   |   *Virtualization*   |
|   *Test QA*    | *DevSecOps*  |      *Network*       |
| *Scrum master* |              |      *Security*      |
| *Project mgr*  |              |        *Noc*         |
| *Product mgr*  |              |      *DB Admin*      |
|                |              |     *Cloud Eng*      |
*SRE = Site Reliability Engeneer*
## DevOps Pipeline

#Pipeline
**Dev:**
1. *Plan*                                         
2. *Develop (Code)* **--->** Gitlab
3. *Build*
4. *Test*
***Ops:***
5. *Release* ---> Integrate
6. *Deploy* ---> Docker
7. *Operate*  ---> Scale, Add to Monitoring, Ansible, Bash scripting
8. *Monitor*
---
### **Dev** *(CI) (Build Process)*:


|     ***Plan***      |          ***Develop***          |       ***Build***        |      ***Test***      |
| :-----------------: | :-----------------------------: | :----------------------: | :------------------: |
|   *Requirements*    |             *Code*              | *Continuous integration* |        *Uat*         |
| *Workflow planning* | *shared source code repository* |    *Error Detection*     |     *Performing*     |
|    *Task Lists*     |        *Version control*        |    *Automated tests*     |    *Load testing*    |
|      *Sprints*      |                                 |                          | *Continuous testing* |


| ***Plan***        | ***Develop***                 | ***Build***            | ***Test***         |
| ----------------- | ----------------------------- | ---------------------- | ------------------ |
| *Requirements*      | *Code*                          | *Continuous integration* | *Uat*                |
| *Workflow planning* | *shared source code repository* | *Error Detection*        | *Performing*         |
| *Task Lists*        | *Version control*               | *Automated tests*        | *Load testing*       |
| *Sprints*           |                               |                        | *Continuous testing* |


---
### **Ops** *(CD) (Deploy Process)*:

|   **Release**    |       **Deploy**       |    **Operate**     |    **Monitor**    |
| :--------------: | :--------------------: | :----------------: | :---------------: |
|   *Repository*   | *Blue_green Strategy*  |   *Environment*    | *Infrastructure*  |
| *Schedule Plan*  |    *Configuration*     |   *Notification*   |    *Feedback*     |
| *Micro-Services* | *Automated deployment* | *Recovery Logging* | *Data Collection* |
|                  |     *Multi Level*      |                    |  *Productivity*   |

---


