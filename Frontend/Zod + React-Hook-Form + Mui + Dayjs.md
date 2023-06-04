
```typescript
import { Controller, useForm } from 'react-hook-form';
...
  const {

    register,

    handleSubmit,

    formState: { errors },

    control,

  } = useForm<Type>({

    resolver: zodResolver(Schema),

  });
  ...
 <Controller

              name="deadline"

              control={control}

              rules={{ required: true }}

              defaultValue={today}

              render={({ field }) => (

                <DatePicker

                  {...field}

                  slotProps={{

                    textField: {

                      error: errors.deadline ? true : false,

                      helperText: errors.deadline?.message,

                    },

                  }}

                />

              )}

            />
```

Validation schema:
```typescript
import { z } from "zod";
import dayjs, { Dayjs } from "dayjs";

export const Schema = z.object({

  deadline: z.custom<Dayjs>((data) => {

    const date = dayjs(data as unknown as Date);

    return dayjs().isBefore(date);

  }, 'Date must be future date.'),
});
```