<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
<!-- [![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url] -->
[![LinkedIn][linkedin-shield]][linkedin-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/github_username/repo_name">
    <img src="images/white_logo.png" alt="Logo" width="100" height="">
  </a>

<h3 align="center">Authentication (v 1.0.0)</h3>

  <p align="center">
    This repo contatins all the necessary information for developers to interact with Vastmindz's authentication service and obtain websocket authentication tokens.
    <br />
  </p>
</div>


<!-- ABOUT THE PROJECT -->
## About The Project

To use Vastmindz's SDKs, you must first authenticate with our authentication service. This service will provide you with a websocket token that you can use to connect to our websocket server. This token will be valid for only one use. You will need to generate a new token for each websocket connection.


<!-- GETTING STARTED -->
## Getting started
The authentication service is a simple REST API that will return a websocket token. To use this service, you must first obtain access credentials from your Vastmindz representive. The below is the basic structure of the authentication request.

You MUST first obtain the credentials below from your Vastmindz representative.

```
USERNAME=<YOUR USERNAME>
PASSWORD=<YOUR PASSWORD>
MASTER_TOKEN=<YOUR MASTER TOKEN>
```

The credentials will be specific to your environment. The following environments are available and the following prefixes will be used:
```
rppg-dev2 = Development Environment
rppg-prod = Production Environment
```

The structure of the request is as follows:

- **URL**
  - https://```{{ENVIRONMENT}}```.xyz/admin-basic/access/onetime-key/generate
- **Method**
    `POST`
- **Basic Auth params**
        {
            "username": "string",
            "password": "string"
        }
- **Body**
    {
        "token": "```{{MASTER TOKEN}}```"
    }

- **Success Response**
```JSON
{
    "id": "YOUR COMPANY ID",
    "token":"YOUR WEBSOCKET TOKEN",
    "parentToken":"YOUR MASTER TOKEN",
    "used":false,
}
```
Explanation of the response:
- **id** - Your company id
- **token** - Your websocket token (this is the generated token you can use to make requests to our websocket server)
- **parentToken** - Your master token (this is the token you used to generate the websocket token)
- **used** - Whether or not the token has been used

<!-- EXAMPLES -->
## Examples

You can use the following examples to get started with generating authentication keys. You will need to replace the environment variable with the environment you are using. You will also need to replace the USERNAME, PASSWORD, and MASTER_TOKEN variables with the credentials you received from your Vastmindz representive.

**PLEASE NOTE THAT EACH EXAMPLE MUST BE TESTED THOROUGHLY ON YOUR SIDE BEFORE DEPLOYING**

**Python**
```python
import requests
import os

# Specify the environment
environment = "rppg-dev2"

# Construct the URL
url = "https://" + "environment" + ".xyz/admin-basic/access/onetime-key/generate"

# Make a basic auth request
auth = requests.auth.HTTPBasicAuth(os.getenv("USERNAME"), os.getenv("PASSWORD"))

body = {
    "token": os.getenv("MASTER_TOKEN")
}

# Make the request
response = requests.post(url, auth=auth, json=body)

# Print the response
print(response.text)
```

**Javascript**
```javascript
// Specify the environment
const environment = "rppg-dev2";

// Construct the URL
const url = "https://" + environment + ".xyz/admin-basic/access/onetime-key/generate";

// Create an object to store the request headers
const headers = new Headers();

// Set the "Authorization" header
headers.set("Authorization", "Basic " + btoa(process.env.USERNAME + ":" + process.env.PASSWORD));

// Set the "Content-Type" header
headers.set("Content-Type", "application/json");

// Create an object to store the request body
const body = {
    token: process.env.MASTER_TOKEN
};

// Make the request
fetch(url, {
    method: "POST",
    headers: headers,
    body: JSON.stringify(body)
})
.then(response => {
    // Print the response
    console.log(response.text);
});
```

**cURL**
```bash
curl -X POST "https://{{ENVIRONMENT}}.xyz/admin-basic/access/onetime-key/generate" \
-H "Authorization: Basic {{base64 encoded string}}" \
-H "Content-Type: application/json" \
-d '{"token":"{{MASTER_TOKEN}}"}'
```

**SWIFT (iOS)**
```swift
import Foundation

let environment = "rppg-prod"
let url = "https://" + environment + ".xyz/admin-basic/access/onetime-key/generate"
let auth = URLCredential(user: "<YOUR USERNAME>", password: "<YOUR PASSWROD>", persistence: .none)
let body: [String: Any] = ["token": "<YOUR MASTER TOKEN>"]
let jsonData = try! JSONSerialization.data(withJSONObject: body)

var request = URLRequest(url: URL(string: url)!)
request.httpMethod = "POST"
request.setValue("application/json", forHTTPHeaderField: "Content-Type")
request.httpBody = jsonData
request.addValue("Basic \(auth.base64Encoded)", forHTTPHeaderField: "Authorization")

let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    if let error = error {
        print(error)
        return
    }

    if let data = data, let responseText = String(data: data, encoding: .utf8) {
        print(responseText)
    }
}

task.resume()
```

<!-- CONTACT -->
## Contact

- Twitter: [@vastmindz](https://twitter.com/vastmindz)
- Email: team@vastmindz.com

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo_name.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo_name/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_username/repo_name.svg?style=for-the-badge
[forks-url]: https://github.com/github_username/repo_name/network/members
[stars-shield]: https://img.shields.io/github/stars/github_username/repo_name.svg?style=for-the-badge
[stars-url]: https://github.com/github_username/repo_name/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_username/repo_name.svg?style=for-the-badge
[issues-url]: https://github.com/github_username/repo_name/issues
[license-shield]: https://img.shields.io/github/license/github_username/repo_name.svg?style=for-the-badge
[license-url]: https://github.com/Vastmindz-Public-Repository/Web-SDK/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/company/28917477/admin/
[product-screenshot]: images/screenshot.png
[Next.js]: https://img.shields.io/badge/next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white
[Next-url]: https://nextjs.org/
[React.js]: https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB
[React-url]: https://reactjs.org/
[Vue.js]: https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D
[Vue-url]: https://vuejs.org/
[Angular.io]: https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white
[Angular-url]: https://angular.io/
[Svelte.dev]: https://img.shields.io/badge/Svelte-4A4A55?style=for-the-badge&logo=svelte&logoColor=FF3E00
[Svelte-url]: https://svelte.dev/
[Laravel.com]: https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white
[Laravel-url]: https://laravel.com
[Bootstrap.com]: https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white
[Bootstrap-url]: https://getbootstrap.com
[JQuery.com]: https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white
[JQuery-url]: https://jquery.com 


