# API Overview



1. Log in by calling POST <code>https://freddy.codesubmit.io/login</code> \
In the response, you will get Bearer access token (valid for 15 minutes) and refresh token (valid for 30 days);
2. Get dashboard data by calling GET <code>https://freddy.codesubmit.io/dashboard</code> \
Here you will use the access token you got in step 1.  \
However, since the token is valid for 15 minutes, you may need to request a fresh one by calling POST <code>https://freddy.codesubmit.io/refresh</code> \
When requesting a new token, you will need to use the refresh token you got in step 1.\
3. Fetch orders by calling GET <code>https://freddy.codesubmit.io/orders?page=1&q=search_term</code>


# Login

## Method

POST <code>https://freddy.codesubmit.io/login</code>

Used to log in.

## Parameters


<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Mandatory</strong>
   </td>
  </tr>
  <tr>
   <td><code>username</code>
   </td>
   <td>string
   </td>
   <td>Username
   </td>
   <td>Yes
   </td>
  </tr>
  <tr>
   <td><code>password</code>
   </td>
   <td>string
   </td>
   <td>Password
   </td>
   <td>Yes
   </td>
  </tr>
</table>


cURL example


```
curl --location --request POST 'https://freddy.codesubmit.io/login' \
--form 'username="freddy"' \
--form 'password="ElmStreet2019"'
```



## Example Response

```
{
   "username": "freddy",
   "password": "ElmStreet2019",
   "access_token": "SPFPQ5IBLB6DPE6FKPWHMIWW4MCR",
   "refresh_token": "FL4GSVQS4W5CKSFRVZBLPIVZZJ2"
   
 }
```



## Response Fields


<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>username
   </td>
   <td>string
   </td>
   <td>Username
   </td>
  </tr>
  <tr>
   <td>password
   </td>
   <td>string
   </td>
   <td>Password
   </td>
  </tr>
  <tr>
   <td>access_token
   </td>
   <td>string
   </td>
   <td>Bearer access token that is valid for 15 minutes
   </td>
  </tr>
  <tr>
   <td>refresh_token
   </td>
   <td>string
   </td>
   <td>Bearer refresh token that is valid for 30 days
   </td>
  </tr>
</table>



## HTTP Response


<table>
  <tr>
   <td>Code
   </td>
   <td>Status
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>OK
   </td>
   <td>The request has succeeded.
   </td>
  </tr>
  <tr>
   <td>404
   </td>
   <td>Not Found
   </td>
   <td>The user was not found or the password was incorrect. The response will be empty.
   </td>
  </tr>
</table>



# Get Dashboard Data

## Method

GET <code>https://freddy.codesubmit.io/dashboard</code>

Used to retrieve the data for the dashboard. 

## Parameters


<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Mandatory</strong>
   </td>
  </tr>
  <tr>
   <td><code>access_token</code>
   </td>
   <td>string
   </td>
   <td>Bearer access token that you retrieved from login.
<p>
Note that the token is valid for 15 minutes, so you should request a fresh one.
   </td>
   <td>Yes
   </td>
  </tr>
</table>


cURL example


```
curl --location --request POST 'https://freddy.codesubmit.io/dashboard' \
--header 'Authorization: Bearer access_token' \
```


## Response

Revenue and Bestsellers are returned.


## HTTP Response


<table>
  <tr>
   <td>Code
   </td>
   <td>Status
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>OK
   </td>
   <td>The request has succeeded.
   </td>
  </tr>
  <tr>
   <td>400
   </td>
   <td>Bad Request
   </td>
   <td>The access token is invalid.
   </td>
  </tr>
</table>



# Refresh Access Token

## Method

POST <code>https://freddy.codesubmit.io/refresh</code>

Used to request a fresh access token. 

## Parameters


<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Mandatory</strong>
   </td>
  </tr>
  <tr>
   <td><code>refresh_token</code>
   </td>
   <td>string
   </td>
   <td>Bearer refresh token that you retrieved from login.
   </td>
   <td>Yes
   </td>
  </tr>
</table>


cURL example


```
curl --location --request POST 'https://freddy.codesubmit.io/refresh' \
--header 'Authorization: Bearer refresh_token' \
```


## Example Response


```
{
  "access_token": "BWjcyMzY3ZDhiNmJkNTY",
  "token_type": "bearer",
  "expires": 900
}
```



## HTTP Response


<table>
  <tr>
   <td>Code
   </td>
   <td>Status
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>OK
   </td>
   <td>The request has succeeded.
   </td>
  </tr>
</table>



# Fetch Orders

## Method

GET <code>https://freddy.codesubmit.io/orders?page=1&q=search_term</code>

Used to fetch orders. 

## Parameters


<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
   <td><strong>Mandatory</strong>
   </td>
  </tr>
  <tr>
   <td><code>access_token</code>
   </td>
   <td>string
   </td>
   <td>Bearer access token that you retrieved from login. Since this one is valid for 15 minutes, you may need to request a fresh one.
   </td>
   <td>Yes
   </td>
  </tr>
  <tr>
   <td><code>page</code>
   </td>
   <td>integer
   </td>
   <td>Specifies which page of results to return
   </td>
   <td>No
   </td>
  </tr>
  <tr>
   <td><code>search_term</code>
   </td>
   <td>string
   </td>
   <td>Particular search term 
   </td>
   <td>No
   </td>
  </tr>
</table>


cURL example


```
curl --location --request GET ' https://freddy.codesubmit.io/orders?page=1&q=search_term' \
--header 'Authorization: Bearer access_token' \
```



## Response

A list of items is returned.


## HTTP Response


<table>
  <tr>
   <td>Code
   </td>
   <td>Status
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>OK
   </td>
   <td>The request has succeeded.
   </td>
  </tr>
  <tr>
   <td>400
   </td>
   <td>Bad Request
   </td>
   <td>The access token is invalid.
   </td>
  </tr>
</table>
