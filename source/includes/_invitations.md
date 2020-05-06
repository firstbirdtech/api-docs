# Invitations

Invitations allow you to invite people to join your company

## Create an Invitation

This endpoint lets you create a new invitation 

### HTTP Request 

> This is an example request body

```json
{
    "email": "test.user@firstbird.com",
    "locale": "en_US",
    "message": "hey, would you like to join our company?",
    "role": "ROLE_TALENT_SCOUT"
}
```

`POST /v1/companies/{companyId}/invitations`