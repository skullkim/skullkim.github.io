---
layout:       post
title:        "Nested class, inner class"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- java
---

<head></head>
<body id="tt-body-page" class="">
<div id="wrap" class="wrap-right">
    <div id="container">
        <main class="main ">
            <div class="area-main">
                <div class="area-view">
                    <div class="article-header"></div>
                    <hr>
                    <div class="article-view">
                        <div class="contents_style">
                            <pre id="code_1620185801764" class="java" data-ke-language="java" data-ke-type="codeblock"><code>class Outer{
	class Nested{}
}</code></pre>
<p>위 코드에서 Nested클래와 같이 클래스 내부에 있는 클래스를 nested class라고 한다. 이때 nested class는 두 종류로 나뉜다.</p>
<p>&nbsp; 1. Static nested class</p>
<pre id="code_1620185911446" class="java" data-ke-language="java" data-ke-type="codeblock"><code>class Outer{
    static class StaticNested{}
}</code></pre>
<p>&nbsp; 2. Non-static nested class(inner class)</p>
<pre id="code_1620185932692" class="java" data-ke-language="java" data-ke-type="codeblock"><code>class Outer{
    class Inner{}
}</code></pre>
<p>그리고 inner class는 다음과 같은 세 종류로 나뉜다</p>
<p>&nbsp; 1. Member Inner Class:멤버 변수와 같은 위치에 정의된 클래스</p>
<p>&nbsp; 2. Local Inner Class:메서드 내에서 정의된 클래스</p>
<p>&nbsp; 3. Anonymous Inner Class: 클래스 이름이 없는 클래스</p>
<p>&nbsp; 이때 통상적으로 Inner를&nbsp; 생략하고 다음과 같이 부른다. member class, local class, anonymous class</p>
<p>&nbsp;</p>
<p><b>Static nested class</b></p>
<pre id="code_1620186300900" class="java" data-ke-language="java" data-ke-type="codeblock"><code>class Outer{
    private static int num = 0;
    static class Nested{
        void add(int n){num += n;}
        int get(){return num;}
    }
}

public class Main {
    public static void main(String[] args){
        Outer.Nested n1 = new Outer.Nested();
        n1.add(2);
        Outer.Nested n2 = new Outer.Nested();
        System.out.println(n2.get());
    }
}
//출력: 2</code></pre>
<p>위 코드에서 볼 수 있듯이 static nested class는 왜부 클래스의 static 멤버 변수에 접근이 가능하다. 또 한 외부 클래스의 인스턴스 생성 없이도 생성이 가능하다. 이때문에 Static nested class는 클래스 내에서 외부 클래스의 인스턴스 변수와 메소드에 접근할 수 없다.</p>
<p>&nbsp;</p>
<p><b>Member class</b></p>
<pre id="code_1620186678370" class="java" data-ke-language="java" data-ke-type="codeblock"><code>class Outer{
    private int num = 0;
    class Member{
        void add(int n){num += n;}
        int get(){return num;}
    }
}

public class Main {
    public static void main(String[] args){
        Outer o1 = new Outer();
        Outer o2 = new Outer();
        Outer.Member om1 = o1.new Member();
        Outer.Member om2 = o2.new Member();
        om1.add(3);
        System.out.println(om1.get());
        om2.add(10);
        System.out.println(om2.get());
    }
}
//출력:
//3
//10</code></pre>
<p>위 코드에서 볼수 있듯이 Member class내에서 외부 클래스의 인스턴스 변수에 접근이 가능하다(private이여도 가능). 또 한 외부 클래스의 인스턴스 없이는 멤버 클래스 인스턴스의 생성이 불가능하다. 따라서 멤버 클래스의 인스턴스는 외부 클래스 인스턴스에 종속적이다.</p>
<p>&nbsp;&nbsp;<i><b>Member class의 장점</b></i></p>
<pre id="code_1620187206244" class="java" data-ke-language="java" data-ke-type="codeblock"><code>interface Printable{
    void print();
}

class Papers{
    private String con;
    public Papers(String s){con = s;}
    public Printable getPrinter(){//return member class instance
        return new Printer();
    }
    private class Printer implements Printable{//Member class
        @Override public void print(){
            System.out.println(con);
        }
    }
}

public class Main {
    public static void main(String[] args){
       Papers p = new Papers("Hello member class");
       Printable prn = p.getPrinter();
       prn.print();
    }
}
//출력: Hello member class</code></pre>
<p>&nbsp; 위 코드를 보면 멤버 클래스가 private이기 때문에 멤버클래스를 감싸는 외부 클래스 에서만 인스턴스 생성이 가능하다. 따라서 해당 멤버 클래스의 인스턴스를 참조하기 위해 getter를 호출했다. 그때문에 외부에서는 getPrinter메소드가 어떤 인스턴스의 참조값을 반환하는지 알지 못한다. 그저 반환되는 참조 값이 인스턴스가 Printable를 구현하고 있어서 Printable의 참조 변수로 참조할 수 있다는 것만 알고 있다. 이를 <i><b>클래스의 정의가 감추어진 상황</b></i>이라 한다.&nbsp;</p>
<p>&nbsp; 이경우 getter가 반환하는 인스턴스가 다른 클래스의 인스턴스로 변경되어도 Papers클래스 외부의 코드는 수정할 필요가 없게 되기 때문에 코드에 유연성이 부여된다.&nbsp;</p>
<p>&nbsp;</p>
<p><b>Local class</b></p>
<pre id="code_1620187856851" class="java" data-ke-language="java" data-ke-type="codeblock"><code>interface Printable{
    void print();
}

class Papers{
    private String con;
    public Papers(String s){con = s;}
    public Printable getPrinter(){//getter, return Printer instance
        class Printer implements Printable{//local class
            @Override public void print(){
                System.out.println(con);
            }
        }
        return new Printer();
    }
}

public class Main {
    public static void main(String[] args){
       Papers p = new Papers("Hello local class");
       Printable prn = p.getPrinter();
       prn.print();
    }
}
//출력: Hello local class</code></pre>
<p>&nbsp; 위와 같이 local class는 메서드 내에서 정의 되어 있어서 해당 메서드 내에서만 정의가 가능하다. 따라서 local class에 대한 private선언의 무의미하다. local class는 member class보다 더 깊이, 특정 블록안에 클래스를 감춘다.</p>
<p>&nbsp;</p>
<p><b>Anonymous class</b></p>
<pre id="code_1620188219393" class="java" data-ke-language="java" data-ke-type="codeblock"><code>interface Printable{
    void print();
}

class Papers{
    private String con;
    public Papers(String s){con = s;}
   public Printable getPrinter(){
        return new Printable() {
            @Override
            public void print() {
                System.out.println(con);
            }
        };
   }
}

public class Main {
    public static void main(String[] args){
       Papers p = new Papers("Hello anonymous class");
       Printable prn = p.getPrinter();
       prn.print();
    }
}
//출력: Hello anonymous class</code></pre>
<p>&nbsp;</p>
                        </div>
                        <br>
                        <div class="tags"></div>
                    </div>
                    
                </div>
            </div>
        </main>
    </div>
</div>


</body>