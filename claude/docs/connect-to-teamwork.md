# Connect to Teamwork

                                                                                         
                                                                                                                                                  
⏺ It looks like the MCP server isn't authenticated. The Teamwork MCP tools require credentials to be configured.
                                                                                                                                                  
  To fix this, make sure your environment has the proper credentials set:                                                                         
                                                                                                                                                  
  - STDIO mode: Set TW_MCP_BEARER_TOKEN to your Teamwork API token                                                                                
  - HTTP mode: The server needs a valid Bearer token in the request

  You can check your .env or local.yml for the current configuration, or refer to claude/docs/connect-to-teamwork.md for setup instructions.

## CURL Call

```bash
curl -u "twp_ZXGh4V1enGvV8kK0NM8IMasU8RPR:X" \
     -H "Content-Type: application/json" \
     -X GET "https://theapiguys.teamwork.com/projects.json"
```

## Response:

```json
{
    "STATUS": "OK",
    "projects": [
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "6162",
                "name": "Internal"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2015-08-28T12:33:55Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "API Guys internal work, including work on our own business processes, sales, and customer service work for clients without active projects.",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548476",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": false,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-09T18:14:34Z",
            "lastWorkedOn": "2025-09-16T14:05:39Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "Administration",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10207"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "179085",
                "is-owner": "0",
                "name": "Adventures in Writing"
            },
            "created-on": "2019-12-02T18:58:52Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "549485",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T19:28:00Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "AIW Portal",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10250"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "190643",
                "is-owner": "0",
                "name": "IAB"
            },
            "created-on": "2022-02-18T00:11:14Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "654988",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2024-02-26T20:27:56Z",
            "lastWorkedOn": "2023-03-16T15:54:04Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "AML Complete",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10278"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "184941",
                "is-owner": "0",
                "name": "Art Moki LLC"
            },
            "created-on": "2019-03-20T19:38:27Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "This project reflects ongoing work on the Class List Portal for Marvegos.\n\nhttps://docs.google.com/document/d/1BfXicNAxOgI6rw6yDq2BTKv0E0efhG-y3l6-zJHF_PQ/edit?usp=sharing\n\n<https://apiguys.harvestapp.com/projects/20558220>  \n<https://tv101.infusionsoft.com.infusionsoft.com/Opportunity/manageOpportunity.jsp?view=edit&ID=2441>",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548455",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-06T22:05:16Z",
            "lastWorkedOn": "2026-03-02T14:40:40Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Art Moki - Marvegos",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10327"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2022-08-22T19:55:58Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "The mystery of the SyncThing has yet to be solved. Rumors of the mysterious beast have been told throughout time but there are no recorded instances of it to date. Where will it be spotted next?",
            "endDate": "20220911",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "673696",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-10-08T15:56:50Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "ASyncThing",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20220822",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10344"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "196049",
                "is-owner": "0",
                "name": "Big Quiz Thing"
            },
            "created-on": "2022-10-19T20:50:36Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20260205",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "679274",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-06T22:48:06Z",
            "lastWorkedOn": "2025-02-13T22:00:01Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Big Quiz Thing - TriviaTies",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20221019",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10427"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "198260",
                "is-owner": "0",
                "name": "Corentus"
            },
            "created-on": "2024-12-04T18:55:03Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "743800",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": false,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2024-12-16T14:42:31Z",
            "lastWorkedOn": "2024-12-16T14:43:08Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Corentus Course Move",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10465"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "197904",
                "is-owner": "0",
                "name": "Daha Wellness"
            },
            "created-on": "2024-09-26T21:21:35Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20250910",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "738913",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-05T03:15:51Z",
            "lastWorkedOn": "2024-09-27T18:39:51Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Daha Wellness",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20240926",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10472"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "38265",
                "is-owner": "0",
                "name": "Diligent Auto Solutions"
            },
            "created-on": "2017-02-14T19:07:42Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "Diligent",
            "endDate": "20251107",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548461",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-10T16:28:55Z",
            "lastWorkedOn": "2026-03-10T16:28:55Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c38265/companyLogo1505842198365643300.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "Diligent",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20200723",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10487"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "6162",
                "name": "Internal"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2023-09-11T19:45:45Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "709313",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": false,
            "isOnBoardingProject": false,
            "isProjectAdmin": true,
            "isSampleProject": false,
            "last-changed-on": "2025-01-29T20:56:57Z",
            "lastWorkedOn": "2024-10-16T13:36:53Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "Documentation",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10510"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "185405",
                "is-owner": "0",
                "name": "The Order of the Daughters of the King®"
            },
            "created-on": "2021-03-02T19:11:53Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "606749",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T19:49:58Z",
            "lastWorkedOn": "2026-02-23T17:22:35Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "DOK",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10517"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "7F8C8D",
                "id": "7465",
                "name": "Archived"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "183305",
                "is-owner": "0",
                "name": "Human Design For Us All"
            },
            "created-on": "2020-09-18T14:06:34Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "582851",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T19:51:47Z",
            "lastWorkedOn": "2026-03-02T14:09:11Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Evolutionary Human Design For Us All",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "190751",
                "is-owner": "0",
                "name": "Funder Trading"
            },
            "created-on": "2022-04-26T17:52:29Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20241030",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "662789",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-12-01T15:04:19Z",
            "lastWorkedOn": "2025-12-01T15:05:12Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Funder Trading",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20220426",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10534"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "",
                "id": "",
                "name": ""
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "185273",
                "is-owner": "0",
                "name": "Prospective Devs"
            },
            "created-on": "2022-12-13T21:05:15Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20221213",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "683964",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": false,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2022-12-14T21:39:58Z",
            "lastWorkedOn": "2022-12-14T21:39:58Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Jotform-Keap Integration Sample Project:",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20221213",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10626"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "187818",
                "is-owner": "0",
                "name": "Naturalcare Cleaning Service"
            },
            "created-on": "2021-09-13T16:05:02Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "636132",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T20:00:00Z",
            "lastWorkedOn": "2024-06-26T13:22:51Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Natural Care Cleaning Service (NCCS)",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10763"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "179328",
                "is-owner": "0",
                "name": "Prosper Trading Academy"
            },
            "created-on": "2018-12-04T20:22:50Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "<https://apiguys.harvestapp.com/projects/19372143>  \r\n<https://tv101.infusionsoft.com.infusionsoft.com/Opportunity/manageOpportunity.jsp?view=edit&ID=2344>",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "551623",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-07-01T19:25:13Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Prosper Trading Company Projects",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "list",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10877"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "6162",
                "name": "Internal"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2015-08-28T12:34:15Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548477",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T14:53:36Z",
            "lastWorkedOn": "2026-03-02T14:58:18Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "Sales/Customer Service",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10922"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "195313",
                "is-owner": "0",
                "name": "Jones Fiduciary Wealth Management"
            },
            "created-on": "2023-10-03T15:10:18Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20231023",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "711172",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2024-03-12T18:16:28Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Shaun Jones: Keap-Ringcentral Integration",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20231003",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10942"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "6162",
                "name": "Internal"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2020-12-16T16:11:32Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "592912",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-03-02T14:41:50Z",
            "lastWorkedOn": "2026-03-02T14:42:19Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "TAG Website",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10975"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "",
                "id": "",
                "name": ""
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "179688",
                "is-owner": "0",
                "name": "Tekton Ministries"
            },
            "created-on": "2023-01-10T21:03:46Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "686066",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-12-02T19:12:09Z",
            "lastWorkedOn": "2025-12-01T15:05:44Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Tekton Ministries Custom Order Form",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10982"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "6162",
                "name": "Internal"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34428",
                "is-owner": "1",
                "name": "The API Guys"
            },
            "created-on": "2021-07-29T15:40:05Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "630707",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-01-20T20:06:47Z",
            "lastWorkedOn": "2024-08-16T14:13:01Z",
            "logo": "https://s3.amazonaws.com/TWFiles/111402/companies/c34428/companyLogo1505841363566500900.png",
            "logoColor": "",
            "logoFromCompany": true,
            "logoIcon": null,
            "name": "Training",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "10995"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34429",
                "is-owner": "0",
                "name": "USPA"
            },
            "created-on": "2020-02-19T16:29:07Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "559368",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2024-11-08T15:00:36Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "USPA Handicap Voting Portal",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "11000"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34429",
                "is-owner": "0",
                "name": "USPA"
            },
            "created-on": "2015-08-28T12:32:46Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548466",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-12-01T15:03:46Z",
            "lastWorkedOn": "2025-12-01T15:03:55Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "USPA Membership Portal",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "11013"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "3D82DE",
                "id": "36486",
                "name": "Ongoing"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "34429",
                "is-owner": "0",
                "name": "USPA"
            },
            "created-on": "2017-07-03T11:36:15Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "USPA",
            "endDate": "",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "548459",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2025-12-01T15:04:00Z",
            "lastWorkedOn": "2025-12-01T15:05:10Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "USPA Tournament Database",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "current",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "11034"
            ]
        },
        {
            "boardData": {},
            "category": {
                "color": "99DF72",
                "id": "37447",
                "name": "Active"
            },
            "company": {
                "currency": {
                    "id": "1",
                    "name": "US dollar",
                    "code": "USD",
                    "symbol": "$",
                    "decimalPoints": "2"
                },
                "currencyId": "1",
                "id": "197138",
                "is-owner": "0",
                "name": "John Pocorobba"
            },
            "created-on": "2024-04-05T17:28:29Z",
            "defaultPrivacy": "open",
            "defaults": {
                "privacy": ""
            },
            "description": "",
            "endDate": "20240405",
            "filesAutoNewVersion": false,
            "harvest-timers-enabled": true,
            "id": "726164",
            "integrations": {
                "onedrivebusiness": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "sharepoint": {
                    "account": "",
                    "enabled": false,
                    "folder": "root",
                    "foldername": "root"
                },
                "xero": {
                    "basecurrency": "",
                    "connected": "NO",
                    "countrycode": "",
                    "enabled": false,
                    "organisation": ""
                }
            },
            "isBillable": true,
            "isOnBoardingProject": false,
            "isProjectAdmin": false,
            "isSampleProject": false,
            "last-changed-on": "2026-02-17T19:44:22Z",
            "lastWorkedOn": "2026-02-17T14:29:46Z",
            "logo": "",
            "logoColor": "",
            "logoIcon": null,
            "name": "Website: John Pocorobba",
            "notifyeveryone": false,
            "overview-start-page": "default",
            "portfolioBoards": [],
            "privacyEnabled": false,
            "replyByEmailEnabled": true,
            "show-announcement": false,
            "starred": false,
            "startDate": "20240405",
            "start-page": "tasks",
            "status": "active",
            "subStatus": "late",
            "tags": [],
            "tasks-start-page": "list",
            "timelogRequiresTask": false,
            "workflowIds": [
                "11103"
            ]
        }
    ]
}
````