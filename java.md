# Java 정리

### packages

```java


// Object 클래스
// protected Object clone() : 객체 자산의 복사본을 반환
// public boolean equals(Object obj) : 객체 자신과 객체 obj가 같은 객체인지 알려줌
// public Class getClass() : 객체 자신의 클래스 정보를 담고 있는 Class 인스턴스를 반환한다.
// public int hashCode() : 객체 자신의 hashCode를 반환한다.
// public String toString() : 객체 자신의 정보를 문자열로 반환한다.
// public void notify() : 객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다.
// public void notifyAll() : 객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다.
// public void wait(long timeout) : 다른 쓰레드가 notify()나 notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 또는 지정된 시간동안 기다리게 한다

class packages {
  public static void main(String[] args) {
    Value v1 = new Value(10);
    Value v2 = new Value(10);

    if (v1.equals(v2)){
      System.out.println("v1과 v2는 같습니다.");
    } else {
      System.out.println("v1과 v2는 다릅니다.");
    }
    v2 = v1;

    if (v1.equals(v2)){
      System.out.println("v1과 v2는 같습니다.");
    } else {
      System.out.println("v1과 v2는 다릅니다.");
    }

    Person p1 = new Person(4525426L);
    Person p2 = new Person(4525426L);

    if(p1 == p2) {
      System.out.println("p1과 p2는 같은 객체입니다.");
    } else {
      System.out.println("p1과 p2는 다른 객체입니다.");
    }
    if(p1.equals(p2)) {
      System.out.println("p1과 p2는 같은 사람입니다.");
    } else {
      System.out.println("p1과 p2는 다른 사람입니다.");
    }
    //*************************************************
    // hashCode는 해싱(hashing)기법에 사용되는 해시함수를 구현한 것으로 다량의 데이터를 저장하고 검색하는데 유용
    String str1 = new String("abc");
    String str2 = new String("abc");

    System.out.println(str1.equals(str2));
    System.out.println(str1.hashCode());
    System.out.println(str2.hashCode());
    System.out.println(System.identityHashCode(str1));
    System.out.println(System.identityHashCode(str2));

    //*************************************************
    //toString : 인스턴스에 대한 정보를 문자열(String)으로 제공. Object 클래스에서는 hashCode, String클래스는 string, Date 클래스는 시간을 반환
    Card c1 = new Card();
    Card c2 = new Card();
    System.out.println(c1.toString());
    System.out.println(c2.toString());

    String str = new String("YOURSSUNSSUN");
    java.util.Date today = new java.util.Date();
    System.out.println(str);
    System.out.println(str.toString());
    System.out.println(today);
    System.out.println(today.toString());

    Card cc1 = new Card();
    Card cc2 = new Card("HEART", 10);
    System.out.println(cc1.toString());
    System.out.println(cc2.toString());


    //*************************************************
    // clone : 자신을 복제하여 새로운 인스턴스 생성
    Point original = new Point (2,3);
    //Point copy = (Point)original.clone();
    Point copy = original.clone();
    System.out.println(original);
    System.out.println(copy);

    int [] arr = {1,2,3,4,5};
    int [] arrClone = arr.clone();
    arr[0]=6;
    System.out.println(java.util.Arrays.toString(arr));
    System.out.println(java.util.Arrays.toString(arrClone));
    // 원본과 복제본 중 한곳이 변경되면 나머지 한곳도 변경되는 것을 얕은복사(shallow copy)라 하고 원본과 복제본 한쪽의 변경이 다른 한쪽에 영향을 미치지 않는 것을 깊은 복사(deep copy)라 한다.
    Circle cr1 = new Circle(new Point(1,1), 2.0);
    Circle cr2 = cr1.shallowCopy();   // 얕은 복사
    Circle cr3 = cr1.deepCopy();      // 깊은 복사
    System.out.println(cr1);
    System.out.println(cr2);
    System.out.println(cr3);
    cr1.p.x = 10;
    cr1.p.y = 10;
    System.out.println("cr1의 x,y변경 후");
    System.out.println(cr1);
    System.out.println(cr2);
    System.out.println(cr3);

    //*************************************************
    // getClass : 자신이 속한 클래스의 Class객체를 반환
    // Class cObj = new Card().getClass(); // 생성된 객체로 부터 Class객체에 대한 참조 얻음
    // Class cObj = Card.class;            // 클래스 리터럴 (*.class)로 부터 얻는 방법
    // Class cObj = Class.forName("Card"); // 클래스 이름으로부터 얻는 방법 (에러발생 unreported exception ClassNotFoundException)
    // System.out.println(cObj);

    Card crd = new Card("HEART", 3);
    // Card crd2 = Card.class.newInstance(); // unreported exception InstantiationException
    Class cObj = crd.getClass();

    System.out.println(crd);
    System.out.println(cObj);
    System.out.println(cObj.getName());
    System.out.println(cObj.toGenericString());
    System.out.println(cObj.toString());


    //*************************************************
    // String : 변경 불가능
    String st1 = "abc";
    String st2 = "abc";

    System.out.println("String st1 =\"abc\"; ");
    System.out.println("String st2 =\"abc\"; ");

    System.out.println("st1 == st2 ? " + (st1==st2));
    System.out.println("st1.equals(st2) ? " + (st1.equals(st2)));
    System.out.println();

    String st3 = new String("\"abc\"");
    String st4 = new String("\"abc\"");

    System.out.println("String st3 = new String(\"abc\"); ");
    System.out.println("String st4 = new String(\"abc\"); ");

    System.out.println("st3 == st4 ? " + (st3==st4));
    System.out.println("st3.equals(st4) ? " + (st3.equals(st4)));

    String s1=new String("Hello");

    char[] c ={'H','e','l','l','o'};
    String s2 = new String(c);

    StringBuffer sb = new StringBuffer("Hello");
    String s3 = new String(sb);

    System.out.println(s3.charAt(1));

    System.out.println("aaa".compareTo("aaa")); // 같으면 0
    System.out.println("aaa".compareTo("bbb")); // 사전순으로 이후면 -1
    System.out.println("bbb".compareTo("aaa")); // 사전순으로 이전이면 1

    System.out.println("Hello".concat(" World"));
    System.out.println("Harry potter".contains("po"));
    System.out.println("readme.txt".endsWith("txt"));
    System.out.println("Hello".equals("HELLO"));
    System.out.println("Hello".equalsIgnoreCase("HELLO"));
    System.out.println("Hello".indexOf("l"));
    System.out.println("Hello".indexOf("lo"));
    System.out.println("java.lang.Object".lastIndexOf("Object"));
    System.out.println("java.lang.Object".lastIndexOf("."));
    System.out.println("java.lang.Object".startsWith("java"));
    System.out.println("java.lang.Object".substring(10));
    System.out.println("java.lang.Object".substring(5, 9));
    System.out.println("java.lang.Object".toUpperCase());
    System.out.println("java.lang.Object".toLowerCase());
    System.out.println("She's my girl".length());
    System.out.println("You are my moon".replace("moon","sun"));
    System.out.println("World religion is a kind of history".replaceAll("i","1"));
    System.out.println("World religion is a kind of history".replaceFirst("i","1"));
    System.out.println("                  a kind of history".trim());
    System.out.println(String.valueOf(true));
    java.util.Date dd = new java.util.Date();
    System.out.println(String.valueOf(dd));
    System.out.println(Integer.valueOf("100"));  // string to int
    System.out.println(Integer.parseInt("100"));
    System.out.println(Double.parseDouble("100"));
    String animals = "dog,cat,bear";
    String[] arn = animals.split(",");
    for (int i=0;i<arn.length;i++){
      System.out.println(arn[i]);
    }

    String fileName = "Packages.java";
    int idx = fileName.indexOf(".");
    System.out.println("File 이름 : " + fileName.substring(0, idx));
    System.out.println("File 확장자 : " + fileName.substring(idx+1));

    //*************************************************
    // StringBuffer : 변경 가능. 쓰레드의 동기화를 사용하지 않는 경우 StringBuilder사용
    StringBuffer strb = new StringBuffer("abc");
    strb.append("123");
    strb.append("ZZ");
    System.out.println(strb);
    System.out.println("Buffer size : " + strb.capacity());
    System.out.println("String size : " + strb.length());
    System.out.println(strb.charAt(4));
    System.out.println(strb.delete(2,4));
    System.out.println(strb.deleteCharAt(2));
    System.out.println(strb.insert(2,","));
    System.out.println(strb.reverse());
    System.out.println(strb.replace(2, 4,"MoT"));

    //*************************************************
    // Math
    System.out.println(java.lang.Math.round(10.24));
    System.out.println(java.lang.Math.ceil(10.24));
    System.out.println(java.lang.Math.floor(10.24));
    System.out.println(java.lang.Math.rint(10.24));
    System.out.println(java.lang.Math.sqrt(64));
    System.out.println(java.lang.Math.pow(8,2));
    System.out.println(java.lang.Math.log10(2));
    System.out.println(java.lang.Math.log(2));
    System.out.println(java.lang.Math.exp(2));
    System.out.println(java.lang.Math.max(3, 2));
    System.out.println(java.lang.Math.min(3, 2));
    System.out.println(java.lang.Math.random()); // 0~1 사이의 값
  }
}

class Value {
  int value;

  Value(int value){
    this.value = value;
  }
}

class Person {
  long id;

  public boolean equals(Object obj) {          // equals overriding
    if (obj != null && obj instanceof Person) {
      return id == ((Person)obj).id;           // obj가 object 타입이므로 id를 참조하기 위해서는 Person타입으로 형변환
    } else {
      return false;
    }
  }

  Person (long id){
    this.id = id;
  }
}

class Card {
  String kind;
  int number;

  Card() {
    this("SPADE", 1); // Card(String kind, int number)호출 : default값을 지정하는 방식
  }
  Card(String kind, int number) {
    this.kind = kind;
    this.number = number;
  }
  public String toString() {
    // Card 인스턴스의 kind와 number를 문자열로 반환
    return "kind : " + kind + ", number : " + number;
  }

}

class Point implements Cloneable{        // Cloneable인터페이스를 구현해야만 clone()호출 가능
  int x;
  int y;

  Point(int x, int y) {
    this.x = x;
    this.y = y;
  }

  public String toString() {
    return "x= " + x + ", y= " + y;
  }

  public Point clone() {               // public으로 변경
    Object obj = null;
    try {
      obj = super.clone();              // clone()은 반드시 예외처리를 해주어야 한다.
    } catch (CloneNotSupportedException e) {}
    return (Point)obj;                // 공변 반환 (covariant return type): 상위클래스 타입이 아닌 자신의 타입으로 반환
  }
}

class Circle implements Cloneable {
  Point p;  // 원점
  double r; // 반지름

  Circle(Point p, double r) {
    this.p = p;
    this.r = r;
  }

  public Circle clone() {  //얕은 복사
    Object obj = null;
    try {
      obj = super.clone();              // clone()은 반드시 예외처리를 해주어야 한다.
    } catch (CloneNotSupportedException e) {}
    return (Circle)obj;                // Circle내의 Point는 같은 인스턴스를 사용하므로 한쪽이 변경되면 다른 쪽이 변경된다.
  }

  public Circle shallowCopy() {
      return this.clone();
  }

  public Circle deepCopy() { //깊은 복사
    Object obj = null;
    try {
      obj = super.clone();              // clone()은 반드시 예외처리를 해주어야 한다.
    } catch (CloneNotSupportedException e) {}
    Circle c = (Circle)obj;
    c.p = new Point(this.p.x, this.p.x);  // Circle내의 Point instance를 새로 생성함으로서 한쪽이 변경되도 다른쪽이 변경되지 않는다.
    return c;
  }

  public String toString() {
    return "[p=]" + p + ", r=" + r +"]";
  }

}

```
