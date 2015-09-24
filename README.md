# Replace-Java-Core-APIs
Let the JVM load your DIY class before the jars in JRE.
替换步骤如下：
1、编写程序入口类：
   |--文件名：Test.java
   |--内容：
/*****************代码开始***************/
public class Test{
	public static void main(String[] args) {
		System.out.println(new Integer(100));
	}
}
/*****************代码结束***************/

2、暂时删除修改后的API核心类，否则报错：
   |--报错内容：
/*****************报错开始***************/
Test.java:3: 无法访问 Integer
错误的类文件： .\Integer.java
文件不包含类 Integer
请删除该文件或确保该文件位于正确的类路径子目录中。
                System.out.println(new Integer(100));
/*****************报错开始***************/

3、shift+鼠标右键打开命令行编译程序入口类的java文件：
   |--粘贴语句：javac Test.java

4、编译修改后的API核心类：（执行命令后无视警告继续第5步）
   |--粘贴语句：javac Integer.java

5、将得到的两个class文件装入java/lang文件夹中

6、使用jar命令打包java文件夹
   |--粘贴语句：jar vcf myapi.jar java
   |--vcf中v表示详细 c表示创建 f表示指定jar包的文件名

7、使用一下指令执行Test.class文件
   |--粘贴语句：java -Xbootclasspath/p:myapi.jar Test
