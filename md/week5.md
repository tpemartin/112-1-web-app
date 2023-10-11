
# Goals 

[![](../img/officeInfo.png) ](https://www.figma.com/file/79Qn6m4sEy7CE8Z30OS80h/lecture-notes?type=design&node-id=17-19&mode=design&t=GFFJkKeslmAAz6Kt-4)


  - [Full time faculty](https://econ.ntpu.edu.tw/en/teachers/5)


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
        <Stack direction="column" spacing={2}>
            <Typography variant="h6">
                {title}
            </Typography>
            <Typography variant="body1">
                {content}
            </Typography>
        </Stack>
    )
}
```

## Stacking adjustment

To fine tune the style of the component, we can use the browser's developer tool.

- Run `npm run dev` to see the live view of your app. 

- Right click on the component and select "Inspect" to open the developer tool.

![](../img/stacking%20adjustment.png)

- element selected will be highlighted in the browser.  
- "Styles" tab shows the CSS rules applied to the element.

### Flex box

- MUI Stack component uses [flex box](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) to stack the items.   
- In chrome developer tool, flex box will be marked with a special icon as below.  

![](../img/display%20flex.png)

- `align-items: center;` centers the items vertically.

```jsx
<Stack direction="column" spacing={2}
 sx={{alignItems: "center"}}>
```

  * sx: style system in Material UI. Its a prop that allows us to pass in CSS rules as an object.
  * style name used to be in snake style needs to be in camel style. For example, `align-items` becomes `alignItems`.

> In js, an object is a collection of key-value pairs. For example, `{name: "John", age: 30}` is an object.
>

## Stacking further

![](../img/stacking%20further.png)

```jsx
function InfoOnDoor_fixedContent(){
    return (
        <Stack direction="column" spacing={2}>
            <InfoPanel_variableContent title="Office Hours" content="Thu. 12:00 - 14:00" />
            <InfoPanel_variableContent title="Email" content="guowc@gm.ntpu.edu.tw" />
            <InfoPanel_variableContent title="Phone" content="886-2-86741111#66100" />  
            <InfoPanel_variableContent title="Office" content="社科院 3F16" />
        </Stack>
    )
}
```

## Image panel stacking

![](../img/image%20panel.png)
  
  - `<img>` tag: <https://www.w3schools.com/tags/tag_img.asp>  
  - image link: <https://econ.ntpu.edu.tw/storage/images/ZlP7DHjLRh8IeahmFoT1EMxkmCgaxYtguN76FqiW.jpg>

```jsx
function ImagePanel_fixedContent() {
    return (
      <Stack direction="column" spacing={2}>
          <img src="https://econ.ntpu.edu.tw/storage/images/ZlP7DHjLRh8IeahmFoT1EMxkmCgaxYtguN76FqiW.jpg" 
          alt="image" width="100%" height="100%" />
          <Typography variant="h6">
              郭文宗 教授
          </Typography>
      </Stack>
    )
}

```

> Need to confine image within a certin size. We can use `Box` component to do that.

```jsx
function ImagePanel_fixedContent() {
    return (
        <Stack direction="column" spacing={2}>
            <Box sx={{ width: "200px", height: "100%" }}>
                <img src="https://econ.ntpu.edu.tw/storage/images/ZlP7DHjLRh8IeahmFoT1EMxkmCgaxYtguN76FqiW.jpg"
                    alt="image" width="100%" height="100%" />
            </Box>
            <Typography variant="h6">
                郭文宗 教授
            </Typography>
        </Stack>
    )
}
```

  - [height css](https://developer.mozilla.org/en-US/docs/Web/CSS/height)

## Final result

Module `index.jsx`

```jsx
import { Stack, Typography, Box } from "@mui/material";


export default function OfficeInformation({imgLink, name ,officeHour, email, phone, office}) {
    return (
        <>
          <Stack direction="row" spacing={2}>
            <ImagePanel_fixedContent imgLink={imgLink} name={name}/>
            <InfoPanel officeHour={officeHour} email={email}
                phone={phone}
                office={office}/>
          </Stack>
        </>
      )
}


 function ImagePanel_fixedContent({imgLink, name}) {
    return (
        <Stack direction="column" spacing={2}>
            <Box sx={{ width: "200px", height: "100%" }}>
                <img src={imgLink}
                    alt="image" width="100%" />
            </Box>
            <Typography variant="h6">
                {name} 教授
            </Typography>
        </Stack>
    )
}


 function InfoPanel({ officeHour, email, phone, office }) {
    return (
        <>
            <Stack direction="column" spacing={2}>
                <InfoPanel_variableContent title="Office Hours" content={officeHour} />
                <InfoPanel_variableContent title="Email" content={email} />
                <InfoPanel_variableContent title="Phone" content={phone} />
                <InfoPanel_variableContent title="Office" content={office} />
            </Stack>
        </>
    )
}
 function InfoPanel_variableContent({ title, content }) {
    return (
        <Stack direction="column" spacing={2}>
            <Typography variant="h6">
                {title}
            </Typography>
            <Typography variant="body1">
                {content}
            </Typography>
        </Stack>
    )
}

```

`App.jsx`

```jsx
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
import OfficeInformation from './components/OfficeInformation'
function App() {
  
  return (
  <>
   <OfficeInformation
      imgLink="https://econ.ntpu.edu.tw/storage/images/ZlP7DHjLRh8IeahmFoT1EMxkmCgaxYtguN76FqiW.jpg"
      name = "郭文宗 教授"
      officeHour="Thu. 12:00 - 14:00"
      email="guowc@gm.ntpu.edu.tw"
      phone="886-2-86741111 ext. 67156"
      office="社3F16"          
                />
  </>
  )
}

export default App


```