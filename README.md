# Framer X Cookbook
This is a list of short and useful Framer X tips to build impressive prototypes.

<br/>

- [How to share data between components using override?](#how-to-detect-if-a-component-has-children-nodes)
- [How to detect if a component has children nodes?](#how-to-detect-if-a-component-has-children-nodes)
- [How to import JSON files with data?](#how-to-import-json-files-with-data)
- [How to use a design component structure inside your code component?](#how-to-use-a-design-component-structure-inside-your-code-component)
- [How to wrap an installed component with your code component?](#how-to-wrap-a-installed-component-with-your-code-component)
- [How to use REST API inside a code component?](#how-to-use-rest-api-inside-a-code-component)
- [How to use GraphQL API inside a code component?](#how-to-use-graphql-api-inside-a-code-component)
- [How to install an npm package?](#how-to-install-an-npm-package)

<br/>

#### How to share data between components using override?
```js
import { Data, Override } from "framer"

const data = Data({
    text: "Overview",
})

export const TextChange: Override = props => {
    return {
        onValueChange: (text: string) => {
            data.text = text
        }
    }
}

export const GetText: Override = el => {
    let page = 0
    
    if (data.text == "Overview") page = 1
    if (data.text == "Interaction") page = 2

    return {
        page: page,
    }
}

```

#### How to detect if a component has children nodes?
```js
const hasChildren = (children: React.ReactNode) =>
  !!React.Children.count(children);
```

#### How to import JSON files with data?
```js
// Add the follow code in tsconfig.json file
"compilerOptions": {
  ...
  "resolveJsonModule:" true
}
```
#### How to use a design component structure inside your code component?
```js
  import { componentName } from './canvas'; 
```
#### How to wrap a installed component with your code component
```js
import { Component } from '@framer/componentname/code/File.js'

static defaultProps = { 
  ...Component.defaultProps,
}

// Reuse the propertyControls from the imported component
static propertyControls: PropertyControls = { 
  ...Component.propertyControls,
} 

render() { 
  return <Component {...this.props}>
}
```
#### How to use REST API inside a code component:
```js
loadData = async () => {
  const url = "http://url"
  const result = await fetch(url)
  const result = await result.json()
  this.setState({ result })
}

componentDidMount = () => { 
  this.loadData();
};
```
#### How to use GraphQL api inside a code component:
```js
import { request } from 'graphql-request'

loadData = async () => {
  const url = "http://url"
  const query =`
  {
    query { 
      fields
    }	
  }
  `
  const result = await request(url, query)
  this.setState({ result })
}

componentDidMount = () => { 
  this.loadData();
};
```
#### How to install a npm package

1. File > Show Project Folder
2. Open the path in terminal and install the the package
