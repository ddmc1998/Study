# BigDecimal转换

> 获取精度，小数位数

* 精度为整数部分和小数部分总长度（200.12精度为5）

```java
BigDecimal bigDecimal = BigDecimal.valueOf(200.12);

//5
System.out.println("精度：" + bigDecimal.precision());

//2
System.out.println("小数位数：" + bigDecimal.scale());
```

> 保留指定位数

```java
package com.util;

import org.springframework.util.StringUtils;

import java.math.BigDecimal;

/**
 * 计算工具类
 */
public class CalcUtil {

    /**
     * @param value 值
     * @param scale 保留小数位数
     * @return
     */
    public static BigDecimal calc(Object value, int scale) {
        BigDecimal result = parse(value).setScale(scale, BigDecimal.ROUND_HALF_UP);
        return result;
    }

    /**
     *  保留指定位数小数，去除小数后面的0
     * @param value 值
     * @param scale 保留小数位数
     * @return
     */
    public static BigDecimal calcDisplayZero(Object value, int scale) {
        BigDecimal result = parse(value).setScale(scale, BigDecimal.ROUND_HALF_UP);;
        return result.stripTrailingZeros();
    }

    /**
     *  转换为BigDecimal
     * @param value
     * @param <T>
     * @return
     */
    private static <T> BigDecimal parse(T value) {
        BigDecimal result;
        if (value instanceof String) {
            if (!StringUtils.hasText((String) value)) {
                return BigDecimal.ZERO;
            }
            result = new BigDecimal((String) value);
        } else if (value instanceof Integer) {
            result = BigDecimal.valueOf((Integer) value);
        } else if (value instanceof Double) {
            result = BigDecimal.valueOf((Double) value);
        } else if (value instanceof Float) {
            result = BigDecimal.valueOf((Float) value);
        } else if (value instanceof Long) {
            result = BigDecimal.valueOf((Long) value);
        } else {
            result = BigDecimal.ZERO;
        }
        return result;
    }
}
```

## 去除小数末尾0，可能导致科学计数法，用toPlainString()解决

> stripTrailingZeros()去除0
> toPlainString() 输出为字符，防止科学计数

```java
stripTrailingZeros().toPlainString()
```

