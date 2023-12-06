# StringUtils工具类
该类是 JDK 提供的 String 类型操作方法的补充，并且是null安全(如果输入参数为 null 则不会抛出 NullPointException)和线程安全的。

## 常用方法

### 判断

#### 判空

* **isBlank**(final CharSequence cs)：判断是否为`空白字符串`，`null`、`""`、`" "`等没有实际内容的都属于空白字符串。
* **isNotBlank**(final CharSequence cs)：判断是否不为`空白字符串`。
* **isAllBlank**(final CharSequence... css)：判断多个cs是否为`空白字符串`。
* **isEmpty**(final CharSequence cs)：判断是否为`空白字符串`，`null`、`""`等没有实际内容的都属于空白字符串。
* **isNotEmpty**(final CharSequence cs)：判断是否不为`空白字符串`。
* **isAllEmpty**(final CharSequence... css)：判断多个cs是否为`空白字符串`。

#### 判断大小写

* *boolean* **isAllUpperCase**(*final* *CharSequence* cs)：校验字符串是否为大写。
* *boolean* **isAllLowerCase**(*final* *CharSequence* cs)：校验字符串是否为小写。

```java
StringUtils.isAllUpperCase("ABC");//---true
StringUtils.isAllLowerCase("abC");//---false
```

#### 判断字符串数字

* *boolean* **isNumeric**(*final* *CharSequence* cs)：校验字符串是否仅包含数字。
* *boolean* **isNumericSpace**(*final* *CharSequence* cs)：校验字符串是否仅包含数字或空格。

```java
StringUtils.isNumeric("123");  		//---true
StringUtils.isNumeric("12 3"); 		//---false
StringUtils.isNumericSpace("12 3"); //---true
StringUtils.isNumericSpace("  "); 	//---true
StringUtils.isNumericSpace(""); 	//---true
```





### 比较

#### 相等比较

* **equals**(final CharSequence cs1, final CharSequence cs2)：比较两个字符串是否相等。
* **equalsIgnoreCase**(final CharSequence cs1, final CharSequence cs2)：比较两个字符串是否相等，忽略大小写。
* **equalsAny**(final CharSequence string, final CharSequence... searchStrings)：指定多个对比的字符串，有一个与主字符串相等即可。
* **equalsAnyIgnoreCase**(final CharSequence string, final CharSequence...searchStrings)：指定多个对比的字符串，有一个与主字符串相等即可，并忽略大小写。

#### 包含比较

* *boolean* **contains**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq)：判断seq字符串是否包含searchSeq字符串。
* *boolean* **containsIgnoreCase**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq)：判断seq字符串是否包含searchSeq字符串。`忽略大小写`。
* *boolean* **containsAny**(*final* *CharSequence* seq, *final* *CharSequence*... searchCharSequences)：判断seq字符串是否包含searchCharSequences中的任一字符串。
* *boolean* **containsAnyIgnoreCase**(*final* *CharSequence* seq, *final* *CharSequence*... searchCharSequences)：判断seq字符串是否包含searchCharSequences中的任一字符串。`忽略大小写`。

#### 不包含比较

* *boolean* **containsNone**(*final* *CharSequence* seq, *final String* searchSeq)：判断seq字符串是否`不`包含searchSeq字符串。

#### 包含空格

* *boolean* **containsWhitespace**(*final* *CharSequence* seq)：判断seq字符串是否包含任一`空格`。包含则返回true。

#### 大小比较

* *int* **compare**(*final* String str1, *final* String str2)：根据`String.compareTo(String)`来比较两个字符串的大小。
  * =0：说明str1等于str2，或者str1、str2都为空。
  * <0：说明str1小于str2。
  * \>0：说明str1大于str2。
* *int* **compare**(*final* String str1, *final* String str2)：根据`String.compareTo(String)`来比较两个字符串的大小。`忽略大小写`。

* *int* **compare**(*final* String str1, *final* String str2, *final boolean* nullIsLess)：根据`String.compareTo(String)`来比较两个字符串的大小。`nullIsLess`可以指定null和非空字符大小优先级。
  * nullIsLess=true：则 null < "a"。
  * nullIsLess=false：则 null \> "a"。
* *int* **compareIgnoreCase**(*final* String str1, *final* String str2, *final boolean* nullIsLess)：`忽略大小写`。

#### 比较不同

* String **difference**(*final* String str1, *final* String str2)：比较两字符串，返回不同之处。确切地说是返回第二个参数中与第一个参数所不同的字符串。

  ``` java
  StringUtils.difference("abcde", "abxyz");//---"xyz"
  ```

#### 前缀比较

* *boolean* **startsWith**(*final* *CharSequence* str, *final* *CharSequence* prefix)：检查字符串是否以指定的前缀开头。
* *boolean* **startsWithAny**(*final* *CharSequence* sequence, *final* *CharSequence*... searchStrings)：检查字符串是否以指定「前缀数组」中的某一个开头。
* *boolean* **startsWithIgnoreCase**(*final* *CharSequence* str, *final* *CharSequence* prefix)：检查字符串是否以指定的前缀开头。忽略大小写。

``` java
StringUtils.startsWith("abcdef", "abc");//---true
StringUtils.startsWithIgnoreCase("ABCDEF", "abc");//---true
StringUtils.startsWithAny("abcxyz", new String[] {null, "xyz", "abc"});//---true
```

* String **getCommonPrefix**(*final* String... strs)：获取多个字符串共同的前缀。

  ```java
  StringUtils.getCommonPrefix(new String[] {"abcde", "abxyz"}) //---"ab"
  ```

  

#### 后缀比较

* *boolean* **endsWith**(*final* *CharSequence* str, *final* *CharSequence* suffix)：校验字符串是否以制定的后缀结尾。
* *boolean* **endsWithAny**(*final* *CharSequence* sequence, *final* *CharSequence*... searchStrings)：检查字符串是否以指定「后缀数组」中的某一个开头。
* *boolean* **endsWithIgnoreCase**(*final* *CharSequence* str, *final* *CharSequence* suffix)：校验字符串是否以制定的后缀结尾。忽略大小写。

```java
StringUtils.endsWith("abcdef", "def");//---true
StringUtils.endsWithIgnoreCase("ABCDEF", "def");//---true
StringUtils.endsWithAny("abcxyz", new String[] {null, "xyz", "abc"});//---true
```



### 截取

* String **substring**(*final* String str, *int* start)：截取字符串。从start开始截取到末尾。

  * start如果为负数，则从后往前截取start个字符

    ```java
    StringUtils.substring("abc", 2);  //---"c"
    StringUtils.substring("abc", -2); //---"bc"
    ```

* String **substring**(*final* String str, *int* start, *int* end)：截取字符串。从start开始，截取end个字符。

  ```java
  StringUtils.substring("abc", 2, 4); //---"c"
  ```

* String **substringBetween**(*final* String str, *final* String tag)：获取两个`相同tag`字符串之间的内容。
* String **substringBetween**(*final* String str, *final* String open, *final* String close)：获取两个`不同tag`字符串之间的内容。
* String[] **substringsBetween**(*final* String str, *final* String open, *final* String close)：获取`多个不同tag`字符串之间的内容。

```java
StringUtils.substringBetween("*abc*", "*");  //---"abc"
StringUtils.substringBetween("${username}", "${", "}"); //---"username"
StringUtils.substringsBetween("${username}${password}", "${", "}"); //---["username", "password"]
```

* String **left**(*final* String str, *final int* len)：从左开始截取n个字符。
* String **right**(*final* String str, *final int* len)：从右开始截取n个字符。

```java
StringUtils.left("abc", 2);//---"ab"
StringUtils.right("abc", 2);//---"bc"
```





### 分割

* String[] **split**(*final* String str, *final* String separatorChars)：使用指定的分隔符对字符串进行分割。



### 连接join

注意：该方法的实现是以StringBuilder的方式来进行字符串拼接的，线程不安全，多线程环境下不建议使用。

* **join**(final `byte/short/int/long/float/double/char/boolean/String/Object`[] array, final `char/String` delimiter)：使用指定的分隔符，拼接数组中的内容。
* **join**(final `byte/short/int/long/float/double/char/boolean/String/Object`[] array, final `char/String` delimiter, final int startIndex, final int endIndex)：使用指定的分隔符，拼接数组中的内容。并指定数组中数据的使用范围
* **join**(*final* *List*<?> list, *final* String separator, *final int* startIndex, *final int* endIndex)：使用指定的分隔符，拼接`集合`中的内容。
* **join**(*final* T... elements)：拼接所提供的元素elements，默认没有分隔符。例如  `StringUtils.join(["a", "b", "c"]) = "abc"`。
* **joinWith**(*final* String delimiter, *final* Object... array)：使用指定的分隔符，拼接数组中的内容。





### 查找字符

#### 正向查找

* *int* **indexOf**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq)：正向查找字符在字符串中第一次出现的位置。
* *int* **indexOf**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq, *final int* startPos)：正向查找字符在字符串中第一次出现的位置，从`指定下标`位置开始查找。
* *int* **indexOfAny**(*final* *CharSequence* str, *final* *CharSequence*... searchStrs)：正向查找`字符串数组中任一字符`在字符串中第一次出现的位置。
* *int* **ordinalIndexOf**(*final* *CharSequence* str, *final* *CharSequence* searchStr, *final int* ordinal)：正向查找字符在字符串中第N次出现的位置。

```java
StringUtils.indexOf("aabaabaa", "b"); // 2
StringUtils.indexOf("aabaabaa", "b", 3); //5(从角标3后查找)
StringUtils.ordinalIndexOf("aabaabaa", "b", 1);// 2(查找第n次出现的位置)
StringUtils.ordinalIndexOf("aabaabaa", "b", 2);// 5(查找第n次出现的位置)
```



#### 反向查找

* *int* **lastIndexOf**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq)：反向查找字符在字符串中第一次出现的位置。
* *int* **lastIndexOf**(*final* *CharSequence* seq, *final* *CharSequence* searchSeq, *final int* startPos)：反向查找字符在字符串中第一次出现的位置，从`指定下标`位置开始查找。
* *int* **lastIndexOfAny**(*final* *CharSequence* str, *final* *CharSequence*... searchStrs)：反向查找`字符串数组中任一字符`在字符串中第一次出现的位置。
* *int* **lastOrdinalIndexOf**(*final* *CharSequence* str, *final* *CharSequence* searchStr, *final int* ordinal)：反向查找字符在字符串中第N次出现的位置。

```java
StringUtils.indexOf("aabaabaa", "b"); // 5
StringUtils.indexOf("aabaabaa", "b", 3); //2 (查找角标范围0-3)
StringUtils.indexOf("aabaabaa", "b", 6); //5 (查找角标范围0-6)
StringUtils.lastOrdinalIndexOf("aabaabaa", "b", 1); // 5
StringUtils.lastOrdinalIndexOf("aabaabaa", "b", 2); // 2
```



### 替换字符

* String **replace**(*final* String text, *final* String searchString, *final* String replacement)：替换字符串内容。
* String **replace**(*final* String text, *final* String searchString, *final* String replacement, *final int* max)：替换字符串内容，并限制最大替换次数。
* String **replaceAll**(*final* String text, *final* String regex, *final* String replacement)：使用正则表达式批量替换字符串。`虽然该方法已被重构到RegExUtils类中，但是为了方便记忆和使用，仍然使用StringUtils中的`。

```java
StringUtils.replace("aba", "a", "z"); // "zbz"
StringUtils.replace("abaa", "a", "z", 2); // "zbza"
StringUtils.replaceAll("ABCabc123", "[a-z]", "_"); // "ABC___123"
```

* String **overlay**(*final* String str, String overlay, *int* start, *int* end)：使用字符串A替换指定范围内的字符串B。

  ```java
  StringUtils.overlay("abcdef", "zzzz", 2, 4); // "abzzzzef"
  ```

  

### 删除字符

#### 删除字符串中的所有空格

* String **deleteWhitespace**(*final* String str)：删除字符串中的所有空格

  ```java
  StringUtils.deleteWhitespace("   ab  c  "); // "abc"
  ```

#### 删除某个字符

* String **remove**(*final* String str, *final* String remove)：从字符串中删除某段字符。

  ```java
  StringUtils.remove("queued", "ue"); // "qd"
  ```



### 大小写转换

#### 全部大小写转换

* String **upperCase**(*final* String str)：将字符串转换为大写。
* String **lowerCase**(*final* String str)：将字符串转换为小写。



#### 首字母大小写转换

* String **capitalize**(*final* String str)：首字母大写。

* String **uncapitalize**(*final* String str)：首字母小写。

```java
StringUtils.capitalize("cat");//---"Cat"
StringUtils.uncapitalize("Cat");//---"cat"
```



#### 大小写反转

* String **swapCase**(*final* String str)：把字符串中的大小变小写，小写变大写。

  ```java
  StringUtils.swapCase("The dog has a BONE");//---"tHE DOG HAS A bone"
  ```

  



### 重复字符

* String **repeat**(*final* String str, *final int* repeat)：将一个字符串重复N次形成一个新字符串。

  ```java
  StringUtils.repeat("a", 3); // "aaa"
  ```



### 反转字符串

* String **reverse**(*final* String str)：将一个字符串反转并生成一个新字符串。

  ```java
  StringUtils.reverse("bat"); // "tab"
  ```



### 统计字符

* *int* **countMatches**(*final* *CharSequence* str, *final* *CharSequence* sub)：统计字符串A在字符串B中的出现次数

  ```java
  StringUtils.countMatches("abba", "a"); // 2
  StringUtils.countMatches("abba", "ab"); // 1
  StringUtils.countMatches("abba", "x"); // 0
  ```

  



### 去除换行字符(\r\n\t)

* String **chomp**(*final* String str)：去除换行字符 "\n", "\r", "\r\n"。

  ```java
  StringUtils.chomp("abc \r"); //---"abc "
  StringUtils.chomp("abc\n"); //---"abc"
  StringUtils.chomp("abc\r\n"); //---"abc"
  ```

  

### 缩减字符串...

* String **abbreviate**(*final* String str, *final int* maxWidth)：缩短到某长度,用...结尾.其实就是(substring(str, 0, max-3) + "...")

  ```java
  StringUtils.abbreviate("abcdefg", 6);//---"abc..."
  StringUtils.abbreviate("abcdefg", 4);//---"a..."
  ```

  

### 提取字符

#### 提取字符串中的数字

* String **getDigits**(*final* String str)：提取字符串中的数字并返回一个新字符串。

  ```java
  StringUtils.getDigits("(541) 754-3010"); // "5417543010"
  ```

  

### 旋转字符

* String **rotate**(*final* String str, *final int* shift)：将一个字符串旋转指定的位移。

  ```java
  StringUtils.rotate("abcdefg", 2); // "fgabcde"
  StringUtils.rotate("abcdefg", -2);// "cdefgba"
  ```

  * 利用该方法可以实现一个打印旋转字符圆圈的小游戏

    ```java
        /**
         * 旋转字符
         * @param str 原始字符
         * @param count 旋转次数
         */
        public static void circleChar(final String str, final int count) {
            String temp = str;
            int i = count;
            while (i > 0) {
                temp = StringUtils.rotate(temp, 1);
                System.out.println(temp);
                i--;
            }
        }
    ```

    







> 参考资料
>
> [Java中的StringUtils引入及使用](https://blog.csdn.net/weixin_48903815/article/details/123107338)













