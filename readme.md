# Method password forgot
### Send reset-password link
## HTTP request
```code
	POST https://api.voicer.software/api/v1/auth/password-forgot
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "data": {
    "description": "forgot password data",
    "name": "data",
    "in": "body",
    "required": true,
    "type": "object",
    "properties": {
      "email": {
        "type": "string"
      },
      "languageCode": {
        "type": "string"
      }
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/auth/password-forgot' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token`' \
--data '{
  "email": "<string>",
  "languageCode": "<string>"
}'```"
"# Method Reset Password
### Reset password
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/auth/password-reset?code=
	Content-Type: application/json
	Accept: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `code`| string | Yes |                       reset code  |
## Request body
```json
{
  "password": "<string>",
  "passwordConfirmation": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "Password changed",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/auth/password-reset?code=' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
    "password": "<string>",
    "passwordConfirmation": "<string>"
}'```"
"# Method Register new user
### Register new user
## HTTP request
```code
	POST https://api.voicer.software/api/v1/auth/register
	Content-Type: application/json
```
## Request body
```json
{
  "data": {
    "description": "register data",
    "properties": {
      "email": {
        "type": "string"
      },
      "name": {
        "type": "string",
        "maxLength": 255
      },
      "password": {
        "type": "string",
        "minLength": 3
      },
      "passwordConfirmation": {
        "type": "string",
        "minLength": 3
      }
    },
    "required": [
      "email",
      "name",
      "password",
      "passwordConfirmation"
    ]
  }
}
```
## Response body (code 200)
```json
{

}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/auth/register''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--data '''{
  "email": "<string>",
  "name": "<string>",
  "password": "<string>",
  "passwordConfirmation": "<string>"
}'''"
"# Method get bot autoreply
### Get bot autoreply if chat is inactive based on defined conditions
## HTTP request
```code
    GET https://api.voicer.software/api/v1/bots/autoreply?chatID=<chat_id>&companyID=<company_id>
    Authorization: Bearer Token
    Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------------------------- |
| `chatID`| string | Yes |                       Chat ID  |
| `companyID`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Autorply model",
  "type": "object",
  "properties": {
    "text": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/bots/autoreply?chatID=<chat_id>&companyID=<company_id>''' \
--header '''Authorization: Bearer Token''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json'''
```"
"# Method upload attachment for chat
### Upload attachment and returns link to uploaded file
## HTTP request
```code
	POST https://api.voicer.software/api/v1/reviews/chat/attachments
	Content-Type: multipart/form-data
	Authorization: Bearer Token
```
## Query parameters
No query parameters
## Request body
```json
{
  "attachment": {
    "type": "file",
    "description": "attachment",
    "name": "attachment",
    "in": "formData",
    "required": true
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "DeleteUrl": {
      "type": "string"
    },
    "attachmentType": {
      "$ref": "#/definitions/domain.AttachmentType"
    },
    "attachmentUrl": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/reviews/chat/attachments''' \
--header '''Content-Type: multipart/form-data''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--form '''attachment=@<path_to_file>'''
```"
"# Method get chat log for review
### Get chat log for review
## HTTP request
```code 
	GET https://api.voicer.software/api/v1/reviews/{id}/chat
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| string | Yes |                       Review ID  |
## Response body (code 200)
```json
{
  "description": "Chat model",
  "type": "object",
  "properties": {
    "clientID": {
      "type": "integer"
    },
    "log": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/dtos.ChatLogEntry"
      }
    }
  }
}
```
## CURL Requests 
```code 
curl --location --request GET 'https://api.voicer.software/api/v1/reviews/{id}/chat' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--header 'id: <id>'
```"
"# Method send message to chat
### Send message to chat
## HTTP request
```code
	POST https://api.voicer.software/api/v1/reviews/{id}/chat
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| string | Yes |                       Review ID  |
## Request body
```json
{
  "message": {
    "attachmentUrl": "<string>",
    "close": <boolean>,
    "text": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example":"OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/reviews/{id}/chat' \
--header 'Authorization: Bearer Token` \
--header 'Content-Type: application/json' \
--data-raw '{
    "message": {
        "attachmentUrl": "<string>",
        "close": <boolean>,
        "text": "<string>"
    }
}'```
Please replace `{id}` with the actual value of the review ID you want to send a message to."
"# Method get full chat history by review ID
### Get full chat history by clientID
## HTTP request
```code
	GET https://api.voicer.software/api/v1/reviews/{id}/chat/history
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| string | Yes |                       Review ID  |
## Response body (code 200)
```json
{
  "description": "Chat history model",
  "type": "object",
  "properties": {
    "history": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/dtos.ChatLogEntry"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/reviews/{id}/chat/history''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''"
"# Method list chat bots for a company
### List chat bots for a company
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{company_id}/chat-bots
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `company_id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "ChatTemplate domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "companyID": {
        "type": "integer"
      },
      "createdAt": {
        "type": "string"
      },
      "fullhistoryURL": {
        "type": "string"
      },
      "historyURL": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "link": {
        "type": "string"
      },
      "sendURL": {
        "type": "string"
      },
      "type": {
        "$ref": "#/definitions/domain.BotType"
      },
      "updatedAt": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{company_id}/chat-bots' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--path-variable 'company_id:<integer>'```"
"# Method List chat templates for a company
### List chat templates for a company
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{company_id}/chat-templates
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `company_id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "ChatTemplate domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "company_id": {
        "type": "integer"
      },
      "content": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "key": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{company_id}/chat-templates' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'
```
To replace `{company_id}` with the actual value, please provide the specific ID of the company."
"# Method create new chat template
### Create new chat template
## HTTP request
```code
	POST https://api.voicer.software/api/v1/companies/{company_id}/chat-templates
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `company_id`| integer | Yes |                       Company ID  |
## Request body
```json
{
  "content": "string",
  "key": "string"
}
```
## Response body (code 200)
```json
{
  
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/companies/{company_id}/chat-templates''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token``` --data '''{
  "content": "<string>",
  "key": "<string>"
}'''```"
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method store form client
### Store form
## HTTP request
```code 
	POST https://api.voicer.software/api/v1/client
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "data": {
    "description": "client",
    "name": "data",
    "in": "body",
    "required": true,
    "type": "object",
    "properties": {
      "answers": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/client.StoreRequestAnswerData"
        }
      },
      "formID": {
        "type": "integer"
      },
      "sessionID": {
        "type": "string"
      },
      "status": {
        "type": "integer"
      }
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "Created",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code 
curl --location --request POST 'https://api.voicer.software/api/v1/client' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token` \
--data-raw '{
  "formID": <integer>,
  "sessionID": "<string>",
  "answers": [
    {
      "<client.StoreRequestAnswerData>": {}
    }
  ],
  "status": <integer>
}'```"
"# Method get form field
### Show form field
## HTTP request
```code
	GET https//api.voicer.software/api/v1/client/forms/{form_id}/fields/{field_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `form_id`| integer | Yes |                       Form ID  |
| `field_id`| integer | Yes |                       Field ID  |
## Response body (code 200)
```json
{
  "description": "Form field",
  "type": "object",
  "properties": {
    "answers": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.AnswerOption"
      }
    },
    "createdAt": {
      "type": "string"
    },
    "fieldID": {
      "type": "integer"
    },
    "formID": {
      "type": "integer"
    },
    "id": {
      "type": "integer"
    },
    "options": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "question": {
      "type": "string"
    },
    "styles": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "type": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https//api.voicer.software/api/v1/client/forms/{form_id}/fields/{field_id}' \
--header 'Authorization: Bearer Token`'```"
"# Method get client form by slug
### Show form
## HTTP request
```code
	GET https://api.voicer.software/api/v1/client/{slug}?lang=<language>&session=<session_ID>
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `slug`| string | Yes |                       Form slug  |
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `lang`| string | No |                       Language  |
| `session`| string | No |                       Session ID  |
## Response body (code 200)
```json
{
  "description": "Review response",
  "type": "object",
  "properties": {
    "bots": {
      "$ref": "#/definitions/responses.ReviewBotsResponse"
    },
    "company": {
      "$ref": "#/definitions/domain.Company"
    },
    "form": {
      "$ref": "#/definitions/domain.Form"
    },
    "languages": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Language"
      }
    },
    "node": {
      "$ref": "#/definitions/domain.Node"
    },
    "sessionID": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/client/{slug}?lang=<language>&session=<session_ID>' \
--header 'Authorization: Bearer Token'
```
Замените `<slug>` на конкретное значение slug.
Замените `<language>` на конкретное значение языка.
Замените `<session_ID>` на конкретное значение ID сессии."
Error: Could not get a response from the API.
"# Method create company
### Create company
## HTTP request
```code
	POST https://api.voicer.software/api/v1/companies
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "company": {
    "alias": "<string>",
    "name": "<string>",
    "enableOverdue": <boolean>
  }
}
```
## Response body (code 200)
```json
{
  
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/companies' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data '{
  "company": {
    "alias": "<string>",
    "name": "<string>",
    "enableOverdue": <boolean>
  }
}'```"
"# Method get company info by id
### Show company
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Company domain model",
  "type": "object",
  "properties": {
    "alias": {
      "type": "string"
    },
    "createdAt": {
      "type": "string"
    },
    "enableOverdue": {
      "type": "boolean"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{id}' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json'
```"
"# Method PUT Update Company
### Update company
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/companies/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                 |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                      Company ID  |
## Request body
```json
{
  "description": "company",
  "name": "company",
  "in": "body",
  "required": true,
  "type": "object",
  "properties": {
    "alias": {
      "type": "string",
      "maxLength": 255
    },
    "enableOverdue": {
      "type": "boolean"
    },
    "name": {
      "type": "string",
      "maxLength": 255
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/companies/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{ 
  '''alias''': '''<string>''',
  '''enableOverdue''': '''<boolean>''',
  '''name''': '''<string>'''
}'''
```"
"# Method delete company id
### Delete company
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/companies/{id}
	Authorization: Bearer Token
	Accept: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/companies/{id}''' \
--header '''Authorization: Bearer Token`''' \
--header '''Accept: application/json'''```"
"# Method GET List all users attached to a company
### List all users attached to a company
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/users
	Authorization: Bearer Token
	Accept: application/json
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `limit`| integer | No |                       Limit of users  |
| `offset`| integer | No |                       Offset of users  |
## Response body (code 200)
```json
{
  "description": "User domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "createdAt": {
        "type": "string"
      },
      "email": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      },
      "nodesCount": {
        "type": "integer"
      },
      "responsibleCount": {
        "type": "integer"
      },
      "updatedAt": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/users''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token` '''\
--header '''Content-Type: application/json''' \
--data-raw '''{
    "limit": <integer>,
    "offset": <integer>
}'''
```"
"# Method get company languages
### Show company languages
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/languages
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Language domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "icon": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{id}/languages' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'
```"
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method create contact
### Create contact
## HTTP request
```code
	POST https://api.voicer.software/api/v1/contacts
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "contact": {
    "clientID": <integer>,
    "client_photo": "<string>",
    "email": "<string>",
    "phone": "<string>",
    "telegramID": "<string>",
    "viberID": "<string>",
    "whatsappID": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "Contact domain model",
  "type": "object",
  "properties": {
    "clientID": {
      "type": "integer"
    },
    "client_photo": {
      "type": "string"
    },
    "createdAt": {
      "type": "string"
    },
    "email": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "phone": {
      "type": "string"
    },
    "telegramID": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    },
    "viberID": {
      "type": "string"
    },
    "whatsappID": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/contacts' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "contact": {
    "clientID": <integer>,
    "client_photo": "<string>",
    "email": "<string>",
    "phone": "<string>",
    "telegramID": "<string>",
    "viberID": "<string>",
    "whatsappID": "<string>"
  }
}'```"
"# Method Store chat in cache
### Store chat in cache
## HTTP request
```code
	POST https://api.voicer.software/api/v1/contacts/chats
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "chatID": "<string>",
  "type": "<string>",
  "uid": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "Success",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/contacts/chats' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token`' \
--data-raw '{
  "chatID": "<string>",
  "type": "<string>",
  "uid": "<string>"
}'```"
"# Method get Contact info by id
### Show contact
## HTTP request
```code
	GET https://api.voicer.software/api/v1/contacts/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Contact ID  |
## Response body (code 200)
```json
{
  "description": "Contact domain model",
  "type": "object",
  "properties": {
    "clientID": {
      "type": "integer"
    },
    "client_photo": {
      "type": "string"
    },
    "createdAt": {
      "type": "string"
    },
    "email": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "phone": {
      "type": "string"
    },
    "telegramID": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    },
    "viberID": {
      "type": "string"
    },
    "whatsappID": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/contacts/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```

Please note that you need to replace `{id}` with the actual ID value of the contact you want to retrieve."
"# Method Update contact
### Update contact
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/contacts/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Contact ID  |
## Request body
```json
{
  "email": "<string>",
  "phone": "<string>",
  "telegramID": "<string>",
  "viberID": "<string>",
  "whatsappID": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl--location --request PUT 'https://api.voicer.software/api/v1/contacts/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "email": "<string>",
  "phone": "<string>",
  "telegramID": "<string>",
  "viberID": "<string>",
  "whatsappID": "<string>"
}'```"
Error: Could not get a response from the API.
"# Method get all contacts by review id
### List all contacts
## HTTP request
```code
	GET https://api.voicer.software/api/v1/reviews/{id}/contacts
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Review ID  |
## Response body (code 200)
```json
{
  "description": "Contact domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "clientID": {
        "type": "integer"
      },
      "client_photo": {
        "type": "string"
      },
      "createdAt": {
        "type": "string"
      },
      "email": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "phone": {
        "type": "string"
      },
      "telegramID": {
        "type": "string"
      },
      "updatedAt": {
        "type": "string"
      },
      "viberID": {
        "type": "string"
      },
      "whatsappID": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/reviews/{id}/contacts''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method get Node count
### Show nodes count, according to the filter
## HTTP request
```code
	GET https://api.voicer.software/api/v1/counts/node?companies=<comma_separated_list_of_company_ids>&sources=<comma_separated_list_of_source_ids>
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `companies`| array | No |                       list of companies ids  |
| `sources`| array | No |                       list of sources ids  |
## Response body (code 200)
```json
{
  "description": "Nodes count",
  "type": "integer"
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/counts/node?companies=<comma_separated_list_of_company_ids>&sources=<comma_separated_list_of_source_ids>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer Token'
```"
"# Method get reviews count
### Show reviews count, according to the filter
## HTTP request
```code
	GET https://api.voicer.software/api/v1/counts/review
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `companies`| array[integer] | No |   list of companies ids  |
| `nodes`| array[integer] | No |   list of nodes ids  |
| `sources`| array[integer] | No |   list of sources ids  |
| `statuses`| array[integer] | No |   list of client statuses  |
| `from`| string | No |   from client created_at, RFC3339  |
| `to`| string | No |   to client created_at, RFC3339  |
## Response body (code 200)
```json
{
  "description": "Reviews count",
  "type": "integer"
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/counts/review' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
    "companies": [array_of_company_ids],
    "nodes": [array_of_node_ids],
    "sources": [array_of_source_ids],
    "statuses": [array_of_client_statuses],
    "from": "from_date_in_RFC3339_format",
    "to": "to_date_in_RFC3339_format"
}'```
Replace `[array_of_company_ids]`, `[array_of_node_ids]`, `[array_of_source_ids]`, `[array_of_client_statuses]`, `from_date_in_RFC3339_format`, and `to_date_in_RFC3339_format` with the actual values you want to use."
Error: Could not get a response from the API.
"# Method List all documents
### List all documents
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/documents
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Document domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "company_id": {
        "type": "integer"
      },
      "created_at": {
        "type": "string"
      },
      "description": {
        "type": "string"
      },
      "file_id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      },
      "updated_at": {
        "type": "string"
      },
      "url": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{id}/documents' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--header 'id: <integer>'
```"
"# Method create document
### Create document
## HTTP request
```code
	POST https://api.voicer.software/api/v1/documents
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `document`| object | Yes |                       Document  |
## Request body
```json
{
  "company_id": {"type":"integer"},
  "description": {"type":"string","maxLength":255},
  "file_id": {"type":"integer"},
  "name": {"type":"string","maxLength":255},
  "url": {"type":"string","maxLength":255}
}
```
## Response body (code 200)
```json
{
  "description": "Document domain model",
  "type": "object",
  "properties": {
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "file_id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    },
    "url": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/documents' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "company_id": <integer>,
  "description": "<string>",
  "file_id": <integer>,
  "name": "<string>",
  "url": "<string>"
}'```"
"# Method get document by id
### Show document
## HTTP request
```code
	GET https://api.voicer.software/api/v1/documents/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Document ID  |
## Response body (code 200)
```json
{
  "description": "Document domain model",
  "type": "object",
  "properties": {
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "file_id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    },
    "url": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/documents/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method Update document by id
### Update document
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/documents/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Document ID  |
## Request body
```json
{
  "description":{
    "type":"string",
    "maxLength":255
  },
  "name":{
    "type":"string",
    "maxLength":255
  },
  "url":{
    "type":"string",
    "maxLength":255
  }
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/documents/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "description": "<string>",
  "name": "<string>",
  "url": "<string>"
}'''```"
"# Method delete document id
### Delete document
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/documents/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Document ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/documents/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''```"
"# Method GET email templates
### List email-templates
## HTTP request
```code
	GET https://api.voicer.software/api/v1/email-templates?limit=<integer>&offset=<integer>
	Authorization: Bearer Token
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `limit`| integer | No |                      Limit of results  |
| `offset`| integer | No |                      Offset for pagination  |
## Response body (code 200)
```json
{
  "description": "EmailTemplates list",
  "type": "array",
  "items": {
    "type": "array",
    "items": {
      "type": "object",
      "properties": {
        "createdAt": {
          "type": "string"
        },
        "id": {
          "type": "integer"
        },
        "languageCode": {
          "type": "string"
        },
        "name": {
          "type": "string"
        },
        "subject": {
          "type": "string"
        },
        "updatedAt": {
          "type": "string"
        },
        "variables": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/email-templates?limit=<integer>&offset=<integer>''' \
--header '''Authorization: Bearer Token'''```"
"# Method create new email-template
### Create new email-template
## HTTP request
```code
	POST https://api.voicer.software/api/v1/email-templates
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "data": {
    "languageCode": "string",
    "name": "string",
    "subject": "string",
    "variables": [
      "string1",
      "string2"
    ]
  }
}
```
## Response body (code 200)
```json
{
  
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/email-templates' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
    "languageCode": "<string>",
    "name": "<string>",
    "subject": "<string>",
    "variables": ["<string1>", "<string2>"]
}'```"
"# Method find EmailTemplate by ID
### Find email-template by id
## HTTP request
```code
	GET https://api.voicer.software/api/v1/email-templates/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Email Template ID  |
## Response body (code 200)
```json
{
  "description": "EmailTemplate domain model",
  "type": "object",
  "properties": {
    "createdAt": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "languageCode": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "subject": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    },
    "variables": {
      "type": "array",
      "items": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/email-templates/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method update email-template
### Update email-template
## HTTP request
```code
	PUT https:/api.voicer.software/api/v1/email-templates/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       email-template id  |
## Request body
```json
{
  "languageCode": "<string>",
  "name": "<string>",
  "subject": "<string>",
  "variables": ["<string>", "<string>"]
}
```
## Response body (code 200)
```json
{
  "description": "Updated",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/email-templates/{id}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "languageCode": "<string>",
  "name": "<string>",
  "subject": "<string>",
  "variables": ["<string>", "<string>"]
}'```"
"# Method Delete Email Template by ID
### Delete email-template
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/email-templates/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Email-template ID  |
## Response body (code 200)
```json
{
  "description": "Deleted",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/email-templates/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''```"
"# Method get forms for company
### Show forms for company
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/forms
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Form domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "anonymous": {
        "type": "boolean"
      },
      "companyID": {
        "type": "integer"
      },
      "createdAt": {
        "type": "string"
      },
      "fieldID": {
        "type": "integer"
      },
      "fields": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.FormField"
        }
      },
      "id": {
        "type": "integer"
      },
      "isActive": {
        "type": "boolean"
      },
      "isDefault": {
        "type": "boolean"
      },
      "languageID": {
        "type": "integer"
      },
      "logo": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "nodeID": {
        "type": "integer"
      },
      "options": {
        "type": "array",
        "items": {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      },
      "status": {
        "type": "string"
      },
      "styles": {
        "type": "array",
        "items": {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      },
      "updatedAt": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/forms''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method Store form
### Store form
## HTTP request
```code
	POST https://api.voicer.software/api/v1/forms
	Authorization: Bearer Token
	Content-Type: application/json
```

## Request body
```json
{
  "form": {
    "companyID": <integer>,
    "languageID": <integer>,
    "name": "<string>",
    "nodeID": <integer>,
    "status": "<string>",
    "anonymous": <boolean>,
    "isActive": <boolean>,
    "isDefault": <boolean>,
    "logo": "<string>",
    "fieldID": <integer>,
    "options": [
      {
        "$ref": "#/definitions/form.StoreRequestOption"
      }
    ],
    "styles": [
      {
        "$ref": "#/definitions/form.StoreRequestOption"
      }
    ]
  }
}
```

## Response body (code 200)
```json
{
  "description": "Form domain model",
  "type": "object",
  "properties": {
    "anonymous": {
      "type": "boolean"
    },
    "companyID": {
      "type": "integer"
    },
    "createdAt": {
      "type": "string"
    },
    "fieldID": {
      "type": "integer"
    },
    "fields": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.FormField"
      }
    },
    "id": {
      "type": "integer"
    },
    "isActive": {
      "type": "boolean"
    },
    "isDefault": {
      "type": "boolean"
    },
    "languageID": {
      "type": "integer"
    },
    "logo": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "nodeID": {
      "type": "integer"
    },
    "options": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "status": {
      "type": "string"
    },
    "styles": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```

## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/forms' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data '{
  "form": {
    "companyID": <integer>,
    "languageID": <integer>,
    "name": "<string>",
    "nodeID": <integer>,
    "status": "<string>",
    "anonymous": <boolean>,
    "isActive": <boolean>,
    "isDefault": <boolean>,
    "logo": "<string>",
    "fieldID": <integer>,
    "options": [
      {
        "$ref": "#/definitions/form.StoreRequestOption"
      }
    ],
    "styles": [
      {
        "$ref": "#/definitions/form.StoreRequestOption"
      }
    ]
  }
}'```"
"# Method get Form id
### Show form
## HTTP request
```code
	GET https://api.voicer.software/api/v1/forms/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Form ID  |
## Response body (code 200)
```json
{
  "description": "Form domain model",
  "type": "object",
  "properties": {
    "anonymous": {
      "type": "boolean"
    },
    "companyID": {
      "type": "integer"
    },
    "createdAt": {
      "type": "string"
    },
    "fieldID": {
      "type": "integer"
    },
    "fields": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.FormField"
      }
    },
    "id": {
      "type": "integer"
    },
    "isActive": {
      "type": "boolean"
    },
    "isDefault": {
      "type": "boolean"
    },
    "languageID": {
      "type": "integer"
    },
    "logo": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "nodeID": {
      "type": "integer"
    },
    "options": {
      "type": "array",
      "items": {
        "key": {"type":"string"},
        "value": {"type":"string"}
      }
    },
    "status": {
      "type": "string"
    },
    "styles": {
      "type": "array",
      "items": {
        "key": {"type":"string"},
        "value": {"type":"string"}
      }
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/forms/{id}''' \
--header '''Authorization: Bearer Token''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--data '''
{
  "id": <integer>
}
'''```"
"# Method Update form
### Update form
### HTTP request
```code
	PUT https://api.voicer.software/api/v1/forms/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```

## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Form ID  |

## Parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `form`| object | Yes |                       Form data  |
| `form.anonymous`| boolean | No |                       Form anonymous flag  |
| `form.companyID`| integer | Yes |                       Form company ID  |
| `form.fieldID`| integer | No |                       Form field ID  |
| `form.isActive`| boolean | No |                       Form isActive flag  |
| `form.isDefault`| boolean | No |                       Form isDefault flag  |
| `form.languageID`| integer | No |                       Form language ID  |
| `form.logo`| string | No |                       Form logo path  |
| `form.name`| string | No |                       Form name  |
| `form.nodeID`| integer | No |                       Form node ID  |
| `form.options`| array | No |                       Form options list  |
| `form.status`| string | No |                       Form status  |
| `form.styles`| array | No |                       Form styles list  |

## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```

## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/forms/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data '{
  "form": {
    "anonymous": "<boolean>",
    "companyID": "<integer>",
    "fieldID": "<integer>",
    "isActive": "<boolean>",
    "isDefault": "<boolean>",
    "languageID": "<integer>",
    "logo": "<string>",
    "name": "<string>",
    "nodeID": "<integer>",
    "options": [],
    "status": "<string>",
    "styles": []
  }
}'
```"
"# Method delete Form by id
### Delete form
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/forms/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Form ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/forms/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''```"
Error: Could not get a response from the API.
"# Method Store form_field
### Store form_field
## HTTP request
```code
	POST https://api.voicer.software/api/v1/form_fields
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters

## Query parameters

## Request body
```json
{
  "form_field": {
    "formID": "<integer>",
    "type": "<string>",
    "answers": [
      {
        "<answer properties>"
      }
    ],
    "fieldID": "<integer>",
    "options": [
      {
        "<option properties>"
      }
    ],
    "question": "<string>",
    "styles": [
      {
        "<style properties>"
      }
    ]
  }
}
```
## Response body (code 200)
```json
{
  "description": "FormField domain model",
  "type": "object",
  "properties": {
    "answers": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.AnswerOption"
      }
    },
    "createdAt": {
      "type": "string"
    },
    "fieldID": {
      "type": "integer"
    },
    "formID": {
      "type": "integer"
    },
    "id": {
      "type": "integer"
    },
    "options": {
      "type": "array",
      "items": {
        {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      }
    },
    "question": {
      "type": "string"
    },
    "styles": {
      "type": "array",
      "items": {
        {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      }
    },
    "type": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/form_fields''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''  --data '''{
      "form_field": {
        "formID": "<integer>",
        "type": "<string>",
        "answers": [
          {
            "<answer properties>"
          }
        ],
        "fieldID": "<integer>",
        "options": [
          {
            "<option properties>"
          }
        ],
        "question": "<string>",
        "styles": [
          {
            "<style properties>"
          }
        ]
      }
    }'''"
"# Method get Form Field by id
### Show form_field
## HTTP request
```code
	GET https://api.voicer.software/api/v1/form_fields/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Field ID  |
## Response body (code 200)
```json
{
  "description": "FormField domain model",
  "type": "object",
  "properties": {
    "answers": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.AnswerOption"
      }
    },
    "createdAt": {
      "type": "string"
    },
    "fieldID": {
      "type": "integer"
    },
    "formID": {
      "type": "integer"
    },
    "id": {
      "type": "integer"
    },
    "options": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "question": {
      "type": "string"
    },
    "styles": {
      "type": "array",
      "items": {
        "key": {
          "type": "string"
        },
        "value": {
          "type": "string"
        }
      }
    },
    "type": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/form_fields/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''
{
  "id": <integer>
}'''
```"
"# Method update form_field
### Update form_field
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/form_fields/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Field ID  |
## Request body
```json
{
  "answers": [<array_of_answers>],
  "fieldID": <integer>,
  "options": [<array_of_options>],
  "question": "<string>",
  "styles": [<array_of_styles>],
  "type": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/form_fields/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token``` ''' \
--data '''
{
  "answers": [<array_of_answers>],
  "fieldID": <integer>,
  "options": [<array_of_options>],
  "question": "<string>",
  "styles": [<array_of_styles>],
  "type": "<string>"
}
'''
```
Replace `Token` with the actual bearer token value and `{id}` with the actual ID value. Replace `<array_of_answers>`, `<integer>`, `<array_of_options>`, `<string>`, and `<array_of_styles>` with the actual values for the respective fields."
"# Method delete form_field by id
### Delete form_field
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/form_fields/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Form Field ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/form_fields/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''```"
"# Method get fields for form id
### Show fields for form
## HTTP request
```code
	GET https://api.voicer.software/api/v1/forms/{id}/fields
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Form ID  |
## Response body (code 200)
```json
{
  "description": "FormField domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "answers": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.AnswerOption"
        }
      },
      "createdAt": {
        "type": "string"
      },
      "fieldID": {
        "type": "integer"
      },
      "formID": {
        "type": "integer"
      },
      "id": {
        "type": "integer"
      },
      "options": {
        "type": "array",
        "items": {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      },
      "question": {
        "type": "string"
      },
      "styles": {
        "type": "array",
        "items": {
          "key": {
            "type": "string"
          },
          "value": {
            "type": "string"
          }
        }
      },
      "type": {
        "type": "string"
      },
      "updatedAt": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code 
curl --location --request GET 'https://api.voicer.software/api/v1/forms/{id}/fields' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'
```
Замените `{id}` на реальный идентификатор формы."
Error: Could not get a response from the API.
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method update group
### Update group
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/groups/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Group ID  |
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `data`| object | Yes |                      Request body  |
## Request body
```json
{
  "name": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/groups/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "name": "<string>"
}'```"
"# Method delete group
### Delete group
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/groups/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       group id  |
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/groups/{id}''' \
--header '''Authorization: Bearer Token''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--data '''{}'''
```
Remember to replace `{id}` with the actual group identifier."
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method add node subtree view to group
### Add node subtree view to group
## HTTP request
```code
	POST https://api.voicer.software/api/v1/groups/{id}/nodes/{node_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Group ID  |
| `node_id`| integer | Yes |                       Node ID  |
## Response body (code 200)
```json
{
  "description": "View provided",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/groups/{id}/nodes/{node_id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{}'''
```
"
"# Method delete node from group
### Remove node subtree view from group
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/groups/{id}/nodes/{node_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Group ID |
| `node_id`| integer | Yes |                       Node ID  |
## Response body (code 200)
```json
{
  "description": "View removed",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/groups/{id}/nodes/{node_id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```"
Error: Could not get a response from the API.
"# Method Remove user from group
### Remove user from group
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/groups/{id}/users/{user_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Group ID  |
| `user_id`| integer | Yes |                       User ID  |
## Response body (code 200)
```json
{
  "description": "User removed",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/groups/{id}/users/{user_id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''```"
"# Method healthChecks
### healthChecks
## HTTP request
```code
	GET https://api.voicer.software/api/v1/health_checks
	Authorization: Bearer Token
	Content-Type: application/json
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/health_checks' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```"
"# Method get languages
### List languages
## HTTP request
```code
	GET https://api.voicer.software/api/v1/languages
	Authorization: Bearer Token
```
## Response body (code 200)
```json
{
  "description": "list",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "icon": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/languages' \
--header 'Authorization: Bearer Token'```"
Error: Could not get a response from the API.
"# Method delete language
### Delete language
## HTTP request
```code
    DELETE https://api.voicer.software/api/v1/languages
    Authorization: Bearer Token
    Content-Type: application/json
```
## Request body
```json
{
    "name": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/languages' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data '{
    "name": "<string>"
}'```"
"# Method Create Metadata
### Create metadata
## HTTP request
```code
	POST https://api.voicer.software/api/v1/metadata/{entity}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `entity`| string | Yes |                       Type of entity ("companies" or "nodes") |
## Request body
```json
{
  "metadata": {
    "key": "<string>",
    "parentID": <integer>,
    "value": "<string>"
  },
  "entity": "<string>"
}
```
## Response body (code 200)
```json
{
  "description": "Metadata domain model",
  "type": "object",
  "properties": {
    "createdAt": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "key": {
      "type": "string"
    },
    "parentID": {
      "type": "integer"
    },
    "updatedAt": {
      "type": "string"
    },
    "value": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/metadata/{entity}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data '{
  "metadata": {
    "key": "<string>",
    "parentID": <integer>,
    "value": "<string>"
  },
  "entity": "<string>"
}'```
Replace `<string>` with the actual values and `<integer>` with the actual integer value."
"# Method get entity metadata by ID
### Show metadata
## HTTP request
```code
	GET https://api.voicer.software/api/v1/metadata/{entity}/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `entity`| string | Yes |                       Entity Type  |
| `id`| integer | Yes |                       Metadata ID  |
## Response body (code 200)
```json
{
  "description": "Metadata domain model",
  "type": "object",
  "properties": {
    "createdAt": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "key": {
      "type": "string"
    },
    "parentID": {
      "type": "integer"
    },
    "updatedAt": {
      "type": "string"
    },
    "value": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/metadata/{entity}/{id}''' \
--header '''Authorization: Bearer Token''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
```"
"# Method Update metadata
### Update metadata
## HTTP request
```code 
	PUT https://api.voicer.software/api/v1/metadata/{entity}/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `entity`| string ['companies','nodes'] | Yes |                       Entity type  |
| `id`| integer | Yes |                       Entity ID  |
## Request body
```json
{
  "metadata": {
    "value": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/metadata/{entity}/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
    "metadata": {
        "value": "<string>"
    }
}'
```"
"# Method delete metadata by entity and id
### Delete metadata
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/metadata/{entity}/{id}
	Authorization: Bearer Token
	Content-Type: application/json
	entity: <string>
	id: <integer>
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `entity`| string | Yes |                Metadata entity (companies or nodes)  |
| `id`| integer | Yes |                       Metadata ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/metadata/{entity}/{id}''' \
--header '''Authorization: Bearer Token`''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''entity: <string>''' \
--header '''id: <integer>''' \
'''{
}'''"
"# Method get entity metadata by ID
### Show entity metadata by ID
## HTTP request
```code
	GET https://api.voicer.software/api/v1/{entity}/{id}/metadata
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `entity`| string | Yes |                       Entity type (companies or nodes)  |
| `id`| integer | Yes |                       Entity ID  |
## Response body (code 200)
```json
{
  "description": "Metadata domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "createdAt": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "key": {
        "type": "string"
      },
      "parentID": {
        "type": "integer"
      },
      "updatedAt": {
        "type": "string"
      },
      "value": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/{entity}/{id}/metadata''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method get nodes by company ID
### Show nodes by company ID
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/nodes
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Node domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "children": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.Node"
        }
      },
      "code": {
        "type": "string"
      },
      "companyID": {
        "type": "integer"
      },
      "createdAt": {
        "type": "string"
      },
      "enableOverdue": {
        "type": "boolean"
      },
      "id": {
        "type": "integer"
      },
      "metadata": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.Metadata"
        }
      },
      "name": {
        "type": "string"
      },
      "parentID": {
        "type": "integer"
      },
      "referencedID": {
        "type": "integer"
      },
      "responsibleID": {
        "type": "integer"
      },
      "slug": {
        "type": "string"
      },
      "sourceID": {
        "type": "integer"
      },
      "updatedAt": {
        "type": "string"
      },
      "useDetectLanguage": {
        "type": "boolean"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/nodes''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '{}'''
```"
"# Method create node
### Create node
## HTTP request
```code
	POST https://api.voicer.software/api/v1/nodes
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "node": {
    "code": "string",
    "companyID": 0,
    "enableOverdue": true,
    "name": "string",
    "parentID": 0,
    "referencedID": 0,
    "responsibleID": 0,
    "sourceID": 0,
    "useDetectLanguage": true
  }
}
```
## Response body (code 200)
```json
{}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/nodes' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token`' \
--data-raw '{
  "node": {
    "code": "string",
    "companyID": 0,
    "enableOverdue": true,
    "name": "string",
    "parentID": 0,
    "referencedID": 0,
    "responsibleID": 0,
    "sourceID": 0,
    "useDetectLanguage": true
  }
}'```"
"# Method get Node by id
### Show node
## HTTP request
```code
	GET https://api.voicer.software/api/v1/nodes/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Node ID  |
## Response body (code 200)
```json
{
  "description": "Node domain model",
  "type": "object",
  "properties": {
    "children": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Node"
      }
    },
    "code": {
      "type": "string"
    },
    "companyID": {
      "type": "integer"
    },
    "createdAt": {
      "type": "string"
    },
    "enableOverdue": {
      "type": "boolean"
    },
    "id": {
      "type": "integer"
    },
    "metadata": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Metadata"
      }
    },
    "name": {
      "type": "string"
    },
    "parentID": {
      "type": "integer"
    },
    "referencedID": {
      "type": "integer"
    },
    "responsibleID": {
      "type": "integer"
    },
    "slug": {
      "type": "string"
    },
    "sourceID": {
      "type": "integer"
    },
    "updatedAt": {
      "type": "string"
    },
    "useDetectLanguage": {
      "type": "boolean"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/nodes/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Authorization: Bearer Token''' \
--header '''Accept: application/json'''
```"
"# Method update Node
### Update node
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/nodes/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Node ID  |
## Request body
```json
{
  "enableOverdue": "<boolean>",
  "name": "<string>",
  "parentID": "<integer>",
  "referencedID": "<integer>",
  "responsibleID": "<integer>",
  "sourceID": "<integer>",
  "useDetectLanguage": "<boolean>"
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/nodes/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token` --data '''{
  '''enableOverdue''': '''<boolean>''',
  '''name''': '''<string>''',
  '''parentID''': '''<integer>''',
  '''referencedID''': '''<integer>''',
  '''responsibleID''': '''<integer>''',
  '''sourceID''': '''<integer>''',
  '''useDetectLanguage''': '''<boolean>'''
}'''```"
"# Method delete Node id
### Delete node
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/nodes/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Node ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/nodes/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  '''id''': '''<integer>'''
}'''"
"# Method GET: Show node with metadata
Description: Show node with metadata
## HTTP request
```code 
GET https//api.voicer.software/api/v1/nodes/{id}/full
Authorization: Bearer Token`
```
```http
Content-Type: application/json
Accept: application/json
```
## Path parameters
| Parameter | Type    | Required | Description  |
| :-------- | :------:| :-------:| :----------- |
| `id`      | integer |   true   | Node ID      |
## Response body (code 200)
```json
{
  "description": "Node domain model",
  "Type": "object",
  "Properties": {
    "children": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Node"
      }
    },
    "code": {
      "type": "string"
    },
    "companyID": {
      "type": "integer"
    },
    "createdAt": {
      "type": "string"
    },
    "enableOverdue": {
      "type": "boolean"
    },
    "id": {
      "type": "integer"
    },
    "metadata": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Metadata"
      }
    },
    "name": {
      "type": "string"
    },
    "parentID": {
      "type": "integer"
    },
    "referencedID": {
      "type": "integer"
    },
    "responsibleID": {
      "type": "integer"
    },
    "slug": {
      "type": "string"
    },
    "sourceID": {
      "type": "integer"
    },
    "updatedAt": {
      "type": "string"
    },
    "useDetectLanguage": {
      "type": "boolean"
    }
  }
}
```
## CURL Requests
```curl
curl --location --request GET 'https//api.voicer.software/api/v1/nodes/{id}/full' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token`'
```"
"# Method Update Node Responsible
### Update node responsible.
There are two levels of responsible distribution: one (default) and all.
type=one - responsible user is set only on the given node.
type=all - responsible user is set on a full subtree started with the given node.
If you pass null to responsibleID in body it will remove responsible from node.

## HTTP request
```code
	PUT https://api.voicer.software/api/v1/nodes/{id}/responsible
	Authorization: Bearer Token
	Content-Type: application/json
```

## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Node ID  |

## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `type`| enum (all, one) | No |                    Distribution type |

## Request body
```json
{
  "responsibleID": <integer>,
  "type": "<string>"
}
```

## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "nodesUpdated": {
      "type": "integer"
    }
  }
}
```

## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/nodes/{id}/responsible''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{\n  '''responsibleID''': <integer>,\n  '''type''': '''<string>'''\n}'''
```"
"# Method Query Reviews
### Query reviews
## HTTP request
```code
	GET https://api.voicer.software/api/v1/reviews
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `limit` | integer | No |       Limit record count |
| `offset` | integer | No |   Offset count |
| `form_id` | integer | No |     List by form id |
| `node_id` | integer | No |     List by node id |
| `company_id` | integer | No |  List by company id |
| `from` | string (date-time) | No | List created after date |
| `to` | string (date-time) | No |    List created before date |
## Response body (code 200)
```json
{
  "description": "Review model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "answers": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.ClientAnswer"
        }
      },
      "comment": {
        "type": "string"
      },
      "created_at": {
        "type": "string"
      },
      "formID": {
        "type": "integer"
      },
      "id": {
        "type": "integer"
      },
      "sessionID": {
        "type": "string"
      },
      "status": {
        "$ref": "#/definitions/domain.ClientStatus"
      },
      "ticket_number": {
        "type": "integer"
      },
      "timestamps": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.Timestamp"
        }
      },
      "updated_at": {
        "type": "string"
      },
      "was_overdue": {
        "type": "boolean"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/reviews''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "limit": <integer>,
  "offset": <integer>,
  "form_id": <integer>,
  "node_id": <integer>,
  "company_id": <integer>,
  "from": <string>,
  "to": <string>
}'''
```"
"# Method POST reviews
### Get reviews list by filter
## HTTP request
```code 
POST https://api.voicer.software/api/v1/reviews
Authorization: Bearer Token
Content-Type: application/json
```
## Request body
```json
{
  "name": "review data",
  "in": "body",
  "required": true,
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "contacts": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.ContactType"
      }
    },
    "forms": {
      "type": "array",
      "items": {
        "type": "integer"
      }
    },
    "from": {
      "type": "string"
    },
    "nodes": {
      "type": "array",
      "items": {
        "type": "integer"
      }
    },
    "sources": {
      "type": "array",
      "items": {
        "type": "integer"
      }
    },
    "statuses": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.ClientStatus"
      }
    },
    "to": {
      "type": "string"
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "Review model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "answers": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.ClientAnswer"
        }
      },
      "comment": {
        "type": "string"
      },
      "contact": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.ClientContact"
        }
      },
      "created_at": {
        "type": "string"
      },
      "form": {
        "$ref": "#/definitions/domain.Form"
      },
      "formFields": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.FormField"
        }
      },
      "formID": {
        "type": "integer"
      },
      "id": {
        "type": "integer"
      },
      "node": {
        "description": "Joined",
        "allOf": [
          {
            "$ref": "#/definitions/domain.Node"
          }
        ]
      },
      "sessionID": {
        "type": "string"
      },
      "source": {
        "$ref": "#/definitions/domain.Source"
      },
      "status": {
        "$ref": "#/definitions/domain.ClientStatus"
      },
      "ticket_number": {
        "type": "integer"
      },
      "timestamps": {
        "type": "array",
        "items": {
          "$ref": "#/definitions/domain.Timestamp"
        }
      },
      "updated_at": {
        "type": "string"
      },
      "wasOverdue": {
        "type": "boolean"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/reviews' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
    "companyID": <integer>,
    "contacts": [<ContactType>],
    "forms": [<integer>],
    "from": "<string>",
    "nodes": [<integer>],
    "sources": [<integer>],
    "statuses": [<ClientStatus>],
    "to": "<string>"
}'```"
Error: Could not get a response from the API.
"# Method get Review by id
### Show review
## HTTP request
```code
	GET https://api.voicer.software/api/v1/reviews/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| string | Yes |                       Review ID  |
## Response body (code 200)
```json
{
  "description": "Review model",
  "type": "object",
  "properties": {
    "answers": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.ClientAnswer"
      }
    },
    "comment": {
      "type": "string"
    },
    "created_at": {
      "type": "string"
    },
    "formID": {
      "type": "integer"
    },
    "id": {
      "type": "integer"
    },
    "sessionID": {
      "type": "string"
    },
    "status": {
      "$ref": "#/definitions/domain.ClientStatus"
    },
    "ticket_number": {
      "type": "integer"
    },
    "timestamps": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.Timestamp"
      }
    },
    "updated_at": {
      "type": "string"
    },
    "was_overdue": {
      "type": "boolean"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/reviews/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''"
Error: Could not get a response from the API.
"# Method send SMS without timezone
### Send SMS without timezone
## HTTP request
```code
	POST https://api.voicer.software/api/v1/sms
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "message": {
    "data": "<string>",
    "phone": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Request
```code
curl --location --request POST 'https://api.voicer.software/api/v1/sms' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "data": "<string>",
  "phone": "<string>"
}'"
"# Method send bulk SMS
### Send SMS without timezone to many
## HTTP request
```code
	POST https://api.voicer.software/api/v1/sms/bulk
	Authorization: Bearer Token
	Content-Type: application/json
	Accept: application/json
```
## Request body
```json
{
  "message": {
    "data": "<string>",
    "phones": ["<phone_number1>", "<phone_number2>"]
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/sms/bulk''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "message": {
    "data": "<string>",
    "phones": ["<phone_number1>", "<phone_number2>"]
  }
}'''```"
"# Method get sources by company id
### Get sources by company id
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{company_id}/sources
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `company_id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "Source domain model",
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/companies/{company_id}/sources' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json'```
Please note that you need to replace `{company_id}` with the actual company ID that you want to retrieve sources for."
"# Method create Source
### Create source
## HTTP request
```code
	POST https://api.voicer.software/api/v1/sources
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "source": {
    "companyID": <integer>,
    "name": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "Source domain model",
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/sources''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "source": {
    "companyID": <integer>,
    "name": "<string>"
  }
}'''"
"# Method get Source by id
### Find source
## HTTP request
```code
	GET https://api.voicer.software/api/v1/sources/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Source ID  |
## Response body (code 200)
```json
{
  "description": "Source domain model",
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/sources/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method Update Source
### Update source
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/sources/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Source ID  |
## Request body
```json
{
  "source": {
    "companyID": {
      "type": "integer",
      "required" : true
    },
    "name": {
      "type": "string",
      "maxLength": 255
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "Source domain model",
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT '''https://api.voicer.software/api/v1/sources/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  '''companyID''': <integer>,
  '''name''': '''<string>'''
}'''"
"# Method Delete Source
### Delete source
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/sources/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Source ID  |
## Response body (code 200)
```json
{
  "description": "Source domain model",
  "type": "object",
  "properties": {
    "companyID": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/sources/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```"
"# Method get all ticket statuses for company id
### List all companies
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/ticket_statuses
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "TicketStatus domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "company_id": {
        "type": "integer"
      },
      "created_at": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      },
      "updated_at": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/ticket_statuses''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "id": <integer>
}'''```"
"# Method create ticket
### Create ticket
## HTTP request
```code
	POST https://api.voicer.software/api/v1/companies/{id}/ticket_statuses
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Request body
```json
{
 "ticket": {
   "comment": "",
   "name": "",
   "node_id": 0,
   "priority": {
     "value": ""
   },
   "responsible_id": 0,
   "review_id": 0,
   "status_id": 0,
   "type_id": 0
 }
 }
```
## Response body (code 200)
```json
{
  "description": "TicketStatus domain model",
  "type": "object",
  "properties": {
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/companies/{id}/ticket_statuses' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "ticket": {
    "comment": "",
    "name": "",
    "node_id": 0,
    "priority": {
      "value": ""
    },
    "responsible_id": 0,
    "review_id": 0,
    "status_id": 0,
    "type_id": 0
  }
}'```"
"# Method get companies ticket types
### List all companies
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/ticket_types
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Response body (code 200)
```json
{
  "description": "TicketType domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "company_id": {
        "type": "integer"
      },
      "created_at": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "img": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "updated_at": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/ticket_types''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--header '''id: <integer>'''
```"
Error: Could not get a response from the API.
"# Method get company tickets
### List all companies
## HTTP request
```code
	GET https://api.voicer.software/api/v1/companies/{id}/tickets
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       company id  |
## Response body (code 200)
```json
{
  "description": "Ticket domain model",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "comment": {
        "type": "string"
      },
      "company_id": {
        "type": "integer"
      },
      "created_at": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "name": {
        "type": "string"
      },
      "node_id": {
        "type": "integer"
      },
      "priority": {
        "$ref": "#/definitions/domain.PriorityType"
      },
      "responsible_id": {
        "type": "integer"
      },
      "review_id": {
        "type": "integer"
      },
      "status_id": {
        "type": "integer"
      },
      "type_id": {
        "type": "integer"
      },
      "updated_at": {
        "type": "string"
      },
      "user_id": {
        "type": "integer"
      }
    }
  }
}
```
## CURL Requests
```code 
curl --location --request GET '''https://api.voicer.software/api/v1/companies/{id}/tickets''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method create ticket
### Create ticket
## HTTP request
```code
	POST https://api.voicer.software/api/v1/companies/{id}/tickets
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Company ID  |
## Request body
```json
{
  "ticket": {
    "comment": "<string>",
    "name": "<string>",
    "node_id": <integer>,
    "priority": "<string>",
    "responsible_id": <integer>,
    "review_id": <integer>,
    "status_id": <integer>,
    "type_id": <integer>
  },
  "id": <integer>
}
```
## Response body (code 200)
```json
{
  "description": "Ticket domain model",
  "type": "object",
  "properties": {
    "comment": {
      "type": "string"
    },
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "node_id": {
      "type": "integer"
    },
    "priority": {
      "$ref": "#/definitions/domain.PriorityType"
    },
    "responsible_id": {
      "type": "integer"
    },
    "review_id": {
      "type": "integer"
    },
    "status_id": {
      "type": "integer"
    },
    "type_id": {
      "type": "integer"
    },
    "updated_at": {
      "type": "string"
    },
    "user_id": {
      "type": "integer"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/companies/{id}/tickets' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "ticket": {
    "comment": "<string>",
    "name": "<string>",
    "node_id": <integer>,
    "priority": "<string>",
    "responsible_id": <integer>,
    "review_id": <integer>,
    "status_id": <integer>,
    "type_id": <integer>
  },
  "id": <integer>
}'```"
Error: Could not get a response from the API.
"# Method get ticket status by id
### Show ticket
## HTTP request
```code
	GET https://api.voicer.software/api/v1/ticket_statuses/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket status ID  |
## Response body (code 200)
```json
{
  "description": "TicketStatus domain model",
  "type": "object",
  "properties": {
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/ticket_statuses/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'
```
Replace `{id}` with the actual value of the ticket status ID you want to retrieve."
"# Method Update ticket
### Update ticket
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/ticket_statuses/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Status ID  |
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `ticket`| object | Yes |                      Ticket Info  |
## Request body
```json
{
  "comment": "<string>",
  "name": "<string>",
  "node_id": <integer>,
  "priority": "<string>",
  "responsible_id": <integer>,
  "review_id": <integer>,
  "status_id": <integer>,
  "type_id": <integer>
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/ticket_statuses/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "comment": "<string>",
  "name": "<string>",
  "node_id": <integer>,
  "priority": "<string>",
  "responsible_id": <integer>,
  "review_id": <integer>,
  "status_id": <integer>,
  "type_id": <integer>
}'```"
"# Method delete ticket status id
### Delete ticket
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/ticket_statuses/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket status ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/ticket_statuses/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```"
"# Method get ticket type by id
### Show ticket
## HTTP request
```code
	GET https://api.voicer.software/api/v1/ticket_types/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket Type ID  |
## Response body (code 200)
```json
{
  "description": "TicketType domain model",
  "type": "object",
  "properties": {
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "img": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "updated_at": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/ticket_types/{id}' \
--header 'Authorization: Bearer Token' \
--header 'Accept: application/json'
```"
"# Method update ticket type
### Update ticket
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/ticket_types/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket type ID  |
## Request body
```json
{
  "comment": "<string>",
  "name": "<string>",
  "node_id": <integer>,
  "priority": <domain.PriorityType>,
  "responsible_id": <integer>,
  "review_id": <integer>,
  "status_id": <integer>,
  "type_id": <integer>
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/ticket_types/{id}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
   "comment": "<string>",
   "name": "<string>",
   "node_id": <integer>,
   "priority": <domain.PriorityType>,
   "responsible_id": <integer>,
   "review_id": <integer>,
   "status_id": <integer>,
   "type_id": <integer>
}'
```
Replace `{id}`, `<string>`, and `<integer>` with the actual values for your request."
"# Method Delete ticket
### Delete ticket
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/ticket_types/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket ID  |
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code 
curl --location --request DELETE 'https://api.voicer.software/api/v1/ticket_types/{id}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw ''
```
Please note that you need to replace `{id}` with the actual value of the ticket type ID you want to delete."
"# Method get Ticket ID
### Show ticket
## HTTP request
```code
	GET https://api.voicer.software/api/v1/tickets/{id}
	Authorization: Bearer Token
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket ID  |
## Response body (code 200)
```json
{
  "description": "Ticket domain model",
  "type": "object",
  "properties": {
    "comment": {
      "type": "string"
    },
    "company_id": {
      "type": "integer"
    },
    "created_at": {
      "type": "string"
    },
    "id": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "node_id": {
      "type": "integer"
    },
    "priority": {
      "$ref": "#/definitions/domain.PriorityType"
    },
    "responsible_id": {
      "type": "integer"
    },
    "review_id": {
      "type": "integer"
    },
    "status_id": {
      "type": "integer"
    },
    "type_id": {
      "type": "integer"
    },
    "updated_at": {
      "type": "string"
    },
    "user_id": {
      "type": "integer"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/tickets/{id}' \
--header 'Authorization: Bearer Token`'```"
"# Method Update Ticket
### Update ticket
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/tickets/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       Ticket ID  |
## Request body
```json
{
  "comment": "<string>",
  "name": "<string>",
  "node_id": <integer>,
  "priority": "<domain.PriorityType>",
  "responsible_id": <integer>,
  "review_id": <integer>,
  "status_id": <integer>,
  "type_id": <integer>
}
```
## Response body (code 200)
```json
{
  "description": "ok",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/tickets/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "comment": "<string>",
  "name": "<string>",
  "node_id": <integer>,
  "priority": "<domain.PriorityType>",
  "responsible_id": <integer>,
  "review_id": <integer>,
  "status_id": <integer>,
  "type_id": <integer>
}'```"
Error: Could not get a response from the API.
"## Method List user contacts
### List user contacts.
Query params can be used to find a specific subset of contacts.
## HTTP request
```code
	GET https://api.voicer.software/api/v1/user_contacts?email=<user_email>&chatID=<chat_id>&userID=<user_id>
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `email`| string | No |                       User Email  |
| `chatID`| integer | No |                       Chat ID  |
| `userID`| integer | No |                       User ID  |
## Response body (code 200)
```json
{
  "description": "user contacts list",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "active": {
        "type": "boolean"
      },
      "createdAt": {
        "type": "string"
      },
      "email": {
        "type": "string"
      },
      "id": {
        "type": "integer"
      },
      "telegramID": {
        "type": "string"
      },
      "updatedAt": {
        "type": "string"
      },
      "userID": {
        "type": "integer"
      },
      "viberID": {
        "type": "string"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/user_contacts?email=<user_email>&chatID=<chat_id>&userID=<user_id>' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer <token>'
```
Replace `<user_email>` with the email of the user you want to search for contacts, `<chat_id>` with the desired chat ID, `<user_id>` with the user ID you want to search for contacts, and `<token>` with the actual token value."
"# Method store user contact
### Store user contact
## HTTP request
```code
	POST https://api.voicer.software/api/v1/user_contacts
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "contact": {
        "chatID": "<string>",
        "payload": "<string>",
        "type": "<string>",
        "userID": <integer> 
  }
}
```
## Response body (code 200)
```json
{
  
}
```
## CURL Requests
```code
curl--location --request POST 'https://api.voicer.software/api/v1/user_contacts' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
    "contact": {
        "chatID": "<string>",
        "payload": "<string>",
        "type": "<string>",
        "userID": <integer>
    }
}'```"
"# Method update user contact
### Update user contact
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/user_contacts/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       User contact ID  |
## Request body
```json
{
  "active": {
    "type": "boolean"
  },
  "email": {
    "type": "string"
  }
}
```
## Response body (code 200)
```json
{
  "description": "Success",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT [url: https://api.voicer.software/api/v1/user_contacts/{id}] \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token` \
--data-raw '{
  "active": true,
  "email": "<string>"
}'```"
"# Method delete user contact by id
### Delete user contact
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/user_contacts/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       User contact ID  |
## Response body (code 200)
```json
{
  "description": "Success",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE '''https://api.voicer.software/api/v1/user_contacts/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "id": <integer>
}'''"
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method store user notification
### Store user notification
## HTTP request
```code
	POST https://api.voicer.software/api/v1/user_notifications/list
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "deliveryAt": "<string>",
  "message": "<string>",
  "userID": <integer>
}
```
## Response body (code 200)
```json
{}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/user_notifications/list''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "deliveryAt": "<string>",
  "message": "<string>",
  "userID": <integer>
}'''
```"
Error: Could not get a response from the API.
Error: Could not get a response from the API.
"# Method List Users
### List users filtered by provided query
## HTTP request
```code
	GET https://api.voicer.software/api/v1/users?name=<name>&email=<email>&q=<search_text>&companyID=<company_id>&groupID=<group_id>&limit=<limit>&offset=<offset>
	Authorization: Bearer Token
	Content-Type: application/json
```
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `name`| string | No |                       user name  |
| `email`| string | No |                       user email  |
| `q`| string | No |                      search text  |
| `companyID`| integer | No |                      company id  |
| `groupID`| integer | No |                      group id  |
| `limit`| integer | No |                      limit  |
| `offset`| integer | No |                      offset  |
## Response body (code 200)
```json
{
  "description": "Users list",
  "type": "object",
  "properties": {
    "count": {
      "type": "integer"
    },
    "data": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/domain.User"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET 'https://api.voicer.software/api/v1/users?name=<name>&email=<email>&q=<search_text>&companyID=<company_id>&groupID=<group_id>&limit=<limit>&offset=<offset>' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json'```"
Error: Could not get a response from the API.
"# Method Update User
### Update user
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/users/{user_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
## Request body
```json
{
  "email": "string",
  "name": "string",
  "password": "string",
  "passwordConfirmation": "string"
}
```
## Response body (code 200)
```json
{
  "description": "User updated",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl -X PUT \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -H "Authorization: Bearer Token" \
     -d '{
       "email": "<string>",
       "name": "<string>",
       "password": "<string>",
       "passwordConfirmation": "<string>"
     }' \
     "https://api.voicer.software/api/v1/users/{id}"
```"
"# Method DELETE user id
### Delete user
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/users/{user_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
## Response body (code 200)
```json
{
  "description": "User deleted",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/users/{id}' \
--header 'Authorization: Bearer Token' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json'
```
Please replace `{id}` with the actual user ID."
Error: Could not get a response from the API.
"# Method Attach notifiable source to a user
### Attach notifiable source to a user
## HTTP request
```code
	POST https://api.voicer.software/api/v1/users/{user_id}/notifiable-sources/{source_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
| `source_id`| integer | Yes |                       Source ID  |
## Request body
```json
{
  "notifyTimeBegin": "<HH:MM:SS>",
  "notifyTimeEnd": "<HH:MM:SS>"
}
```
## Response body (code 200)
```json
{

}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/users/{user_id}/notifiable-sources/{source_id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "notifyTimeBegin": "<HH:MM:SS>",
  "notifyTimeEnd": "<HH:MM:SS>"
}''' 
```"
"# Method delete Detach Notifiable Source from User
### Detach notifiable source from a user
## HTTP request
```code
	DELETE https://api.voicer.software/api/v1/users/{user_id}/notifiable-sources/{source_id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
| `source_id`| integer | Yes |                       Source ID  |
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request DELETE 'https://api.voicer.software/api/v1/users/{user_id}/notifiable-sources/{source_id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token'```"
"# Method get user settings
### Show user settings for a specific user
## HTTP request
```code
	GET https://api.voicer.software/api/v1/users/{user_id}/settings
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
## Response body (code 200)
```json
{
  "description": "User settings",
  "type": "object",
  "properties": {
    "location": {
      "type": "string"
    },
    "notifyTimeBegin": {
      "type": "string"
    },
    "notifyTimeEnd": {
      "type": "string"
    },
    "updatedAt": {
      "type": "string"
    },
    "userID": {
      "type": "integer"
    },
    "workTimeBegin": {
      "type": "string"
    },
    "workTimeEnd": {
      "type": "string"
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/users/{user_id}/settings''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''
```"
"# Method update user settings
### Update user settings
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/users/{user_id}/settings
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `user_id`| integer | Yes |                       User ID  |
## Request body
```json
{
  "description": "update data",
  "name": "data",
  "in": "body",
  "required": true,
  "type": "object",
  "properties": {
    "location": {
      "type": "string"
    },
    "notifyTimeBegin": {
      "type": "string"
    },
    "notifyTimeEnd": {
      "type": "string"
    },
    "workTimeBegin": {
      "type": "string"
    },
    "workTimeEnd": {
      "type": "string"
    }
  }
}
```
## Response body (code 200)
```json
{
  "description": "User settings updated",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request PUT 'https://api.voicer.software/api/v1/users/{id}/settings' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
    "location": "<string>",
    "notifyTimeBegin": "<string>",
    "notifyTimeEnd": "<string>",
    "workTimeBegin": "<string>",
    "workTimeEnd": "<string>"
}'```"
"# Method Send Viber without timezone
### Send Viber message without specifying a timezone
## HTTP request
```code
	POST https://api.voicer.software/api/v1/viber
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "message": {
    "data": "<string>",
    "phone": "<string>"
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/viber' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token` \
--data-raw '{
  "data": "<string>",
  "phone": "<string>"
}'```"
"# Method Send Viber to many
### Send Viber to many
## HTTP request
```code
	POST https://api.voicer.software/api/v1/viber/bulk
	Authorization: Bearer Token
	Content-Type: application/json
```
## Request body
```json
{
  "message": {
    "data": "<string>",
    "phones": ["<string>", "<string>", ...]
  }
}
```
## Response body (code 200)
```json
{
  "description": "OK",
  "type": "object",
  "properties": {
    "message": {
      "type": "string",
      "example": "OK"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST '''https://api.voicer.software/api/v1/viber/bulk''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token` \
--data '''{
  "message": {
    "data": "<string>",
    "phones": ["<string>", "<string>", ...]
  }
}'''"
"# Method GET user view
### Get all companies and nodes attached to provided user
## HTTP request
```code
	GET https://api.voicer.software/api/v1/view/user/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       User ID  |
## Response body (code 200)
```json
{
  "description": "result",
  "type": "object",
  "properties": {
    "danglingNodes": {
      "type": "array",
      "items": {
        "type": "integer"
      }
    },
    "structures": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/dtos.ViewStructure"
      }
    }
  }
}
```
## CURL Requests
```code
curl --location --request GET '''https://api.voicer.software/api/v1/view/user/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token'''"
"# Method PUT to detach and attach companies and nodes to provided user
### Detach and attach companies and nodes to provided user
##### Important! It works in detach-first attach-second order
## HTTP request
```code
	PUT https://api.voicer.software/api/v1/view/user/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       User ID  |
## Request body
```json
{
  "attachCompanyIDs": [1, 2, 3],
  "attachNodeIDs": [4, 5, 6],
  "detachCompanyIDs": [7, 8, 9],
  "detachNodeIDs": [10, 11, 12],
  "updateType": "domain.ViewUpdateType"
}
```
## Response body (code 200)
```json
{
  "description": "result",
  "type": "object",
  "properties": {
    "companiesAttached": {
      "type": "integer"
    },
    "companiesDetached": {
      "type": "integer"
    },
    "nodesAttached": {
      "type": "integer"
    },
    "nodesDetached": {
      "type": "integer"
    }
  }
}
```
## CURL Requests
```curl
curl --location --request PUT '''https://api.voicer.software/api/v1/view/user/{id}''' \
--header '''Content-Type: application/json''' \
--header '''Accept: application/json''' \
--header '''Authorization: Bearer Token''' \
--data '''{
  "attachCompanyIDs": [1, 2, 3],
  "attachNodeIDs": [4, 5, 6],
  "detachCompanyIDs": [7, 8, 9],
  "detachNodeIDs": [10, 11, 12],
  "updateType": "domain.ViewUpdateType"
}'''
```"
"# Method Attach companies and nodes to user id
### Attach companies and nodes to provided user
## HTTP request
```code
	POST https://api.voicer.software/api/v1/view/user/{id}
	Authorization: Bearer Token
	Content-Type: application/json
```
## Path parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `id`| integer | Yes |                       User ID  |
## Query parameters
| Parameter | Type     | Required  |  Description                |
| :------- | :------: |  :------: |:--------------------------------- |
| `companyID`| integer | Yes |                      Company ID  |
## Request body
```json
{
  "view": {
    "companyID": <integer>,
    "nodeIDs": [<array of integers>]
  }
}
```
## Response body (code 200)
```json
{
  "description": "result",
  "type": "object",
  "properties": {
    "companiesAttached": {
      "type": "integer"
    },
    "nodesAttached": {
      "type": "integer"
    }
  }
}
```
## CURL Requests
```code
curl --location --request POST 'https://api.voicer.software/api/v1/view/user/{id}' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer Token' \
--data-raw '{
  "view": {
    "companyID": <integer>,
    "nodeIDs": [<array of integers>]
  }
}'```
