# 15、leetcode859. 亲密字符串
解法一：
--  
思路：
--
    如果满足亲密字符串，条件是：①、A == B（aaa与aaa，abc与abc） : A 中至少有2个重复元素。②、A != B (ab与ba,abc与bca): AB中只能有2对不同索引 (元素互换相等)。注意：判断是否有重复时，使用set或数组++。
代码： 
--
<pre>
package com.lihe.leetcode.string;

import java.util.HashSet;
import java.util.Set;

/**
 * @author lihe
 * @date 2019/10/21 21:05
 * @descriptor
 */
public class BuddyStrings_859 {
    public static boolean buddyStrings(String A, String B) {
       if(A.length() != B.length())
           return false;
       //A 中至少有2个重复元素才能返回true
       if(A.equals(B)){//aaa aaa || abc abc
            int[] ch = new int[26];
           for (int i = 0; i < A.length(); i++) {
               ch[A.charAt(i) - 'a']++;
           }
           for (int i:ch) {
               if(i > 1)return true;
           }
           return false;
       }else{
            int i = -1,j = -1;
           for (int k = 0; k < A.length(); k++) {
               if(A.charAt(k) != B.charAt(k)){
                   if(i == -1)
                       i = k;
                   else if(j == -1)
                       j = k;
                   else
                       return false;
               }
           }
           return (j != -1) && A.charAt(i) == B.charAt(j) && A.charAt(j) == B.charAt(i);
       }
    }
    public static boolean buddyStrings1(String A, String B) {
        if(A.length() != B.length())
            return false;
        //A 中至少有2个重复元素才能返回true
        if(A.equals(B)){//aaa aaa || abc abc
           Set<Character> set = new HashSet<>();
            for (int i = 0; i < A.length(); i++) {
                if(!set.contains(A.charAt(i)))
                    set.add(A.charAt(i));
                else
                    return true;
            }
            return false;
        }else {
            int i = -1, j = -1;
            for (int k = 0; k < A.length(); k++) {
                if (A.charAt(k) != B.charAt(k)) {
                    if (i == -1)
                        i = k;
                    else if (j == -1)
                        j = k;
                    else
                        return false;
                }
            }
            return (j != -1) && A.charAt(i) == B.charAt(j) && A.charAt(j) == B.charAt(i);
        }
    }
    public static void main(String[] args) {
        String A = "ab", B = "ba";
        boolean b = buddyStrings(A, B);
        System.out.println(b);
    }
}
</pre>
