---
title: Commons Codec基本使用
author: kinglyq
date: 2019-05-23 15:35:51
---
> 在实际的应用中，我们经常需要对字符串进行编解码，Apache Commons家族中的Commons Codec就提供了一些公共的编解码实现，比如Base64, Hex, MD5,Phonetic and URLs等等。

<!--more-->

# Base64编解码
```java
private static String encodeTest(String str){
	Base64 base64 = new Base64();
	try {
		str = base64.encodeToString(str.getBytes("UTF-8"));
	} catch (UnsupportedEncodingException e) {
		e.printStackTrace();
	}
	System.out.println("Base64 编码后："+str);
	return str;

} 

private static void decodeTest(String str){
	Base64 base64 = new Base64();
	// str = Arrays.toString(Base64.decodeBase64(str));
	str = new String(Base64.decodeBase64(str));
	System.out.println("Base64 解码后："+str);
}
```

# Hex编解码
```java
private static String encodeHexTest(String str){
	try {
		str = Hex.encodeHexString(str.getBytes("UTF-8"));
	} catch (UnsupportedEncodingException e) {
		e.printStackTrace();
	}
	System.out.println("Hex 编码后："+str);	
	return str;
} 

private static String decodeHexTest(String str){
	Hex hex = new Hex();
	try {
		str = new String((byte[])hex.decode(str));
	} catch (DecoderException e) {
		e.printStackTrace();
	}
	System.out.println("Hex 编码后："+str);
	return str;

}
```

# MD5加密
```java
private static String MD5Test(String str){
	try {
		System.out.println("MD5 编码后："+newString(DigestUtils.md5Hex(str.getBytes("UTF-8"))));
	} catch (UnsupportedEncodingException e) {
		e.printStackTrace();
  	}
	return str;
}
```

# SHA编码
```java
private static String ShaTest(String str){
	try {
		System.out.println(“SHA 编码后：”+newString(DigestUtils.shaHex(str.getBytes("UTF-8"))));
	} catch (UnsupportedEncodingException e) {
		e.printStackTrace();
	}
	return str;
}
```

# Metaphone和Soundex

- 这个例子来源于网上，网址见：
http://350129923.blog.163.com/blog/static/17959113200763144659125/

- Metaphone 建立出相同的key给发音相似的单字, 比 Soundex 还要准确, 但是 Metaphone 没有固定长度, Soundex 则是固定第一个英文字加上3个数字. 这通常是用在类似音比对, 也可以用在 MP3 的软件开发.
```java
import org.apache.commons.codec.language.*;
import org.apache.commons.codec.*;

public class LanguageTest {

	public static void main(String args[]) {
		Metaphone metaphone = new Metaphone();
		RefinedSoundex refinedSoundex = new RefinedSoundex();
		Soundex soundex = new Soundex();

		for (int i = 0; i < 2; i++) {
			String str = (i == 0) ? "resume" : "resin";
			String mString = null;
			String rString = null;
			String sString = null;

			try {
				mString = metaphone.encode(str);
				rString = refinedSoundex.encode(str);
				sString = soundex.encode(str);

			} catch (Exception ex) {
				;
			}
			System.out.println("Original:" + str);
			System.out.println("Metaphone:" + mString);
			System.out.println("RefinedSoundex:" + rString);
			System.out.println("Soundex:" + sString + "\\n");

		}
	}

}
```