# Exercise

Javascript Exercise List

1. 实现两个大数相加：
 实现思路如下：
 
   1）分别将数据格式化为小数部分和整数部分
   2）采用补全方式，将两个相加数的整数部分和小数部分补全为相同长度的字符串
   3）将字符串拆分为数组，然后对数组进行遍历相加，分别计算出小数部分结果和整数部分结果
   
   具体实现方法 ：
   
   class LongNumberComputer {

  // 分别将数据格式化为小数部分和整数部分
  // 采用补全方式，将两个相加数的整数部分和小数部分补全为相同长度的字符串
  // 将字符串拆分为数组，然后对数组进行遍历相加，分别计算出小数部分结果和整数部分结果
  addUp(preNumber, currentNumber) {
    let preObject = this.parseStrToNumberObject(preNumber);
    let currentObject = this.parseStrToNumberObject(currentNumber);

    let objInt = this.formatDiff(preObject.strInt, currentObject.strInt);
    let objFloat = this.formatDiff(preObject.strFloat, currentObject.strFloat, 'Float');

    let objFloatAddOn = this.addOnObj(objFloat);
    let objIntAddOn = this.addOnObj(objInt, objFloatAddOn.addOnInt);
    objIntAddOn.addOnInt && objIntAddOn.addOnResult.unshift(objIntAddOn.addOnInt.toString());
    return { resultInt: objIntAddOn.addOnResult.join(''), resultFloat: objFloatAddOn.addOnResult.join('') };
  }

  // 实现相加算法
  // objNumber 数组对象，包含需要计算的对象
  // preInt：进位数值，计算整数部分需要将小数相加结果的整数位设置
  addOnObj(objNumber, preInt = 0) {
    let numberResult = [];
    for (let i = objNumber.count; i > 0; i--) {
      let addResult = parseInt(objNumber.pre[i - 1]) + parseInt(objNumber.curr[i - 1]) + preInt;
      numberResult.unshift((addResult % 10).toString());
      preInt = parseInt(addResult / 10);
    }
    return { addOnResult: numberResult, addOnInt: preInt };
  }

  // 格式化小数部分和整数部分
  // 整数部分左补齐0，小数部分右补齐 0，返回对象，目的使两个数组长度一致
  // type:标识当前是格式化小数部分还是整数部分
  formatDiff(preStr, currStr, type = 'Int') {
    let diffLen = preStr.length - currStr.length;
    if (diffLen !== 0) {
      if (diffLen > 0) {
        currStr = `${type === 'Int' ? '' : currStr}${new Array(diffLen).fill('0').join('')}${type === 'Int' ? currStr : ''}`;
      } else {
        preStr = `${type === 'Int' ? '' : preStr}${new Array(-diffLen).fill('0').join('')}${type === 'Int' ? preStr : ''}`;
      }
    }
    return { pre: preStr.split(''), curr: currStr.split(''), count: preStr.length };
  }

  // 判断输入数据类型，格式化数据为String
  // 返回对象
  parseStrToNumberObject(strNumber) {
    if (typeof (strNumber) === 'number') {
      strNumber = strNumber.toString();
    }
    else if (typeof (strNumber) !== 'string') {
      throw new Error('Params Type Must Be Number Or String!');
    }

    let strInt = strNumber.indexOf('.') && strNumber.substring(0, strNumber.indexOf('.')) || strNumber;
    let strFloat = strNumber.indexOf('.') && strNumber.split('.')[1] || '0';

    return {
      strInt: strInt,
      strFloat: strFloat
    };
  }
}
