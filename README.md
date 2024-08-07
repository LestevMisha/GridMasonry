## Option Parameters


### `breakpointColumns`

> [!NOTE]  
> We recommend to use `min-width` for all the queries.

> [!IMPORTANT]  
> Ensure `breakpointColumnsMax` parameter is set to `true` if using <ins>*max-width*</ins> and `false` if using <ins>*min-width*</ins> queries.

- **Type:** `object`
- **Default:**
```json
{
    "min-width: 1500px": 6,
    "min-width: 1200px": 5,
    "min-width: 992px": 4,
    "min-width: 768px": 3,
    "min-width: 576px": 2,
    "min-width: 0px": 1
}
```
- **Description:** Defines the number of columns for various breakpoints.
- **Behaviour:** If `responsive` parameter is `false` - `breakpointColumns` is disabled.
You can still use `max-width` there's 2 cases you can use it and 1 case you may use it. First - you can use it to have a structure similar to this: 
```javascript
const gridMasonry = new GridMasonry(".element", {
   breakpointColumns: {
        "min-width: 1200px": 4,
        "min-width: 800px": 3,
        "min-width: 600px": 2,
        "min-width: 400px": 1,
        "max-width: 399px": 3, // max-width
    }
});
```
in this case it doesn't make any sense to set max-width on 399px, since you could simply define `defaultColumnAmount` and it would use it on the scope without query. Second - if you want to use max-width instead of min-width everywhere, the structure may look like this:
```javascript
const gridMasonry = new GridMasonry(".element", {
   breakpointColumns: {
        "max-width: 1200px": 4,
        "max-width: 800px": 3,
        "max-width: 600px": 2,
        "max-width: 400px": 1,
    }
});
```
it will not work as you expect it to work. If you will dive deeply into the library, you will know why. You have to set `breakpointColumnsMax` parameter to `true`, it will make sure that max-width is handeled properly. What actually happens under the hood, is that this parameter just reverses the `breakpointColumns` so itteration starts from the least to the highest.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
   breakpointColumns: {
        "min-width: 1200px": 4,
        "min-width: 800px": 3,
        "min-width: 600px": 2,
        "min-width: 400px": 1
    }
});
```
In this example, window that has width in between 0-400px will have 1 column, 400-600px will have 2 columns, 600-800px will have 3 columns, 800-1200px will have 4 columns, anything greater than 1200px will have the `defaultColumnAmount`. **If needed interactive demo [here](https://..).**


### `defaultColumnAmount`

- **Type:** `number`
- **Default:** `1`
- **Description:** Sets the default number of columns. This method is effective only if there are no `breakpointColumns` (media queries) that match. 
- **Behaviour:** If `breakpointColumns` has `min-width: 0px` - `defaultColumnAmount` won't be used, since any window width will match the query.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 2,
});
```
In this example, any window width that is less than 1500px will have 2 columns, since there's no `breakpointColumns` query that would match. **If needed interactive demo [here](https://..).**


### `responsive`

- **Type:** `boolean`
- **Default:** `true`
- **Description:** If `responsive` is `true`, `breakpointColumns` will be used to determine how many columns a grid should have at a given responsive breakpoint.
- **Behaviour:** It's usually set to `false` when no responsiveness is needed, relaying just on the `defaultColumnAmount` parameter.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
});
```
In this example, `responsive` parameter is set to `false`, therefore `breakpointColumns` parameter is disabled, since resposive layout enables the use of the breakpoints. On any window size gridMasonry will have 5 columns. **If needed interactive demo [here](https://..).**


### `unit`

> [!IMPORTANT]  
> `unit` will affect `gap`, `marginTop` and `marginBottom`.

- **Type:** `string`
- **Default:** `em`
- **Description:** Can be `em` or `px`. It sets a unit value for the numeric parameters related to css styling. 
- **Behaviour:** -
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
    gap: 8,
    unit: "px",
});
```
In this example, `unit` parameter is set to `px`, so the gap in this example will have the size of 8px. **If needed interactive demo [here](https://..).**


### `gap`

> [!IMPORTANT]  
> `gap` will depend heavily on `unit` parameter (check it, before using).

- **Type:** `number`
- **Default:** `1`
- **Description:** Sets a gap in between the elements.
- **Behaviour:** Depends on the `unit` parameter, by default will have gap of 1em.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
    gap: 8,
});
```
In this example, `gap` parameter is set to `8`, so gap will be 8em since no `unit` parameter is defined. **If needed interactive demo [here](https://..).**


### `marginTop`

> [!IMPORTANT]  
> `marginTop` will depend heavily on `unit` parameter (check it, before using).

- **Type:** `number`
- **Default:** `0`
- **Description:** Sets margin-top for each element in the GridMasonry.
- **Behaviour:** Depends on the `unit` parameter.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
    gap: 8,
    unit: "px",
    marginTop: 16,
});
```
In this example, `marginTop` parameter is set to `16`, so each child of GridMasonry will have margin-top equaled to 16px. **If needed interactive demo [here](https://..).**


### `marginBottom`

> [!IMPORTANT]  
> `marginBottom` will depend heavily on `unit` parameter (check it, before using).

- **Type:** `number`
- **Default:** `0`
- **Description:** Sets margin-bottom for each element in the GridMasonry.
- **Behaviour:** Depends on the `unit` parameter.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
    gap: 8,
    unit: "px",
    marginTop: 16,
    marginBottom: 32,
});
```
In this example, `marginBottom` parameter is set to `32`, so each child of GridMasonry will have margin-bottom equaled to 32px. **If needed interactive demo [here](https://..).**


### `logQuery`

- **Type:** `boolean`
- **Default:** `false`
- **Description:** Logs breakpoints into developer console.
- **Behaviour:** Each time breakpoint is triggered will logged.
- **Example:**
```javascript
const gridMasonry = new GridMasonry(".element", {
    breakpointColumns: {
        "min-width: 1500px": 4,
    },
    defaultColumnAmount: 5,
     // breakpointColumns will be ignored
    responsive: false,
    gap: 8,
    unit: "px",
    marginTop: 16,
    marginBottom: 32,
    logQuery: true,
});
```
In this example, `logQuery` parameter is set to `true`, so each breakpoint will be logged into console (open console and see). **If needed interactive demo [here](https://..).**