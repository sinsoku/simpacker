# Simpacker react example

## Install simpacker

See https://github.com/hokaccha/simpacker#installation

## Install react and react-dom

```
$ npm install --save react react-dom
$ npm install --save-dev @types/react @types/react-dom
```

## Change the `webpack.config.js`

```diff
   entry: {
-    application: path.resolve(__dirname, "app/javascript/application.ts")
+    application: path.resolve(__dirname, "app/javascript/application.tsx")
   },
   output: {
     path: path.resolve(__dirname, "public/packs"),
@@ -17,7 +17,7 @@
     chunkFilename: "[id]-[chunkhash].js"
   },
   resolve: {
-    extensions: [".js", ".ts"]
+    extensions: [".js", ".ts", ".jsx", ".tsx"]
   },
   module: {
     rules: [
```

## Change the `tsconfig.json`

```diff
     "target": "es5",
     "lib": ["es2019", "dom", "dom.iterable"],
     "module": "es2015",
+    "jsx": "react",
     "moduleResolution": "node",
     "esModuleInterop": true,
     "downlevelIteration": true,
```

## Rename and change scripts

```
$ mv app/javascript/application.{ts,tsx}
$ mv app/javascript/greeter.{ts,tsx}
```

### app/javascript/packs/application.tsx

```typescript
import React from "react";
import ReactDOM from "react-dom";
import { Hello } from "./greeter";

document.addEventListener("DOMContentLoaded", () => {
  ReactDOM.render(<Hello name="Rails" />, document.getElementById("app"));
});

```

### app/javascript/src/greeter.tsx

```typescript
import React, { FC } from "react";

interface Props {
  name: string;
}

export const Hello: FC<Props> = ({ name }) => {
  return <div>Hello {name}!</div>;
};
```

## Run

```
$ npx webpack
```

It works!