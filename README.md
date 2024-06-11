# Onehub Python Sending SMS Library
```Python
import requests
import json

x_username         = "";
x_apikey           = "";

params = {
    "phoneNumbers": "+25472*******,+25473*******,+25474*******",
    "message":      "Hello api!",
    "senderId":     "Your-Sender-ID-Here",
}

sendMessageURL = "https://api.onehub.co.ke/v1/sms/send"

headers = { 'Content-type': 'application/json', 'Accept': 'application/json', 'x-api-user': x_username, 'x-api-key' : x_apikey }

req = requests.post(sendMessageURL, data=json.dumps(params), headers=headers)

print(req.text)
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
# Response Body Parameters
## Response in case of successful sending of a message:
```json
{
    "0":{
        "country":"kenya",
        "cost":"KES 2.00",
        "success":[
            "+2547XXXYXXXX",
            "+2547XXXXXXXX"
        ]
    },
    "status":200,
    "message":"Message sent"
}
```
## Response in case a message fails:
```json
{
   "0":{
      "country":"kenya",
      "cost":"KES 1.00",
      "success":[
         "+2547XXXYXXXX"
      ],
      "failed":[
         "+2547XXXXXXXX"
      ]
   },
   "status":200,
   "message":"Message sent"
}
```
## Response in case of wrong credentials:
```json
{
    "status":401,
    "message":"Unauthorized"
}
```
# Onehub Python Add Contacts Library
```Python
import requests
import json

# authentication
x_username      = "";
x_apikey        = "";

# data
name            = "John Migo" # contact name
phone           = "+254711xxxxxx" # international format
tags            = "developer,nairobi" # optional comma separated tags
groups          = "Nairobi Coding, Group 2" # optional groups to add contact

# endoint
addContactURL   = "https://api.braceafrica.com/v1/contacts/add"

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

params = {
    'name' : name,
    'phone' : phone,
    'tags' : tags,
    'groups': groups
}

req = requests.post(MessageHost, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful adding of a contact:
```json
{
    "status": 200,
    "message": "Contact added"
}
```
# Onehub Python Edit Contacts Library
```Python
import requests
import json

# authentication
x_username      = "";
x_apikey        = "";

# data
name            = "John New" # new contact name
phone           = "+2507xxxxxxxx" # new phonenumber - international format
tags            = "Edited Tag 1, Edited Tag" # new tags - comma separated tags
groups          = "New Group1" # new groups - optional groups to link contact

# id of contact to edit: this can be gotten from the fetch contacts api
contactId       = "1";

# endoint
editContactURL  = "https://api.braceafrica.com/v1/contacts/edit/"+contactId

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

params = {
    'name' : name,
    'phone' : phone,
    'tags' : tags,
    'groups': groups
}

req = requests.post(editContactURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful editing of a contact:
```json
{
    "status": 200,
    "message": "Contact updated"
}
```
# Onehub Python Fetch Contacts Library
```Python
import requests
import json

# authentication
x_username        = "";
x_apikey          = "";

# endoint
fetchContactURL   = "https://api.braceafrica.com/v1/contacts/fetch"

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

req = requests.get(fetchContactURL, headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful fetching of a contact:
```json
{
    "status": 200,
    "contacts": [
        {
            "id": 2,
            "name": "Jane Mwaura",
            "phoneNumber": "+254712345678",
            "tags": "kenya,nairobi",
            "groups": [],
            "createdOn": "2019-12-02T00:00:00.000Z",
            "lastEditedOn": null
        }
    ]
}
```
# Onehub Python Delete Contacts Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

# id of contact to delete
params = {
    "contactIds":[1,2,3,4]
}

# endoint
deleteContactURL   = "https://api.braceafrica.com/v1/contacts/delete

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

req = requests.post(deleteContactURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
## ```!``` Please note that this will also remove the contact from all linked groups.
```json
{
    "contactIds": [1,2,3,4]
}
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Onehub Python Create Group Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

params = {
    "name": "",
    "tags": "",
}

# endpoint
addGroupURL = "https://api.braceafrica.com/v1/contacts/groups/add"

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

# endoint
req = requests.post(addGroupURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Onehub Python Edit Group Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

params = {
    "name": "",
}

groupId = ""

# endpoint
editGroupURL = "https://api.braceafrica.com/v1/contacts/groups/edit/" + groupId

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

# endoint
req = requests.post(editGroupURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful editing of a group:
```json
{
    "status": 200,
    "message": "Group has been updated"
}
```
# Onehub Python Fetch Group Library
```Python
import requests
import json

# authentication
x_username        = "";
x_apikey          = "";

# endoint
fetchGroupsURL   = "https://api.braceafrica.com/v1/contacts/groups/fetch"

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

req = requests.get(fetchGroupsURL, headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching of a group:
```json
{
    "status": 200,
    "groups": [
        {
            "groupId": 12,
            "groupName": "Kenzu Safaris",
            "createdOn": "2019-05-17T00:00:00.000Z",
            "contacts": []
        }
    ]
}
```
# Onehub Python Link Contacts To Group Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

params = {
    "contactIds": [1,2,3,4]
}

groupId = ""

# endpoint
addContactsToGroupURL = "https://api.braceafrica.com/v1/contacts/add/" + groupId

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

# endoint
req = requests.post(addContactsToGroupURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful linking contacts to a group:
```json
{
    "status": 200,
    "message": "The contacts linked to group"
}
```
# Onehub Python Fetch Group Contacts Library
```Python
import requests
import json

# authentication
x_username        = "";
x_apikey          = "";

groupId = ""

# endoint
fetchGroupContactsURL   = "https://api.braceafrica.com/v1/contacts/groups/fetch/" + groupId

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

req = requests.get(fetchGroupContactsURL, headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching group contacts:
```json
{
    "groupId": 2536,
    "groupName": "Chama Ya Mama",
    "contacts": [
        {
            "id": 65,
            "name": "John Doe",
            "phoneNumber": "+2547xxx4578",
            "tags": "chairman"
        },
        {
            "id": 63,
            "name": "Pendo JM",
            "phoneNumber": "+2547xxy4597",
            "tags": "member"
        }
    ]
}
```
# Onehub Python Remove Group Contacts Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

params = {
    "contactIds": [1,2,3,4],
}

groupId = ""

# endpoint
deleteGroupContactsURL = "https://api.braceafrica.com/v1/contacts/delete/" + groupId

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

# endoint
req = requests.post(deleteGroupContactsURL, data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful removing group contacts:
```json
{
    "status": 200,
    "message": "Contacts removed form group"
}
```
# Onehub Python Delete Groups Library
```Python
import requests
import json

# authentication
x_username         = "";
x_apikey           = "";

# endpoint
deleteGroupURL = "https://api.braceafrica.com/v1/contacts/groups/delete"

params = {
    "groupIds":[1,2,3,4]
}

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

# endoint
req = requests.post(deleteGroupURL,data=json.dumps(params), headers=headers)

# response
print(req.text)
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful deleting groups:
```json
{
    "status": 200,
    "message": "4 groups have been deleted"
}
```
# Onehub Python Sender Ids Library
```Python
import requests
import json

# authentication
x_username        = "";
x_apikey          = "";

# endoint
fetchSenderidsURL   = "https://api.braceafrica.com/v1/sms/senderIds/fetch"

headers = {
    'Content-type': 'application/json',
    'Accept': 'application/json',
    'x-api-user': x_username,
    'x-api-key' : x_apikey
}

req = requests.get(fetchSenderidsURL, headers=headers)

# response
print(req.text)
```
# Response Body Parameters
## Response in case of successful fetching of Sender Ids:
```json
{
    "status": 200,
    "senderids": [
        {
            "sender_id": "BraceAfrica",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "JubaPay",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "Foleni",
            "country": "Uganda",
            "status": "active"
        }
    ]
}
```
