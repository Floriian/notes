
## Node FETCH API with Typescript
```typescript
export function publicFetch<T>(url: string): Promise<T> {

  return fetch(`http://localhost:3000/api${url}`)

    .then((r) => {

      if (!r.ok) {

        throw new Error(r.statusText);

      }

      return r.json() as Promise<{ data: T }>;

    })

    .then((data) => {

      return data.data;

    });

}
```
### Usage:
``` typescript
const data = publicFetch<T>("/endpoint")
```