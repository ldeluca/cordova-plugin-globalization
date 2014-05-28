<!---
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.
-->

# org.apache.cordova.globalization

这个插件获取的信息，并执行操作特定于用户的区域设置、 语言和时区。 注意到区域设置和语言之间的区别： 数字、 日期和时间的显示方式为一个区域，虽然语言确定什么语言文本的区域设置控件显示为，与区域设置无关。 开发人员经常使用的区域设置来设置这两个设置，但用户不能将她的语言设置为"英语"没有理由但区域设置为"法语"这样的文本显示在英语但日期、 时间等，同时会显示他们是在法国。 不幸的是，大多数移动平台目前不做这些设置之间的区别。

## 安装

    cordova plugin add org.apache.cordova.globalization
    

## 对象

*   GlobalizationError

## 方法

*   navigator.globalization.getPreferredLanguage
*   navigator.globalization.getLocaleName
*   navigator.globalization.dateToString
*   navigator.globalization.stringToDate
*   navigator.globalization.getDatePattern
*   navigator.globalization.getDateNames
*   navigator.globalization.isDayLightSavingsTime
*   navigator.globalization.getFirstDayOfWeek
*   navigator.globalization.numberToString
*   navigator.globalization.stringToNumber
*   navigator.globalization.getNumberPattern
*   navigator.globalization.getCurrencyPattern

## navigator.globalization.getPreferredLanguage

获取客户端的当前语言 BCP 47 语言标记。

    navigator.globalization.getPreferredLanguage(successCallback, errorCallback);
    

### 说明

返回的 BCP 47 兼容的语言标识符标记 `successCallback` 与 `properties` 对象作为参数。 对象应具有 `value` 属性与 `String` 的值。

如果有出错的语言，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.UNKNOWN_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en-US` 的语言，这应显示弹出式菜单对话框的文本与 `language: en-US` ：

    navigator.globalization.getPreferredLanguage(
        function (language) {alert('language: ' + language.value + '\n');},
        function () {alert('Error getting language\n');}
    );
    

### Android 的怪癖

*   返回的 ISO 639-1 双字母语言代码、 大写 ISO 3166-1 国家代码和由连字符分隔的变形。例子："en"、"EN-US"，"美国"

### Windows Phone 8 怪癖

*   返回 ISO 639-1 两个字母语言代码和相应的设置，由连字符分隔的"语言"区域变形的 ISO 3166-1 国家代码。
*   请注意的区域变体是的"语言"设置的属性，并不由 Windows Phone 上的无关的"国家/地区"设置决定的。

## navigator.globalization.getLocaleName

返回客户端的当前区域设置的 BCP 47 符合标记。

    navigator.globalization.getLocaleName(successCallback, errorCallback);
    

### 说明

返回到的 BCP 47 符合区域设置标识符字符串 `successCallback` 与 `properties` 对象作为参数。 对象应具有 `value` 属性与 `String` 的值。 Locale 标记将包括两个字母小写语言代码、 国家代码两个字母大写和 （未指定） 变量的代码，由连字符分隔。

如果有出错的区域设置，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.UNKNOWN_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en-US` 的区域设置，这将显示弹出式对话框中的文本`locale: en-US`.

    navigator.globalization.getLocaleName(
        function (locale) {alert('locale: ' + locale.value + '\n');},
        function () {alert('Error getting locale\n');}
    );
    

### Android 的怪癖

*   Java 不区分设置"语言"和设置的"区域设置"，所以这种方法基本上是相同`navigator.globalizatin.getPreferredLanguage()`.

### Windows Phone 8 怪癖

*   返回 ISO 639-1 两个字母语言代码和区域 variant 类型的值对应于"区域格式"设置，以连字符分隔的 ISO 3166-1 国家代码。

## navigator.globalization.dateToString

返回一个日期格式设置为一个字符串，根据客户端的区域设置和时区。

    navigator.globalization.dateToString(date, successCallback, errorCallback, options);
    

### 说明

返回格式化的日期 `String` 通过 `value` 属性可从该对象作为一个参数传递`successCallback`.

入站 `date` 参数的类型应为`Date`.

如果有错误格式日期，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.FORMATTING_ERROR`.

`options`参数是可选的且其默认值：

    {formatLength: '短'，选择器： 日期和时间}
    

`options.formatLength`可以是 `short` ， `medium` ， `long` ，或`full`.

`options.selector`可以是 `date` ， `time` 或`date and time`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

如果浏览器设置为 `en_US` 的区域设置，这将显示一个弹出对话框与类似的文本 `date: 9/25/2012 4:21PM` 使用默认选项：

    navigator.globalization.dateToString(
        new Date(),
        function (date) { alert('date: ' + date.value + '\n'); },
        function () { alert('Error getting dateString\n'); },
        { formatLength: 'short', selector: 'date and time' }
    );
    

### Windows Phone 8 怪癖

*   `formatLength`选项仅支持 `short` 和 `full` 的值。

## navigator.globalization.getCurrencyPattern

返回一个模式字符串格式化和分析根据客户端的用户首选项和 ISO 4217 货币代码货币值。

     navigator.globalization.getCurrencyPattern(currencyCode, successCallback, errorCallback);
    

### 说明

返回到模式 `successCallback` 与 `properties` 对象作为参数。该对象应包含以下属性：

*   **模式**： 要格式化和分析货币值的货币模式。 模式按照[Unicode 技术标准 #35][1]。 *（字符串）*

*   **代码**： 模式的 ISO 4217 货币代码。*（字符串）*

*   **分数**： 小数位数解析和货币的格式时要使用的数量。*（人数）*

*   **舍**： 舍递增时分析和格式设置使用。*（人数）*

*   **十进制**： 小数点符号用于分析和格式设置。*（字符串）*

*   **分组**： 分组符号用于分析和格式设置。*（字符串）*

 [1]: http://unicode.org/reports/tr35/tr35-4.html

入站 `currencyCode` 参数应该是 `String` 的 ISO 4217 货币代码，例如 '美元' 之一。

如果有错误获得该模式，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.FORMATTING_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS

### 示例

当浏览器设置为 `en_US` 区域设置和所选的币种是美元，本示例将显示一个弹出对话框与类似的结果，请按照操作的文本：

    navigator.globalization.getCurrencyPattern(
        'USD',
        function (pattern) {
            alert('pattern: '  + pattern.pattern  + '\n' +
                  'code: '     + pattern.code     + '\n' +
                  'fraction: ' + pattern.fraction + '\n' +
                  'rounding: ' + pattern.rounding + '\n' +
                  'decimal: '  + pattern.decimal  + '\n' +
                  'grouping: ' + pattern.grouping);
        },
        function () { alert('Error getting pattern\n'); }
    );
    

预期的结果：

    pattern: $#,##0.##;($#,##0.##)
    code: USD
    fraction: 2
    rounding: 0
    decimal: .
    grouping: ,
    

## navigator.globalization.getDateNames

返回一个数组的几个月的名称或一周内，根据客户端的用户首选项和日历天。

    navigator.globalization.getDateNames(successCallback, errorCallback, options);
    

### 说明

返回的数组的名称为 `successCallback` 与 `properties` 对象作为参数。 该对象包含 `value` 属性与 `Array` 的 `String` 的值。 从任一开始一年或一周内，根据所选的选项的第一天中的第一个月的数组功能名称。

如果有错误取得名字，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.UNKNOWN_ERROR`.

`options`参数是可选的且其默认值：

    {type:'wide', item:'months'}
    

值 `options.type` 可以是 `narrow` 或`wide`.

值 `options.item` 可以是 `months` 或`days`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，本示例显示一系列的十二个弹出对话框，每个月，与类似的文本一个 `month: January` ：

    navigator.globalization.getDateNames(
        function (names) {
            for (var i = 0; i < names.value.length; i++) {
                alert('month: ' + names.value[i] + '\n');
            }
        },
        function () { alert('Error getting names\n'); },
        { type: 'wide', item: 'months' }
    );
    

## navigator.globalization.getDatePattern

返回一个模式字符串格式化和解析日期根据客户端的用户首选项。

    navigator.globalization.getDatePattern(successCallback, errorCallback, options);
    

### 说明

返回到模式 `successCallback` 。作为一个参数传递的对象包含以下属性：

*   **模式**： 要格式化和解析日期的日期和时间模式。 模式按照[Unicode 技术标准 #35][1]。 *（字符串）*

*   **时区**： 在客户端上的时区的缩写的名称。*（字符串）*

*   **utc_offset**： 客户端的时区和协调通用时间当前区别秒。*（人数）*

*   **dst_offset**： 在客户端的夏之间的秒数的当前夏令时偏移量的时区和客户端的夏时制储蓄的时区。*（人数）*

如果您获取该模式，错误 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.PATTERN_ERROR`.

`options`参数是可选的并且默认为以下值：

    {formatLength: '短'，选择器： 日期和时间}
    

`options.formatLength`可以是 `short` ， `medium` ， `long` ，或 `full` 。 `options.selector`可以是 `date` ， `time` 或`date and
time`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，此示例显示弹出式对话框中的文本如 `pattern: M/d/yyyy h:mm a` ：

    function checkDatePattern() {
        navigator.globalization.getDatePattern(
            function (date) { alert('pattern: ' + date.pattern + '\n'); },
            function () { alert('Error getting pattern\n'); },
            { formatLength: 'short', selector: 'date and time' }
        );
    }
    

### Windows Phone 8 怪癖

*   `formatLength`仅支持 `short` 和 `full` 的值。

*   `pattern`的 `date and time` 模式返回只完整的日期时间格式。

*   `timezone`返回全时区名称。

*   `dst_offset`属性不受支持，并且总是返回零。

## navigator.globalization.getFirstDayOfWeek

返回客户端的用户首选项和日历星期的第一天。

    navigator.globalization.getFirstDayOfWeek(successCallback, errorCallback);
    

### 说明

周中天的编号 1，从开始位置 1 假定是星期日。 返回到天 `successCallback` 与 `properties` 对象作为参数。 对象应具有 `value` 属性与 `Number` 的值。

如果有错误获得该模式，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.UNKNOWN_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，这将显示一个弹出对话框与类似的文本`day: 1`.

    navigator.globalization.getFirstDayOfWeek(
        function (day) {alert('day: ' + day.value + '\n');},
        function () {alert('Error getting day\n');}
    );
    

## navigator.globalization.getNumberPattern

返回一个模式字符串格式化和分析数字根据客户端的用户首选项。

    navigator.globalization.getNumberPattern(successCallback, errorCallback, options);
    

### 说明

返回到模式 `successCallback` 与 `properties` 对象作为参数。该对象包含以下属性：

*   **模式**： 要格式化和分析数字的数字模式。 模式按照[Unicode 技术标准 #35][1]。 *（字符串）*

*   **符号**： 符号格式设置和分析过程中，如 %或货币符号时使用。*（字符串）*

*   **分数**： 小数位数解析和设置数字格式时要使用的数量。*（人数）*

*   **舍**： 舍递增时分析和格式设置使用。*（人数）*

*   **积极**： 积极数字分析和格式时要使用的符号。*（字符串）*

*   **负面**： 要为负数时分析和格式设置使用的符号。*（字符串）*

*   **十进制**： 小数点符号用于分析和格式设置。*（字符串）*

*   **分组**： 分组符号用于分析和格式设置。*（字符串）*

如果有错误获得该模式，然后 `errorCallback` 执行与 `GlobalizationError` 对象作为参数。 错误的期望的代码`GlobalizationError.PATTERN_ERROR`.

`options`参数是可选的并且默认值：

    {类型： '十进制'}
    

`options.type`可以是 `decimal` ， `percent` ，或`currency`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，此时应显示一个弹出对话框与类似的结果，请按照操作的文本：

    navigator.globalization.getNumberPattern(
        function (pattern) {alert('pattern: '  + pattern.pattern  + '\n' +
                                  'symbol: '   + pattern.symbol   + '\n' +
                                  'fraction: ' + pattern.fraction + '\n' +
                                  'rounding: ' + pattern.rounding + '\n' +
                                  'positive: ' + pattern.positive + '\n' +
                                  'negative: ' + pattern.negative + '\n' +
                                  'decimal: '  + pattern.decimal  + '\n' +
                                  'grouping: ' + pattern.grouping);},
        function () {alert('Error getting pattern\n');},
        {type:'decimal'}
    );
    

结果:

    pattern: #,##0.###
    symbol: .
    fraction: 0
    rounding: 0
    positive:
    negative: -
    decimal: .
    grouping: ,
    

### Windows Phone 8 怪癖

*   `pattern`不支持属性，和 retuens 为空字符串。

*   `fraction`不支持属性，并返回零。

## navigator.globalization.isDayLightSavingsTime

表示夏令时是否影响使用客户端的时区和日历给定的日期。

    navigator.globalization.isDayLightSavingsTime(date, successCallback, errorCallback);
    

### 说明

将 `successCallback` 与 `properties` 对象作为参数来表示非夏令时是否有效。 对象应具有 `dst` 属性与 `Boolean` 的值。 `true` 值表示夏令时对给定的日期是有效的，并且`false` 表示是无效的。

本国的参数 `date` 应该是`Date`类型.

如果有错误读取日期，然后 `errorCallback` 执行。错误的期望的代码`GlobalizationError.UNKNOWN_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

在夏季，如果浏览器被设置为启用 DST 时区，这应显示一个类似文本`dst: true`方式的弹出式对话框 ：

    navigator.globalization.isDayLightSavingsTime(
        new Date(),
        function (date) {alert('dst: ' + date.dst + '\n');},
        function () {alert('Error getting names\n');}
    );
    

## navigator.globalization.numberToString

根据客户端的用户首选项，作为一个字符串来返回一个数字格式。

    navigator.globalization.numberToString(number, successCallback, errorCallback, options);
    

### 说明

将 `successCallback` 与 `properties` 对象作为参数来返回带格式的数字字符串。 对象应具有 `value` 属性与 `String` 的值。

如果格式化数字有错误，那么`errorCallback`与 `GlobalizationError` 对象作为参数来执行回调。 错误的期望的代码`GlobalizationError.FORMATTING_ERROR`.

`options`参数是可选的且其默认值：

    {类型： '十进制'}
    

The `options.type`可以是 'decimal', 'percent', or 'currency'.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，这将显示一个弹出对话框与类似的文本 `number: 3.142` ：

    navigator.globalization.numberToString(
        3.1415926,
        function (number) {alert('number: ' + number.value + '\n');},
        function () {alert('Error getting number\n');},
        {type:'decimal'}
    );
    

## navigator.globalization.stringToDate

作为一个字符串来解析日期格式，根据使用客户端时区的客户端用户的首选项和日历，并返回对应的 date 对象。

    navigator.globalization.stringToDate(dateString, successCallback, errorCallback, options);
    

### 说明

与 `properties` 对象作为参数返回日期的成功回调。该对象应具有以下属性：

*   **一年**： 将四个数字的年份。*（人数）*

*   **月**： 从 （0-11) 月。*（人数）*

*   **一天**： 从 （1-31) 天。*（人数）*

*   **小时**： 从 (0-23) 小时。*（人数）*

*   **分钟**： 从 (0-59) 分钟。*（人数）*

*   **第二**： 的第二位 (0-59)。*（人数）*

*   **毫秒**： 的毫秒数 （从 0-999)，在所有平台上不可用。*（人数）*

本国的 `dateString` 参数应为`String`类型.

`options`参数是可选的，并且默认为以下值：

    {formatLength: '短'，选择器： 日期和时间}
    

`options.formatLength`可以是 `short` ， `medium` ， `long` ，或 `full` 。 `options.selector`可以是 `date` ， `time` 或`date and
time`.

如果解析日期字符串有错误，那么 `errorCallback`与 `GlobalizationError` 对象作为参数来执行。 错误的期望的代码`GlobalizationError.PARSING_ERROR`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，这将显示一个弹出对话框与类似的文本 `month:8 day:25 year:2012` 。 请注意，本月的整数是比该字符串要少一个的话，这个月的整数就代表数组索引。

    navigator.globalization.stringToDate(
        '9/25/2012',
        function (date) {alert('month:' + date.month +
                               ' day:'  + date.day   +
                               ' year:' + date.year  + '\n');},
        function () {alert('Error getting date\n');},
        {selector: 'date'}
    );
    

### Windows Phone 8 怪癖

*   `formatLength`选项仅支持 `short` 和 `full` 的值。

## navigator.globalization.stringToNumber

解析一个数字格式化为一个字符串，根据客户端的用户的喜好，并返回相应的编号。

    navigator.globalization.stringToNumber(string, successCallback, errorCallback, options);
    

### 说明

将`successCallback` 与 `properties` 对象作为参数来返回编号。对象应具有 `value` 属性与 `Number` 的值。

如果解析编号的字符串有错误，那么 `errorCallback`与 `GlobalizationError` 对象作为参数来执行回调。 错误的期望的代码`GlobalizationError.PARSING_ERROR`.

`options`参数是可选的并且默认为以下值：

    {类型： '十进制'}
    

`options.type`可以是 `decimal` ， `percent` ，或`currency`.

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS
*   Windows Phone 8

### 示例

当浏览器设置为 `en_US` 的区域设置，此时应显示与文本类似于弹出式对话框中 `number: 1234.56` ：

    navigator.globalization.stringToNumber(
        '1234.56',
        function (number) {alert('number: ' + number.value + '\n');},
        function () {alert('Error getting number\n');},
        {type:'decimal'}
    );
    

## GlobalizationError

从Globalization API中 表示一个错误的对象。

### 属性

*   **代码**： 表示错误类型的以下代码之一 *（人数）* 
    *   GlobalizationError.UNKNOWN_ERROR: 0
    *   GlobalizationError.FORMATTING_ERROR: 1
    *   GlobalizationError.PARSING_ERROR: 2
    *   GlobalizationError.PATTERN_ERROR: 3
*   **消息**： 一条文本消息，包括错误的解释，和/或详细说明*（字符串）*

### 说明

此对象被Cordova创建和填充，并在出现错误的情况下返回回调。

### 支持的平台

*   亚马逊火 OS
*   Android 系统
*   iOS

### 示例

以下错误回调执行时，它会显示类似于 `code: 3` 和`message:`文本的弹出对话框 

    function errorCallback(error) {
        alert('code: ' + error.code + '\n' +
              'message: ' + error.message + '\n');
    };