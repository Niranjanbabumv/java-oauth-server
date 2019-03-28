Niranjans Playground and get the permission on any changes

License
-------

  Apache License, Version 2.0


Source Code
-----------

  <code>https://github.com/authlete/java-oauth-server</code>




How To Run
----------

1. Download the source code of this authorization server implementation.

        $ git clone https://github.com/authlete/java-oauth-server.git
        $ cd java-oauth-server

2. Edit the configuration file to set the API credentials of yours.

        $ vi authlete.properties

3. Make sure that you have installed [maven][42] and set `JAVA_HOME` properly.

4. Start the authorization server on [http://localhost:8080][38].

        $ mvn jetty:run &

#### Run With Docker

If you would prefer to use Docker, just hit the following command after the step 2.

    $ docker-compose up

#### Configuration File

`java-oauth-server` refers to `authlete.properties` as a configuration file.
If you want to use another different file, specify the name of the file by
the system property `authlete.configuration.file` like the following.

    $ mvn -Dauthlete.configuration.file=local.authlete.properties jetty:run &

Endpoints
---------

This implementation exposes endpoints as listed in the table below.

| Endpoint               | Path                                |
|:-----------------------|:------------------------------------|
| Authorization Endpoint | `/api/authorization`                |
| Token Endpoint         | `/api/token`                        |
| JWK Set Endpoint       | `/api/jwks`                         |
| Configuration Endpoint | `/.well-known/openid-configuration` |
| Revocation Endpoint    | `/api/revocation`                   |
| Introspection Endpoint | `/api/introspection`                |

The authorization endpoint and the token endpoint accept parameters described
in [RFC 6749][1], [OpenID Connect Core 1.0][13],
[OAuth 2.0 Multiple Response Type Encoding Practices][33], [RFC 7636][14]
([PKCE][15]) and other specifications.

The JWK Set endpoint exposes a JSON Web Key Set document (JWK Set) so that
client applications can (1) verify signatures by this OpenID Provider and
(2) encrypt their requests to this OpenID Provider.

The configuration endpoint exposes the configuration information of this
OpenID Provider in the JSON format defined in [OpenID Connect Discovery 1.0][35].

The revocation endpoint is a Web API to revoke access tokens and refresh
tokens. Its behavior is defined in [RFC 7009][21].

The introspection endpoint is a Web API to get information about access
tokens and refresh tokens. Its behavior is defined in [RFC 7662][32].


Authorization Request Example
-----------------------------

The following is an example to get an access token from the authorization
endpoint using [Implicit Flow][16]. Don't forget to replace `{client-id}` in
the URL with the real client ID of one of your client applications. As for
client applications, see [Getting Started][10] and the [document][17] of
_Developer Console_.

    http://localhost:8080/api/authorization?client_id={client-id}&response_type=token

The request above will show you an authorization page. The page asks you to
input login credentials and click "Authorize" button or "Deny" button. Use
one of the following as login credentials.

| Login ID | Password |
|:--------:|:--------:|
|   Niranjan  |   babu   |
|   Prash   |   Sonnadmath   |

Of course, these login credentials are dummy data, so you need to replace
the user database implementation with your own.


Customization
-------------

How to customize this implementation is described in [CUSTOMIZATION.md][39].
Basically, you need to do programming for _end-user authentication_ because
Authlete does not manage end-user accounts. This is by design. The
architecture of Authlete carefully seperates authorization from authentication
so that you can add OAuth 2.0 and OpenID Connect functionalities seamlessly
into even an existing web service which may already have a mechanism for
end-user authentication.



