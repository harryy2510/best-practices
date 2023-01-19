# 📡 API Layer

### Use a single instance of the API client

Our application is consuming RESTful API. We have a single instance of the API client that's been pre-configured and reused throughout the application. Here is our [axios](https://github.com/axios/axios) instance with pre-defined configuration.

[API Client Code](../src/lib/axios.ts)

### API hooks declarations

We declare API requests on the go, as a fetcher function that calls an endpoint. They are named as queries and mutations that could be consumed by data fetching library, [react-query](https://react-query.tanstack.com/). We export corresponding API hooks from there.

[API Hook Declaration Example Code](../src/features/industry-insights/api/use-kpi.query.ts)
