## 思维导航

* [前言](https://github.com)
* [正则表达式的优势](https://github.com)
* [注意事项](https://github.com)
* [常用元字符](https://github.com)
* [验证邮箱地址](https://github.com)
* [验证手机号码](https://github.com)
* [提取URL](https://github.com)
* [替换文本](https://github.com)
* [分割字符串](https://github.com)
* [C\#正则性能提升技巧](https://github.com)
* [在线正则表达式大全](https://github.com)
* [DotNetGuide技术社区](https://github.com)

:[悠兔机场](https://xinnongbo.com)## 前言


正则表达式（Regular Expression）是一个强大的文本处理工具，主要用于字符串的搜索、替换、验证和分割等操作。通过定义特定的模式，正则表达式可以高效地匹配、查找或替换符合该模式的文本内容。今天大姚将和大家一起来快速了解学习正则表达式，并且在C\#中快速应用。


## 正则表达式的优势


与传统方法相比，正则表达式在处理字符串时具有以下显著优势：


* 灵活性：正则表达式提供了极高的灵活性，能够匹配复杂的文本模式。
* 高效性：对于大量的文本数据，正则表达式提供了一种快速筛选和处理的方法。
* 广泛应用：几乎所有的编程语言都支持正则表达式，使得它在跨平台应用中非常有用。


## 注意事项


* 正则表达式虽然强大，但是在处理复杂模式或大数据量时可能会比较耗时。因此，在性能敏感的场合要谨慎使用。
* 复杂的正则表达式可能难以理解和维护。建议在使用时添加必要的注释，并尽量将复杂的模式拆分成多个简单的部分。


## 常用元字符


元字符是正则表达式中具有特殊意义的字符，以下是一些常用的元字符及其作用：


* `.` : 匹配除换行符外的任何单个字符。
* `-` ：定义一个范围（例如\[A\-Z]）。
* `^` : 匹配字符串的开始。
* `$` : 匹配字符串的结束。
* `*` : 匹配前面的子表达式零次或多次。
* `+` : 匹配前面的子表达式一次或多次。
* `?` : 匹配前面的子表达式零次或一次。
* `[]` : 匹配括号内的任意一个字符。
* `|` : 匹配左右任意一个表达式（或操作）。
* `\` : 将下一个字符标记为一个特殊字符、或一个原义字符、或一个 向后引用、或一个八进制转义符。


## 验证邮箱地址



```
        /// 
        /// 验证邮箱地址
        /// 
        public static void VerifyEmailAddress()
        {
            string email = "edwin.doe@qq.com";
            string pattern = @"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$";
            var regex = new Regex(pattern);
            bool isValid = regex.IsMatch(email);
            Console.WriteLine($"{email} is valid email address: {isValid}");
        }

```

## 验证手机号码



```
        /// 
        /// 验证手机号码
        /// 
        public static void VerifyMobilePhone()
        {
            string mobile = "13812345678";
            string pattern = @"^1[3-9]\d{9}$";
            var regex = new Regex(pattern);
            bool isValid = regex.IsMatch(mobile);
            Console.WriteLine($"{mobile} is valid mobile phone number: {isValid}");
        }

```

## 提取URL



```
        /// 
        /// 提取URL
        /// 
        public static void ExtractUrl()
        {
            string url = "https://github.com/YSGStudyHards/DotNetGuide";
            string pattern = @"^https?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\(\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+$";
            var regex = new Regex(pattern);
            Match match = regex.Match(url);
            if (match.Success)
            {
                Console.WriteLine($"Found URL: {match.Value}"); //Output：https://github.com/YSGStudyHards/DotNetGuide
            }
            else
            {
                Console.WriteLine("No URL found.");
            }
        }

```

## 替换文本



```
        /// 
        /// 替换文本
        /// 
        public static void ReplaceText()
        {
            string input = "The date is 2024/12/16.";
            string pattern = @"(\d{4})/(\d{2})/(\d{2})";
            string replacement = "$1-$2-$3";
            var regex = new Regex(pattern);
            string result = regex.Replace(input, replacement);
            Console.WriteLine(result);//Output:The date is 2024-12-16.
        }

```

## 分割字符串



```
        /// 
        /// 分割字符串
        /// 
        public static void SplitString()
        {
            string pattern = @"[;,]";
            string input = "apple;banana,orange;grape";
            var regex = new Regex(pattern);
            string[] substrings = regex.Split(input);
            foreach (string substring in substrings)
            {
                Console.WriteLine(substring);
                //Output:
                //apple
                //banana
                //orange
                //grape
            }
        }

```

## C\#正则性能提升技巧


### 使用编译选项


使用 RegexOptions.Compiled 选项可以提高正则表达式的执行性能。此选项会在运行时编译正则表达式，从而加快匹配速度。



```
string pattern = @"(\d{4})/(\d{2})/(\d{2})";
Regex regex = new Regex(pattern, RegexOptions.Compiled);  

```

### 避免过度回溯


复杂的正则表达式可能会导致大量的回溯，从而增加匹配时间。通过优化正则表达式，减少不必要的回溯，可以提高性能。例如，尽量避免使用过多的重复限定符（如 `*`, `+`, `?`），并使用非贪婪匹配（`*?`, `+?`, `??`）来减少回溯。



```
// 贪婪匹配  
string pattern = @"<.*>";  
  
// 非贪婪匹配  
string pattern = @"<.*?>";  

```

### 合理设置超时时间


为了防止正则表达式在极端情况下耗费过多的时间，可以设置匹配操作的超时时间。



```
string pattern = @"(\d{4})/(\d{2})/(\d{2})";
TimeSpan timeout = TimeSpan.FromSeconds(1); // 设置1秒的超时时间  
Regex regex = new Regex(pattern, RegexOptions.None, timeout);  

```

## 在线正则表达式大全


对于我们而言正则表达式用的不是很频繁，记一下等到用的时候又忘记了。所以我们主要了解一下常用元字符和基本用法，当遇到需要做正则表达式拼接的时候可以到网上查阅现有资料，这里大姚分享一个比较全面的在线正则表达式大全。


* [https://any\-rule.vercel.app](https://github.com)


![](https://img2024.cnblogs.com/blog/1336199/202412/1336199-20241215225840392-1566376618.png)


![](https://img2024.cnblogs.com/blog/1336199/202412/1336199-20241215225849594-1479926162.png)


![](https://img2024.cnblogs.com/blog/1336199/202412/1336199-20241215225857462-1830520628.png)


## DotNetGuide技术社区


* DotNetGuide技术社区是一个面向.NET开发者的开源技术社区，旨在为开发者们提供全面的C\#/.NET/.NET Core相关学习资料、技术分享和咨询、项目框架推荐、求职和招聘资讯、以及解决问题的平台。
* 在DotNetGuide技术社区中，开发者们可以分享自己的技术文章、项目经验、学习心得、遇到的疑难技术问题以及解决方案，并且还有机会结识志同道合的开发者。
* 我们致力于构建一个积极向上、和谐友善的.NET技术交流平台。无论您是初学者还是有丰富经验的开发者，我们都希望能为您提供更多的价值和成长机会。



> [**欢迎加入DotNetGuide技术社区微信交流群👪**](https://github.com)


