#### 身份证号校验函数
```javascript
const idcardValidate = idcard => {
  // 长度如果不为18位，不合法
  if (!/\d{17}[\dX]/gi.test(idcard)) {
    return false
  }
  // 身份证前11位，分隔为数组
  const idNum = idcard.toString().slice(0, -1).split('')
  // 身份证最后一位效验码
  const validationCode = idcard.slice(-1)
  // 系数
  const coefficient = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2]
  // 身份证前11位分别×系数对应的位数，再求和，最后除以11，取余
  const remainder = idNum.map((num, index) => num * coefficient[index]).reduce((pre, current) => pre + current, 0) % 11
  // 余数对应的最后一位效验码
  const remainderHook = { 0: '1', 1: '0', 2: 'X', 3: '9', 4: '8', 5: '7', 6: '6', 7: '5', 8: '4', 9: '3', 10: '2' }
  // 如果不匹配，则格式错误
  if (remainderHook[remainder] !== validationCode.toString().toUpperCase()) {
    return false
  }
  return true
}
```
