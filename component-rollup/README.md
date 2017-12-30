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


