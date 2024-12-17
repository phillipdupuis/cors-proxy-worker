# cors-proxy-worker

`worker.js` file for a CORS Proxy

https://developers.cloudflare.com/workers/

## Usage

```ts
interface FetchViaProxyOptions {
  proxy?: string;
  responseHeaders?: Record<string, string>;
}

function fetchViaProxy(
  url: string,
  {
    proxy = "https://your-cloudflare-worker.dev/corsproxy/",
    responseHeaders,
  }: FetchViaProxyOptions = {}
) {
  const proxyURL = new URL(proxy);
  proxyURL.searchParams.set("url", encodeURIComponent(url));
  if (responseHeaders && Object.keys(responseHeaders).length > 0) {
    proxyURL.searchParams.set(
      "responseHeaders",
      encodeURIComponent(JSON.stringify(responseHeaders))
    );
  }
  return fetch(proxyURL);
}
```
