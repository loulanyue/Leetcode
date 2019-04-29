## 给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

## 示例 1:

        输入: num1 = "2", num2 = "3"
        输出: "6"
        示例 2:

        输入: num1 = "123", num2 = "456"
        输出: "56088"
        说明：

        num1 和 num2 的长度小于110。
        num1 和 num2 只包含数字 0-9。
        num1 和 num2 均不以零开头，除非是数字 0 本身。
        不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。


>>

        class Solution {
            public String multiply(String num1, String num2) {
                char[] value = new char[num1.length() + num2.length()];
                for (int i = num1.length() - 1; i >= 0; i--) {
                    for (int j = num2.length() - 1; j >= 0; j--) {
                        value[i + j + 1] += (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                    }
                }
                // 处理进位
                int carry = 0;
                for (int i = value.length - 1; i >= 0; i--) {
                    value[i] += carry;
                    carry = value[i] / 10;
                    value[i] %= 10;
                }
                int beginIndex = 0;
                while (beginIndex < value.length - 1 && value[beginIndex] == 0) {
                    beginIndex++;
                }
                for (int i = beginIndex; i < value.length; i++) {
                    value[i] += '0';
                }
                return new String(value, beginIndex, value.length - beginIndex);
            }
        }
