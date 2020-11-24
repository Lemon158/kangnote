#### 1、数据表字典内容转换

##### 1.1、如图所示

![](https://i.bmp.ovh/imgs/2020/10/476e8cf5a9f4d6e9.png)

##### 1.2、获取字典信息

![](https://i.bmp.ovh/imgs/2020/10/e86b14bc726672b7.png)

##### 1.3、比对数据进行回显

```javascript
// 回显数据字典  some函数
export function selectDictLabel(datas, value) {
	var actions = [];
	Object.keys(datas).some((key) => {
		if (datas[key].dictValue == ('' + value)) {
			actions.push(datas[key].dictLabel);
			return true;
		}
	})
	return actions.join('');
}
```

#### 2、时间格式

##### 2.1、方法

```javascript
const parseTime = function(time) {
    const values = (time || '').split(':');
    if (values.length >= 2) {
      const hours = parseInt(values[0], 10);
      const minutes = parseInt(values[1], 10);

      return {
        hours,
        minutes
      };
    }
    /* istanbul ignore next */
    return null;
  };

//使用方法
parseTime(scope.row.createTime, '{y}-{m}-{d}')

```

