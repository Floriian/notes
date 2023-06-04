## Create new app (best boilerplate I think)

```bash
yarn create next-app <project-name> --typescript --eslint --experimental-app --src-dir
```

## <a href="#supabase"></a>Supabase
All inside pages/api. I don't know the perfect option.
Should install "encoding" package as devdependency.
<hr>
### Create Supabase Client
```typescript
import { createClient } from "@supabase/supabase-js";

export default createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);

```
### Supabase + Next.JS 13 get one file's public URL from bucket
```typescript
import type { NextApiRequest, NextApiResponse } from "next";
import supabase from "../../utils/supabase";
export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  const { data } = await supabase.storage
    .from(BUCKETNAME)
    .getPublicUrl("folder/pathtofile");
  res.status(200).json({
    data,
  });
}

```

### Supabase + Next.JS13 get all file's public URL from bucket
I don't know better option...

```typescript
import type { NextApiResponse, NextApiRequest } from "next";
import supabase from "../../utils/supabase";

export default async function handler(
  req: NextApiResponse,
  res: NextApiResponse
) {
  let images: Array<unknown> = [];
  let imageUrls: Array<unknown> = [];

  const imageData = await supabase.storage
    .from(BUCKETNAME)
    .list(FOLDER)
    .then((res) => {
      res.data?.map(async (d) => {
        const { data } = await supabase.storage
          .from(BUCKETNAME)
          .getPublicUrl(`FOLDER/${d.name}`);

        imageUrls.push(data);
      });
    });

  return res.status(200).json({ imageUrls });
}

```