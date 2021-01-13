---
description: 让渡居笔试题
> published_at: 2021.01.11
> updated_at: 2021.01.11

---

# RUNDO

## Front End

### Coding

- Input: "6*3+(4/2)-3*2"
- Output: 14

```python
# https://stackoverflow.com/questions/2371436/evaluating-a-mathematical-expression-in-a-string

import ast
import operator as op

# supported operators
operators = {ast.Add: op.add, ast.Sub: op.sub, ast.Mult: op.mul,
             ast.Div: op.truediv, ast.Pow: op.pow, ast.BitXor: op.xor,
             ast.USub: op.neg}

def eval_expr(expr):
    """
    >>> eval_expr('2^6')
    4
    >>> eval_expr('2**6')
    64
    >>> eval_expr('1 + 2*3**(4^5) / (6 + -7)')
    -5.0
    """
    return eval_(ast.parse(expr, mode='eval').body)

def eval_(node):
    if isinstance(node, ast.Num): # <number>
        return node.n
    elif isinstance(node, ast.BinOp): # <left> <operator> <right>
        return operators[type(node.op)](eval_(node.left), eval_(node.right))
    elif isinstance(node, ast.UnaryOp): # <operator> <operand> e.g., -1
        return operators[type(node.op)](eval_(node.operand))
    else:
        raise TypeError(node)
```

### Open

- git merge和git rebase的区别
  - git merge：将两个分支，合并提交为一个新提交，并且新提交有2个parent。
  - git rebase：会取消分支中的每个提交，并把他们临时存放，然后把当前分支更新到最新的origin分支，最后再把所有提交应用到分支上。
- 如何找到在特定提交中已更改的文件列表
  - 方案1：git diff-tree -r {hash}，给定提交哈希值，这个命令将列出在该提交中更改或添加的所有文件。-r 标志会让命令列出各个文件，而不是仅将它们折叠到根目录名称中。
  - 方案2：输出还将包含一些额外信息，可以通过以下两个标志轻松去掉：git diff-tree -no-commit-id -name-only -r {hash}，这里 -no-commit-id 将禁止提交哈希值出现在输出中，而 -name-only 只会打印文件名而不是它们的路径。
- 如何恢复已经推送并公开的提交的过程
  - 方案1：在新提交中删除或修复错误文件，并将其推送到远程存储库。这是修复错误最自然的方式。对文件进行必要的更改后，将其提交到远程存储库，使用命令：git commit -m“commit message”　　　　　　
  - 方案2：创建一个新的提交，撤消在错误提交中所做的所有更改，使用命令：git revert
- 对原生js感觉如何?
  - 优点： 
    - 性能高——由于JavaScript运行在客户端，节省了web服务器的请求时间和带宽轻量级的脚本语言，运行结果和处理相对比较快。
    - 针对性强——代码完全由自己的业务决定，不会产生多余的代码。
  - 缺点：
    - 安全性差——由于JavaScript在客户端运行，可能被黑客利用;
    - 兼容性差、扩展能力低——在不同浏览器中的处理结果可能不同，代码抽象的层次较低。


### Option

- 以下代码输出什么

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function() { alert(i); }, 1000 + i);
}
```

- 以下代码输出什么

```js
(function() {
  var a = b = 5;
})();
console.log(a);
console.log(b);
```

## BackEnd

### Coding

#### Simple Password

- Write following code in `js`

```python
import re

def SimplePassword(strParam):

  # code goes here
  while True:
    if (len(strParam) <= 7) or (len(strParam) >= 31):
      return False
    elif "password" in strParam.lower():
      return False
    elif not re.search("[A-Z]", strParam):
      return False
    elif not re.search("[0-9]", strParam):
      return False
    elif not re.search("[^a-zA-Z0-9]", strParam):
      return False
  return True
```

```js

```

### WildCard

A string seperated by space, first part contains `+`, `*`, or `{number}`,
- `+`: exactly one alphabeta
- `*`: exactly 3 alphabeta, unless followed by `{number}`

- Input: "+++++**{2} abcdemmmrr"
- Output: true

```js
import re

const inputStr = "+++++**{2} abcdemmmrr"
const strings = inputStr.split(' ')
const wildCard = strings[0]
const myStr    = strings[1]

const regPlus = new RegExp("[a-z]{1}")
const regAste = new RegExp("[a-z]{3}")

let i = 0;
let j = 0;
while (i <= wildCard.length) {
  if (wildCard[i] === "+") {

    if ( !regPlus.test(myStr[j]) ) return false
    else {
      // console.log(myStr[j])
      i = i + 1;
      j = j + 1;
    }

  } else if (wildCard[i] === "*") {
    if (wildCard[i + 1] === "{") {

      const numStr = wildCard.slice(i+2, wildCard.indexOf('}', i+2))
      const num = parseInt(numStr)
      const retAstN = new RegExp(`[a-z]{${num}}`)

      if ( !retAstN.test(myStr.slice(j, j+num)) ) return false
      else {
        // console.log(myStr.slice(j, j+num))
        i = i + 2 + numStr.length
        j = j + num
      }

    } else {

      if ( !regAste.test(myStr.slice(j, j+3)) ) return false
      else {
        // console.log(myStr.slice(j, j+3))
        i = i + 1;
        j = j + 3;
      }

    }
  }
}

if ( !myStr.slice(j, myStr.length) === 0 ) return false
else return true
```

### API and Data Retrieving

Retrieve data from <https://coderbyte.com/api/challenges/json/age-counting>, 
count ages equal to or older than 50.

```js
const https = require('https');
https.get('https://coderbyte.com/api/challenges/json/age-counting', (resp) => {
  let data = '';
  resp.on('data', (chunk) => { data += chunk; });
  resp.on('end',  () => {
    data = (JSON.parse(data).data).split(', ');
    const ages = data.filter((age, i) => i % 2 == 1).map(age => parseInt(age.slice(4, age.length)));
    const agesOlderThan50 = ages.filter(age => age >= 50);
    const numOfOlderThan50 =  agesOlderThan50.length;
    console.log(numOfOlderThan50);
  });
}); 
```
