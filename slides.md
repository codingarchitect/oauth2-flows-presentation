## OAuth2 flows 
---

### Based on Diagrams And Movies Of All The OAuth 2.0 Flows
#### by Takahiko Kawasaki
[https://darutk.medium.com/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85](https://darutk.medium.com/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85)

---

<p class="stretch"><img src="images/01-authorization-code-flow.png"/></p>

---

<div class="stretch"><iframe src="https://www.youtube.com/embed/7D-OU4hZW70" data-autoplay height="100%" width="100%"></iframe></div>

---

### Request To Authorization Endpoint
<section>
  <pre><code data-trim data-noescape>
GET {Authorization Endpoint}
  ?response_type=code             // - Required
  &client_id={Client ID}          // - Required
  &redirect_uri={Redirect URI}    // - Conditionally required
  &scope={Scopes}                 // - Optional
  &state={Arbitrary String}       // - Recommended
  &code_challenge={Challenge}     // - Optional
  &code_challenge_method={Method} // - Optional
  HTTP/1.1
HOST: {Authorization Server}
  </code></pre>
</section>

---

### Response From Authorization Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 302 Found
Location: {Redirect URI}
  ?code={Authorization Code}  // - Always included
  &state={Arbitrary String}   // - Included if the authorization
                              //   request included 'state'.
  </code></pre>
</section>

---

### Request To Token Endpoint
<section>
  <pre><code data-trim data-noescape>
POST {Token Endpoint} HTTP/1.1
Host: {Authorization Server}
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code  // - Required
&code={Authorization Code}     // - Required
&redirect_uri={Redirect URI}   // - Required if the authorization
                               //   request included 'redirect_uri'.
&code_verifier={Verifier}      // - Required if the authorization
                               //   request included
                               //   'code_challenge'.
  </code></pre>
</section>

---

### Response From Token Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
{
  "access_token": "{Access Token}",    // - Always included
  "token_type": "{Token Type}",        // - Always included
  "expires_in": {Lifetime In Seconds}, // - Optional
  "refresh_token": "{Refresh Token}",  // - Optional
  "scope": "{Scopes}"                  // - Mandatory if the granted
                                       //   scopes differ from the
                                       //   requested ones.
}
  </code></pre>
</section>

---

<p class="stretch"><img src="images/02-implicit-flow.png"/></p>

---

<div class="stretch"><iframe src="https://www.youtube.com/embed/KUruB156-h4" data-autoplay height="100%" width="100%"></iframe></div>

---

### Request To Authorization Endpoint
<section>
  <pre><code data-trim data-noescape>
GET {Authorization Endpoint}
  ?response_type=token          // - Required
  &client_id={Client ID}        // - Required
  &redirect_uri={Redirect URI}  // - Conditionally required
  &scope={Scopes}               // - Optional
  &state={Arbitrary String}     // - Recommended
  HTTP/1.1
HOST: {Authorization Server}
  </code></pre>
</section>

---

### Response From Authorization Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 302 Found
Location: {Redirect URI}
  #access_token={Access Token}       // - Always included
  &token_type={Token Type}           // - Always included
  &expires_in={Lifetime In Seconds}  // - Optional
  &state={Arbitrary String}          // - Included if the request
                                     //   included 'state'.
  &scope={Scopes}                    // - Mandatory if the granted
                                     //   scopes differ from the
                                     //   requested ones.
  </code></pre>
</section>

---

<p class="stretch"><img src="images/03-resource-owner-password-credentials-flow.png"/></p>

---

<div class="stretch"><iframe src="https://www.youtube.com/embed/CGMiOHrOAYQ" data-autoplay height="100%" width="100%"></iframe></div>

---

### Request To Token Endpoint
<section>
  <pre><code data-trim data-noescape>
POST {Token Endpoint} HTTP/1.1
Host: {Authorization Server}
Content-Type: application/x-www-form-urlecoded
grant_type=password    // - Required
&username={User ID}    // - Required
&password={Password}   // - Required
&scope={Scopes}        // - Optional
  </code></pre>
</section>

---

### Response From Token Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
{
  "access_token": "{Access Token}",    // - Always included
  "token_type": "{Token Type}",        // - Always included
  "expires_in": {Lifetime In Seconds}, // - Optional
  "refresh_token": "{Refresh Token}",  // - Optional
  "scope": "{Scopes}"                  // - Mandatory if the granted
                                       //   scopes differ from the
                                       //   requested ones.
}
  </code></pre>
</section>

---

<p class="stretch"><img src="images/04-client-credentials-flow.png"/></p>

---

<div class="stretch"><iframe src="https://www.youtube.com/embed/XJuFcXI2v2k" data-autoplay height="100%" width="100%"></iframe></div>

---

### Request To Token Endpoint
<section>
  <pre><code data-trim data-noescape>
POST {Token Endpoint} HTTP/1.1
Host: {Authorization Server}
Authorization: Basic {Client Credentials}
Content-Type: application/x-www-form-urlecoded
grant_type=client_credentials  // - Required
&scope={Scopes}                // - Optional
  </code></pre>
</section>

---

### Response From Token Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
{
  "access_token": "{Access Token}",    // - Always included
  "token_type": "{Token Type}",        // - Always included
  "expires_in": {Lifetime In Seconds}, // - Optional
  "scope": "{Scopes}"                  // - Mandatory if the granted
                                       //   scopes differ from the
                                       //   requested ones.
}
  </code></pre>
</section>

---

<p class="stretch"><img src="images/05-refresh-token-flow.png"/></p>

---

<div class="stretch"><iframe src="https://www.youtube.com/embed/jcKDsQfBgYY" data-autoplay height="100%" width="100%"></iframe></div>

---

### Request To Token Endpoint
<section>
  <pre><code data-trim data-noescape>
POST {Token Endpoint} HTTP/1.1
Host: {Authorization Server}
Content-Type: application/x-www-form-urlecoded
grant_type=refresh_token        // - Required
&refresh_token={Refresh Token}  // - Required
&scope={Scopes}                 // - Optional
  </code></pre>
</section>

---

### Response From Token Endpoint
<section>
  <pre><code data-trim data-noescape>
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
{
  "access_token": "{Access Token}",    // - Always included
  "token_type": "{Token Type}",        // - Always included
  "expires_in": {Lifetime In Seconds}, // - Optional
  "refresh_token": "{Refresh Token}",  // - Optional
  "scope": "{Scopes}"                  // - Mandatory if the granted
                                       //   scopes differ from the
                                       //   original ones.
}
  </code></pre>
</section>

---