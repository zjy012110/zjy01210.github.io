---
title: JS踩坑笔记
---

# JS踩坑笔记  

## 小数精度处理  

> 对于数值小数精度的处理，JS提供了方法toFied()，但在实际的运用中，发现他并不是标准的四舍五入的规则，比如：  

```  
>let cont = 417.025
>cont.toFixed(2)
<"417.02"
```      

> 所得到的结果并不是我们所想要的417.03   

### 方法一：  

重写toFixed()方法    

### 方法二：    

自己写一个小数位处理方法，全局可以调用    

 <!--more-->


```  
  /***
  * 小数位保留函数
  * @num  需要保留的数值 417.025
  * @fix 保留小数位 2
  * @return 417.03
  * **/
  formatNum (num, fix) {
    // num为原数字，fix是保留的小数位数
    if (num === null || num === undefined || num === '') {
      return
    }
    let result = '0'
    if (Number(num) && fix > 0) { // 简单的做个判断
      fix = +fix || 2
      num = num + ''
      if (/e/.test(num)) { // 如果是包含e字符的数字直接返回
        result = num
      } else if (!/\./.test(num)) { // 如果没有小数点
        result = num + `.${Array(fix + 1).join('0')}`
      } else { // 如果有小数点
        num = num + `${Array(fix + 1).join('0')}`
        let reg = new RegExp(`-?\\d*\\.\\d{0,${fix}}`)
        let floorStr = reg.exec(num)[0]
        if (+floorStr >= +num) {
          result = floorStr
        } else {
          let floorNumber = +floorStr + +`0.${Array(fix).join('0')}1`
          let point = /\./.test(floorNumber + '') ? '' : '.'
          let floorStr2 = floorNumber + point + `${Array(fix + 1).join('0')}`
          result = reg.exec(floorStr2)[0]
        }
      }
    }
    return result
  }
```  
