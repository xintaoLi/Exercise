# Exercise

Javascript Exercise List

1. 实现两个大数相加：
 实现思路如下：
 
   1）分别将数据格式化为小数部分和整数部分
   
    // 判断输入数据类型，格式化数据为String
    // 返回对象
    <code>
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
    </code>
   
   2）采用补全方式，将两个相加数的整数部分和小数部分补全为相同长度的字符串
   3）将字符串拆分为数组，然后对数组进行遍历相加，分别计算出小数部分结果和整数部分结果
   
  
