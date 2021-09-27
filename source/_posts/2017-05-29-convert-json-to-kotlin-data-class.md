title: JSON 转换为 Kotlin Data Class 工具
tags: [Kotlin, Java, JSON]
categories: 编程
author: DemoJameson
date: 2017-05-29 16:13:00 
updated:  2017-05-19 16:13:00 
---

{% asset_img cover.png %}

在 Kotlin 中数据类（Data Class）能帮我们减少许多样板代码，自动生成 `equals`/`hashCode`/`toString` 等很多必要的方法。与后端通讯时流行的 JSON 数据十分适合用数据类来存储，如果有个工具能自动将 JSON 转化为数据类就好了。所以退化到只会用原生 Javascript DOM 的我就写了这个工具，没有花太多精力只做了点微小的工作（+1s）。

<!--more-->

# JSON to Data Class 工具

<textarea style="margin: 10px; width: 600px; height: 300px;" id="json" title="JSON" placeholder="JSON"></textarea>
<textarea style="margin: 10px; width: 600px; height: 300px;" id='dataclass' title="Data Class" placeholder="Kotlin Data Class"></textarea>
<input id="convert" type="button" value="转换" onclick="convertJson2DataClass()"/>
<script type="text/ecmascript">
  function convert(parseObj, className, level) {
    var result = '';
    className = className ? capitalizeFirstLetter(className) + 'Bean' : 'DataClass';
    level = level || 1;
    var indent = "";
    var i = 0;
    while (i < level) {
      indent += "  ";
      i++;
    }
    
    if (Array.isArray(parseObj)) {
    
    } else if (typeof parseObj === 'object') {
      var innerClassArr = [];
      result += '\ndata class ' + className + '(';
      for (var prop in parseObj) {
        var obj = parseObj[prop];
        var typeStr = getType(obj, prop);
        if (Array.isArray(obj) && obj.length > 0) {
          obj = obj[0];
          while (Array.isArray(obj) && obj.length > 0) {
            obj = obj[0];
          }
          if (!Array.isArray(obj) && typeof obj === 'object') {
            innerClassArr.push({'obj': obj, 'prop': prop});
          }
        } else if (typeof obj === 'object' && obj != undefined) {
          innerClassArr.push({'obj': obj, 'prop': prop});
        }
        var modifier = typeStr === 'Any?' ? 'var' : 'val';
        result += modifier + ' ' + prop + ': ' + typeStr + ',\n';
      }
      result = result.slice(0, -2) + ')';
    
      if (innerClassArr.length > 0) {
        result += ' {';
        innerClassArr.forEach(function (data) {
          result += "\n" + indent + convert(data.obj, data.prop, ++level);
        });
        result += '\n' + indent.slice(2) + '}';
      }
    }
    
    return result;
  }

  function getType(obj, prop) {
    var typeStr = '';
    var typeofResult = typeof obj;
    
    if (Array.isArray(obj)) {
      if (obj.length > 0) {
        typeStr = 'List<' + getType(obj[0], prop) + '>';
      } else {
        typeStr = 'List<Any?>';
      }
    } else if (typeofResult === 'object') {
      if (obj != undefined) {
        typeStr = capitalizeFirstLetter(prop) + 'Bean';
      } else {
        typeStr = "Any?"
      }
    } else if (typeofResult === 'string') {
      typeStr = "String";
    } else if (typeofResult === 'boolean') {
      typeStr = "Boolean";
    } else if (typeofResult === 'number') {
      if (obj.toString().indexOf('.') !== -1) {
        typeStr = "Double";
      } else {
        typeStr = "Int";
      }
    }
    return typeStr;
  }

  function convertJson2DataClass() {
    var jsonText = document.querySelector('#json').value;
    if (!jsonText) {
      alert("请先输入 JSON 数据");
      return;
    }
    
    try {
      var parseObj = JSON.parse(jsonText);
    } catch(e) {
      alert("JSON 数据转换异常，请先校验数据是否合法");
      return;
    }
    
    var dataClassText = convert(parseObj).slice(1);
    document.querySelector('#dataclass').value = dataClassText;
  }

  function capitalizeFirstLetter(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }
</script>