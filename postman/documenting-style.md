<i>Last updated: August 16, 2022 02:17 PM</i>

### Documenting Style Rules

#### # Endpoint Documentation
These are the rules when documenting an endpoint in Postman
1. It should started with the title and it must be in short sentences and summarize what the API doing.
2. The next one is the description, you have to explain everything in detail so that it is easy for new developers to understand.
3. It should list all the attribute such as the URL, params, queries, Authorization, authorization type, authorization rules, request body, etc.
4. It should describe the parameters, what it does and what options are acceptable to each parameter.
5. It should describe the parameter type (string or number, or boolean, or anything else).
6. It should describe is the parameter is optional or required to fill.
7. If the endpoint request accepting data from `Params` then you should fill the descrption in `DESCRIPTION` column in the `Params` table, but if it's in `Body` such as JSON format or anything else you should describe it in the `Documentation` panel on the right side of Postman.
8. If authentication is optional you should describe it that the endpoint doesn't require user authentication.
9. If the result of the authenticated request is different from the unauthenticated request, then you should describe what is the difference.

#### # Order
```
[title]

[descriptions]

[options]
```

#### # Example
```
Count user collections by User ID

Auth is optional, if auth is present, and authenticated user is the owner of the collection, it will show all private collections.
But if it's not the authorized user or the owner, count the public collections only.

**URL**
/user/user_id/count/collection

**AUTH**
bearer, optional
```
