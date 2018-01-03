# rollup

[rollup](https://rollupjs.org)��һ����������ߣ���ҪΪ�˽�� `tree-shaking`��

# ��װ
```
npm install rollup --global
```


# ����

�½����� `main.js` �� `foo.js`

```javascript
// src/main.js
import foo from './foo.js';
export default function () {
  console.log(foo);
}
```


```javascript
// src/foo.js
export default 'hello world!';
```


���������������� 

```
rollup src/main.js -f cjs
```

��ֱ�����������̨��

```
src/main.js �� stdout...
'use strict';

// src/foo.js
var foo = 'hello world!';

// src/main.js
function main () {
  console.log(foo);
}

module.exports = main;
created stdout in 32ms
```


����ʹ�� `rollup src/main.js -o bundle.js -f cjs` ������ļ� `bundle.js` ��


# ʹ�������ļ�

Ĭ�������ļ�Ϊ `rollup.config.js` , ʹ�� `rollup -c` ���� `rollup --config` ���С�

```
// rollup.config.js
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
};
```

���ﻹ���Է���һ�����飬�磺

```javascript
export default [{
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
},{
  input: 'src/main.js',
  output: {
    file: 'bundle2.js',
    format: 'cjs'
  }
}];
```

���Ӻõ�ϰ���ǰѿ������������������ֿ����á��� `rollup.config.dev.js` �� `rollup.config.pro.js`��Ȼ��ʹ�� `rollup --config rollup.config.dev.js` ���С�


# ��es6����������ҳ�����ļ�

��Ҫʹ�� `umd` ���� `iife` ��ʽ���Ƽ�ʹ�� `umd` ��ʽ����ʱ��Ҫ�ƶ� `name` ���������ģ�����֣��� `Xiao`��

```
export default [{
  input: 'src/main-babel.js',
  output: {
    file: 'dist/bundle-babel.js',
    format: 'umd',
    name: 'Xiao'
  },
  plugins: [ 
    resolve(),
    babel({
      exclude: 'node_modules/**' // only transpile our source code
    })
  ]
}];
```

package.json

```json
{
  "name": "component-rollup",
  "version": "1.0.0",
  "description": "rollup demo",
  "main": "bundle-babel.js",
  "dependencies": {},
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-plugin-external-helpers": "^6.22.0",
    "babel-preset-env": "^1.6.1",
    "babel-preset-es2015-rollup": "^3.0.0",
    "rollup-plugin-babel": "^3.0.3",
    "rollup-plugin-node-resolve": "^3.0.0"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "rollup -c rollup.config.dev.js"
  },
  "keywords": [],
  "author": "xwjie",
  "license": "ISC"
}

```

���� `npm run build` ����