An enhanced version of **react-router-v4 Route** Component that keeps route component alive on unmatched path and restore it completely on match path.

## Document

[中文](./docs/README-zh.md)

## Demo

### codeSandbox

You can experience and review the source code on codeSandbox.

[![Edit react-live-route-demo-1](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/yj9j33pw4j)

### QR code

You also can scan the QR code of the demo above to experience it on mobile device.

![qr](./docs/qr.png)

## Install

```bash
npm install react-live-route --save-dev
```

or

```bash
yarn add react-live-route --dev
```

## About

It will hide component of route instead of unmout it when the path is not match and restore it when come back. There are a few APIs provided to control the hidden condition of component.

Example：

There is a item list page, click on the items on this page will enter the item detail page. When entering the detail page, item list page will be hidden and it will keep hidden when you are on item detail page. Once back to the list page, the list page will be restored to the last state of leaving.

## Features

- ✅ Fully compatible with react-router-v4, all passed the react-router-v4 unit tests.
- 🎯 Completely restored to the state of the last time you left (scroll position included).
- 🔒 Minimally invasive, all you need to do is import LiveRoute.
- ✌️ Super easy API.

## Caveat ⚠️

- LiveRoute **SHOULD NOT** be wrapped by `Switch` directly, cause `Switch` only render the first matched child element so that LiveRoute may be skipped directly. You can move LiveRoute from `Switch` to the outside.
- If LiveRoute's parent route is unmounted on current location, then it will also be unmounted . This is determined by the top-down design principle of React. You can use LiveRoute to declares a parent route to solve this problem or stop nestting the router.

## Usage

### livePath

`livePath` is the path you want to hide the component instead of unmount it. The specific rules of `livePath` are the same as `path` props of Route in react-router-v4. You still can use `component` or `render` props to render a component. 

LiveRoute will re-render when it come back from a `path` matching location from the `livePath` matching location. It will unmount on other unmatched locations.

Example:

The route of List will be rendered normally under `/list`, and it will be hidden when location change to `/user/:id`, and it will be unmounted normally when entering  other locations.

```jsx
import LiveRoute from 'react-live-route'

<LiveRoute path="/list" livePath="/user/:id" component={List} />
```

### alwaysLive

`alwaysLive` is just like `livePath`. The difference is the component will not be unmount on **any other location** after the it's first mount. 

Example: 

After the first mount on match location, the Modal page will be hidden when the path is not matched, and will re-render when `path` match again.

```jsx
import LiveRoute from 'react-live-route'

<LiveRoute path="/list" alwaysLive={true} component={Modal}/>
```

## Licence

MIT
