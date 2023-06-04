```typescript
const splittedArray: Array<ObjectType>[] =

    images.reduce((acc, curr, i) => {

      const index = Math.floor(i / 3);

      acc[index] = acc[index] || [];

      acc[index].push(curr);

      return acc;

    }, []);
```