# service-performances

> [!WARNING]
> - [X] Not all text is translated by the Page Speed Insights
> - [X] Not all scores exists
> - [X] An URL can fails if it does not exists
> - [X] An URL may do not gives any insights

## API

- [Notes](#notes)
- [Add a route to analyse](#add-a-route-to-analyse)
- [Get a route](#get-a-route)
- [Get a route insights](#get-a-route-insights)
- [Update a route](#update-a-route)
- [Delete a route](#delete-a-route)
- [List the routes](#list-the-routes)

### Notes

The `category` parameters can be one of:

- `HOMEPAGE`
- `CATEGORY`
- `SUB_CATEGORY`
- `PRODUCT`
- `BLOG`
- `LANDING_PAGE`
- `OTHER`

The `frequency` parameters can be one of:

- `ONE_TIME`
- `WEEKLY`
- `MONTHLY`
- `DEBUG` (Only on `staging` environment)

### Add a route to analyse

```text
POST /routes
```

```json
{
  "user": {
    "id": "468be21d-5a9a-48c9-a46d-307e474bf746",
    "workspaces": ["678429b2-501d-4b07-ad51-cf594a3876ae"]
  },
  "workspaceId": "678429b2-501d-4b07-ad51-cf594a3876ae",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "url": "https://www.eskimoz.fr"
}
```

#### Response

```text
201 Created
```

```json
{
  "id": "1807cb90-d635-4c61-b8fc-df6868eb2265",
  "url": "https://www.senek.com",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "userId": "468be21d-5a9a-48c9-a46d-307e474bf746",
  "workspaceId": "678429b2-501d-4b07-ad51-cf594a3876ae",
  "error": false,
  "performance": null,
  "lastUpdate": null,
  "diff": null,
  "success": null
}
```

> [!NOTE]
> An URL can only be defined one time per workspace.

- `error` means that there is an error during the last processing of the
  performances. It means that the processing will no longer execute.
- `performance` is the performance score, between 0 and 100.
- `lastUpdate` is the last processing date.
- `diff` is the diff in percent (0 to 1) between the previous analyse and the last one.
- `success` means that the last processus score is considerered as good.

### Get a route

```
GET /routes/:id
```

#### Reponse

```
200 OK
```

```json
{
  "id": "a3634ae0-c337-44eb-b380-2df0530c59f3",
  "url": "https://www.eskimoz.co.uk",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
  "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
  "error": false,
  "performance": 98,
  "lastUpdate": "2024-07-21T12:50:21.674Z",
  "diff": -0.010204081632652962,
  "success": true
}
```

A query parameter `results` can be defined to `true` to get the main datas over
time:

> [!WARNING]
> This route must never be called on automated updates, like on the table view.

```
GET /routes/:id?results=true
```

#### Reponse

```json
{
  "id": "a3634ae0-c337-44eb-b380-2df0530c59f3",
  "url": "https://www.eskimoz.co.uk",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
  "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
  "error": false,
  "performance": 98,
  "lastUpdate": "2024-07-21T12:50:21.674Z",
  "diff": -0.010204081632652962,
  "results": [
    {
      "date": "2024-07-21T12:46:41.376Z",
      "insightsId": "7ad6f4d3-df79-4129-9301-55e4fd2a06b2",
      "cls": 0.04,
      "ttfb": 0.966,
      "fcp": 1723,
      "fid": null,
      "inp": 181,
      "lcp": 2.216,
      "performance": 99,
      "accessibility": 92,
      "best-practices": 100,
      "seo": 85,
      "overall": "AVERAGE",
      "diff": 0
    },
    {
      "date": "2024-07-21T12:47:01.381Z",
      "insightsId": "8967364a-d9b1-4842-8385-ba1b395d9805",
      "cls": 0.04,
      "ttfb": 0.966,
      "fcp": 1723,
      "fid": null,
      "inp": 181,
      "lcp": 2.216,
      "performance": 99,
      "accessibility": 92,
      "best-practices": 100,
      "seo": 85,
      "overall": "AVERAGE",
      "diff": 0
    },
    {
      "date": "2024-07-21T12:47:21.384Z",
      "insightsId": "9b83f872-21a2-4f81-a328-b67d6f1dc05e",
      "cls": 0.04,
      "ttfb": 0.966,
      "fcp": 1723,
      "fid": null,
      "inp": 181,
      "lcp": 2.216,
      "performance": 99,
      "accessibility": 92,
      "best-practices": 100,
      "seo": 85,
      "overall": "AVERAGE",
      "diff": 0
    }
  ],
  "success": true
}
```

> [!NOTE]
> The detailed results gives all the insights IDs, used on the specific request
> to get the details.

#### Reponse

```
200 OK
```

```json
{
  "id": "a3634ae0-c337-44eb-b380-2df0530c59f3",
  "url": "https://www.eskimoz.co.uk",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
  "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
  "error": false,
  "performance": 98,
  "lastUpdate": "2024-07-21T12:50:21.674Z",
  "diff": -0.010204081632652962,
  "success": true
}
```

### Get a route insights

```text
GET /routes/:id/insights/:insightsId
```

#### Response

```text
200 OK
```

> The content is too big to display on the documentation.

> [!WARNING]
> This call is very expensive, to use with caution. As those data are immutable,
> it can, and must be cached, on the local storage if possible.

### Update a route

```text
POST /routes/:id
```

```json
{
  "user": {
    "id": "468be21d-5a9a-48c9-a46d-307e474bf746",
    "workspaces": ["678429b2-501d-4b07-ad51-cf594a3876ae"]
  },
  "workspaceId": "678429b2-501d-4b07-ad51-cf594a3876ae",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
}
```

#### Response

```text
200 OK
```

```json
{
  "id": "a3634ae0-c337-44eb-b380-2df0530c59f3",
  "url": "https://www.eskimoz.co.uk",
  "category": "HOMEPAGE",
  "frequency": "MONTHLY",
  "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
  "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
  "error": false,
  "performance": 98,
  "lastUpdate": "2024-07-21T12:50:21.674Z",
  "diff": -0.010204081632652962,
  "success": true
}
```

> [!NOTE]
> Only the `category` and `frequency` can be updated.

### Delete a route

```text
DELETE /routes/:id
```

```json
{
  "user": {
    "id": "468be21d-5a9a-48c9-a46d-307e474bf746",
    "workspaces": ["678429b2-501d-4b07-ad51-cf594a3876ae"]
  },
  "workspaceId": "678429b2-501d-4b07-ad51-cf594a3876ae",
}
```

#### Response

```text
204 No content
```

### List the routes

```text
GET /routes
```

```json
{
  "user": {
    "id": "468be21d-5a9a-48c9-a46d-307e474bf746",
    "workspaces": ["678429b2-501d-4b07-ad51-cf594a3876ae"]
  },
  "workspaceId": "678429b2-501d-4b07-ad51-cf594a3876ae",
}
```

#### Response

```text
200 OK
```

```json
{
  "data": [
    {
      "id": "618fd521-e613-4fc1-aefd-94b6248440ec",
      "url": "https://www.eskimoz.it",
      "category": "HOMEPAGE",
      "frequency": "ONE_TIME",
      "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
      "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
      "error": false,
      "performance": 100,
      "lastUpdate": "2024-07-21T12:33:48.434Z",
      "diff": 0,
      "success": true
    },
    {
      "id": "b6a88cb5-5263-49db-827a-2584828efee0",
      "url": "https://www.eskimoz.fr",
      "category": "HOMEPAGE",
      "frequency": "ONE_TIME",
      "userId": "db9ad4ac-a247-47a7-a403-47ecdaf4a107",
      "workspaceId": "af74be70-895e-447c-8c37-d3ff46482c49",
      "error": false,
      "performance": 97,
      "lastUpdate": "2024-07-21T12:34:01.938Z",
      "diff": 0,
      "success": true
    }
  ],
  "count": 2,
  "total": 2,
  "page": 1,
  "pageCount": 1
}
```
