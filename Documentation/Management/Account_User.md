---
uid: accountUser
---

User
=======================================================



	For HTTP requests and responses, the User object has the following properties and JSON-serialized body: 

#### UserObj 

``string Id``
	GUID for this User. Generated by the server upon Creation. Same as AAD UserId.
``string FirstName``
	First Name for this User.
``string LastName``
	Last Name for this User.
``string LoginName``
	Login Name for this User.
``string ContactEmail``
	Contact email address for this User.
``string ContactPhone``
	Contact phone number for this User.
``string UPN``
	Principal unique name for this User.
``[Role] Roles``
	List of Roles for this User. Returned during get calls and can be specified during creation to add the Roles to the new User by Role.Id.
``JObject Preferences``
	A JSON string object denoting user preferences for the OCS portal

.. highlight:: C#

    	HTTP/1.1 200
    	Content-Type: application/json

     {
    	"Id": "id",
    	"FirstName": "firstname",
    	"LastName": "lastname",
    	"LoginName": "loginname",
    	"ContactEmail": "contactemail",
    	"ContactPhone": "contactphone",
    	"UPN": "upn",
    	"Roles": [],
    	"Preferences":  { }
     }

**********************

``Get()``
--------------------------------------------------------------------

Returns a user in an account.

**Http**

    	GET api/Tenants/{tenantId}/Users/{userId}

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier for the user

**Security**  
Allowed by Account Member and Account Administrator [Roles](xref:accountRole#roleobj)

**Returns**  
The [User](#userobj) with the specified userId

**********************

``GetAll()``
--------------------------------------------------------------------

Returns a list of all OCS users in an account.

**Http**

    	GET api/Tenants/{tenantId}/Users

**Parameters**

``string tenantId``
	The identifier for the account

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
An array of [User](#userobj) objects belonging to the account with the specified tenantId

**********************

``Create()``
--------------------------------------------------------------------

Create a User for an account.

**Http**

    	POST api/Tenants/{tenantId}/Users/

**Parameters**

``string tenantId``
	The identifier for the account
``CreateUser user``
	[CreateUser](#createuserobj) object for this request

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
The created [User](#userobj)

**Notes**  
For HTTP requests and responses, the CreateUser object has the following properties and JSON-serialized body: 

#### CreateUserObj 

``optional: bool SendNotification``
	Boolean specifying whether an email should be sent to the new user's account.
``string Id``
	GUID for this User. Generated by the server upon Creation. Same as AAD UserId.
``string FirstName``
	First Name for this User.
``string LastName``
	Last Name for this User.
``string LoginName``
	Login Name for this User.
``string ContactEmail``
	Contact email address for this User.
``string ContactPhone``
	Contact phone number for this User.
``string UPN``
	Principal unique name for this User.
``[Role] Roles``
	List of Roles for this User. Returned during get calls and can be specified during creation to add the Roles to the new User by Role.Id.
``JObject Preferences``
	A JSON string object denoting user preferences for the OCS portal

.. highlight:: C#

    	HTTP/1.1 200
    	Content-Type: application/json

     {
    	"Id": "id",
    	"FirstName": "firstname",
    	"LastName": "lastname",
    	"LoginName": "loginname",
    	"ContactEmail": "contactemail",
    	"ContactPhone": "contactphone",
    	"UPN": "upn",
    	"Roles": [],
    	"Preferences":  { }
     }

**********************

``Update()``
--------------------------------------------------------------------

Updates a specified user.

**Http**

    	PUT api/Tenants/{tenantId}/Users/{userId}

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The user identifier for the request
``User user``
	The [User](#userobj) to be updated

**Security**  
Cluster Operator, Account Administrator, or Account Member (self).

**Returns**  
The updated [User](#userobj)

**********************

``Delete()``
--------------------------------------------------------------------

Delete a specified user.

**Http**

    	DELETE api/Tenants/{tenantId}/Users/{userId}

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The [User](#userobj) to be deleted

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
Nothing is returned

**********************

``ResetUserPassword()``
--------------------------------------------------------------------

Resets the password for the specified user.

**Http**

    	POST api/Tenants/{tenantId}/Users/{userId}/PasswordReset

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose password is to be reset

**Security**  
Account admin, Cluster Operator, or User on self.

**Returns**  
Nothing is returned

**********************

``GetAllRolesForUser()``
--------------------------------------------------------------------

Retrieves all roles for the specified user.

**Http**

    	GET api/Tenants/{tenantId}/Users/{userId}/Roles

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose roles will be retrieved
``string skip``
	Number of [Roles](xref:accountRole#roleobj) to ignore
``string count``
	Number of [Roles](xref:accountRole#roleobj) to be returned
``string query``
	Unsupported parameter

**Security**  
Allowed by Account Member and Account Administrator [Roles](xref:accountRole#roleobj)

**Returns**  
An array of [Role](xref:accountRole#roleobj) objects belonging to the user with the specified userId.

**********************

``AddAccountRoleToUser()``
--------------------------------------------------------------------

Adds an account role to the specified user.

**Http**

    	PUT api/Tenants/{tenantId}/Users/{userId}/Roles/{roleId}

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) who will be given the role
``string roleId``
	The identifier of the role to add to the [User](#userobj)

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
The [Role](xref:accountRole#roleobj) with the specified roleId

**********************

``RemoveAccountRoleFromUser()``
--------------------------------------------------------------------

Removes a role from a user.

**Http**

    	DELETE api/Tenants/{tenantId}/Users/{userId}/Roles/{roleId}

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose role will be removed
``string roleId``
	The identifier of the role to remove from the [User](#userobj)

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
Nothing is returned

**********************

``ReplaceUserRoles()``
--------------------------------------------------------------------

Replace the roles of a user with a new list of roles.

**Http**

    	PUT api/Tenants/{tenantId}/Users/{userId}/Roles

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose roles will be replaced
``[Role] newRoles``
	From the body. An array of [Role](xref:accountRole#roleobj) objects to set as the Roles for the specified user

**Security**  
Allowed by Account Administrator and Community Lead [Roles](xref:accountRole#roleobj)

**Returns**  
An array of all [Role](xref:accountRole#roleobj) objects assigned to the user specified by userId after the replacement operation is complete

**********************

``GetUserPrefs()``
--------------------------------------------------------------------

Gets OCS Portal Preferences for a specific user

**Http**

    	GET api/Tenants/{tenantId}/Users/{userId}/Preferences

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose roles will be replaced

**Security**  
Admins or the User making a call for themself.

**Returns**  
The JSON representation of user preferences

**********************

``UpdateUserPrefs()``
--------------------------------------------------------------------

Updates OCS Portal Preferences for a specific user

**Http**

    	PUT api/Tenants/{tenantId}/Users/{userId}/Preferences

**Parameters**

``string tenantId``
	The identifier for the account in which the user belongs
``string userId``
	The identifier of the [User](#userobj) whose roles will be replaced
``JObject preferences``
	JSON representation of user preferences used in the OCS portal

**Security**  
Admins or the User making a call for themself.

**Returns**  
Updated JSON representation of user preferences

**********************

``GetExternalUsers()``
--------------------------------------------------------------------

Returns a list of Azure Active Directory users that are not member of this account

**Http**

    	GET api/Tenants/{tenantId}/externalusers

**Parameters**

``string tenantId``
	The identifier for the account
``string skip``
	Number of users to skip for paging purposes.
``string count``
	Maximum number of users to return in this page.
``string query``
	Prefix match to filter users by, can be first name, last name, or email address.

**Security**  
Allowed by Account Administrator [Role](xref:accountRole#roleobj)

**Returns**  
An array of [User](#userobj) objects that could be added to this account.

**********************
