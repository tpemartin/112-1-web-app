
# Goals 

[![](../img/officeInfo.png) ](https://www.figma.com/file/79Qn6m4sEy7CE8Z30OS80h/lecture-notes?type=design&node-id=17-19&mode=design&t=GFFJkKeslmAAz6Kt-4)

# Stacking (堆疊)

## One component

### specific info

[![](../img/specific%20info.png)](https://www.figma.com/file/79Qn6m4sEy7CE8Z30OS80h/lecture-notes?type=design&node-id=24-49&mode=design&t=GFFJkKeslmAAz6Kt-4)

```jsx
function InfoPanel_fixedContent() {
    return (
        <Stack direction="column" spacing={2}>
            <Typography variant="h6">
                Office Hours
            </Typography>
            <Typography variant="body1">
                Thu. 12:00 - 14:00
            </Typography>
        </Stack>
    )
}
```

### general info

[![](../img/general%20info.png)](https://www.figma.com/file/79Qn6m4sEy7CE8Z30OS80h/lecture-notes?type=design&node-id=24-50&mode=design&t=GFFJkKeslmAAz6Kt-4)

```jsx
function InfoPanel_variableContent({title, content}) {
    return (
        <Stack direction="column" spacing={2} sx={{alignItems: "center"}}>
            <Typography variant="h6">
                {title}
            </Typography>
            <Typography variant="body1">
                {content}
            </Typography>
        </Stack>
    )
}
``````

## Stacking adjustment

![](../img/stacking%20adjustment.png)

- element selected will be highlighted in the browser.  
- "Styles" tab shows the CSS rules applied to the element.

![](../img/display%20flex.png)

- `align-items: center;` centers the items vertically.

```jsx
<Stack direction="column" spacing={2}
 sx={{alignItems: "center"}}>
```

  * sx: style system in Material UI. Its a prop that allows us to pass in CSS rules as an object.

> In js, an object is a collection of key-value pairs. For example, `{name: "John", age: 30}` is an object.