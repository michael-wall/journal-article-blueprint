



## Setup ##
- Enable the Search Headless API BETA Feature Flag
  - Instance Settings > Feature Flags > Beta > Search Headless API (LPS-179669)
- Setup the Web Content Article Custom fields - see journal-article-publications README.
- Import the 'WCM Expando Field By PostLoginReference' using Control Panel > Applications > Search Experiences > Blueprints screen and the provided WCM Expando Field By PostLoginReference.json
  - If importing into an environment that uses 'en-GB' instead of 'en-GB' then replace references to 'en-US' with 'en-GB' in the json file BEFORE importing.
  - Update the Limit Search to These Sites > Group IDs and Save.
- Add some new Content Articles to the Site from above (either directly in Production or via a Publication that you then Publish).
  - Populate the PostLogin / PostLoginReference custom fields with test data.
 
## To perform a Search ##
 - Go to http://localhost:8080/o/api?endpoint=http://localhost:8080/o/portal-search-rest/v1.0/openapi.json
 - Expand the postSearch Results endpoint
 - Set Search field to *
 - Paste the following into the Request Body field, ensuring the External Reference Code matches the Blueprint and with a valid postLoginReference value:
```
{
  "attributes": {
    "search.experiences.blueprint.external.reference.code": "mw-expando",
    "search.experiences.postLoginReference": "peach"
  }
}
```
- Click 'Execute' to trigger the search.
- Sample result:
```
{
  "items": [
    {
      "dateModified": "2026-02-12T18:58:23Z",
      "description": "article 4 true peach-mw",
      "itemURL": "http://localhost:8080/o/headless-delivery/v1.0/structured-contents/33183",
      "score": 4.633839,
      "title": "article 4"
    },
    {
      "dateModified": "2026-02-12T18:58:30Z",
      "description": "article 8 true peach-mw",
      "itemURL": "http://localhost:8080/o/headless-delivery/v1.0/structured-contents/33224",
      "score": 4.633839,
      "title": "article 8"
    },
    {
      "dateModified": "2026-02-12T18:58:37Z",
      "description": "article 11 true peach-mw",
      "itemURL": "http://localhost:8080/o/headless-delivery/v1.0/structured-contents/33328",
      "score": 4.633839,
      "title": "article 11"
    },
    {
      "dateModified": "2026-02-13T13:40:26Z",
      "description": "article 1 true peach-mw",
      "itemURL": "http://localhost:8080/o/headless-delivery/v1.0/structured-contents/33153",
      "score": 4.633839,
      "title": "article 1"
    }
  ],
  "lastPage": 1,
  "page": 1,
  "pageSize": 20,
  "totalCount": 4
}
```

## Notes ##
- This is a ‘proof of concept’ that is being provided ‘as is’ without any support coverage or warranty.
