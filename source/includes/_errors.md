# Errors

The firstbird API uses the following error codes:

| Error Code | Meaning                                                                               |
|:-----------|:--------------------------------------------------------------------------------------|
| 0000       | Unhandled error                                                                       |
| 0999       | This functionality is not implemented right now                                       |
| 4000       | A query parameter is invalid                                                          |
| 4001       | One of the fields requested in fields query parameter is not allowed for that request |
| 4002       | The validation of your request failed                                                 |
| 4003       | One of the path variables is invalid                                                  |
| 4004       | Inviting a User failed                                                                |
| 4005       | The company domain name is not allowed                                                |
| 4006       | The requested email address is already in use for your company                        |
| 4007       | The social network token for a user is invalid                                        |
| 4010       | The request was unauthorized                                                          |
| 4020       | The provided file was empty                                                           |
| 4030       | The used access token in Authorization HTTP header has been blacklisted.              |
| 4031       | The request contained illegal arguments                                               |
| 4032       | The invitation limit for one request exceeded                                         |
| 4041       | The requested company does not exist                                                  |
| 4042       | The requested applicant does not exist                                                |
| 4043       | The requested job application does not exist                                          |
| 40431      | The requested job application file does not exist                                     |
| 4044       | The requested file does not exist                                                     |
| 4045       | A password reset request does not exist for the current user                          |
| 4046       | The requested invitation does not exist                                               |
| 4047       | The requested social network is not connected for the current user                    |
| 4048       | The requested activity feed does not exist                                            |
| 4049       | The requested user does not exist                                                     |
| 40410      | The provided password for checking your current password is invalid                   |
| 4290       | Too many requests to social networks                                                  |
| 5001       | We were not able to create the provided resource                                      |
| 5002       | We failed connecting you to the requested social network                              |
