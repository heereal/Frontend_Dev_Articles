# Route Handlers
> [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)

<br/>

```javascript
// app/products/api/route.ts
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
  })
  const data = await res.json()
 
  return Response.json({ data })
}
```

- `Route Handler`를 사용하면 Web Request 및 Response API를 사용하여 지정된 경로에 대한 사용자 지정 요청 핸들러를 만들 수 있다.
- `Route Handler`는 `app` 디렉토리의 `route.js` 파일에서 정의된다.
- `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, `OPTIONS` 등의 HTTP 메서드를 제공한다.
- 확장된 `NextRequest`, `NextResponse` API를 제공한다. 
