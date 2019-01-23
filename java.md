# Java

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


### Date and Time

```java
import java.util.*;
import java.text.SimpleDateFormat;

import java.time.temporal.*;
import static java.time.temporal.TemporalAdjusters.*;

class DateTime {
  public static void main(String[] args) {
    //*************************************************
    // Calendar (old) : abstract class
    Calendar today = Calendar.getInstance(); // abstract class
    System.out.println("****************************************************");
    System.out.println(today.get(Calendar.YEAR) +" 년 ");
    System.out.println(today.get(Calendar.MONTH)+1 +" 월 ");
    System.out.println(today.get(Calendar.DATE) + " 일 ");
    System.out.println(today.get(Calendar.DAY_OF_WEEK) +" 요일 (1:일요일) ");
    System.out.println(today.get(Calendar.AM_PM) + " (0:오전, 1:오후)");
    System.out.println(today.get(Calendar.HOUR) + " 시 (12시간)");
    System.out.println(today.get(Calendar.HOUR_OF_DAY) + " 시 (24시간)");
    System.out.println(today.get(Calendar.MINUTE) + " 분 ");
    System.out.println(today.get(Calendar.SECOND) + " 초 ");
    System.out.println(today.get(Calendar.ZONE_OFFSET)/(60*60*1000) + " : time zone (-12 ~ +12) ");
    System.out.println(today.getActualMaximum(Calendar.DATE) + " : 이 달의 마지막 일 ");

    // 요일은 1부터 시작되기 때문에, DAY_OF_WEEK[0]은 비워둠
    final String[] DAY_OF_WEEK = {"","일", "월","화","수","목","금","토"};

    Calendar date1 = Calendar.getInstance();
    Calendar date2 = Calendar.getInstance();
    System.out.println("****************************************************");
    date1.set(2018, 0, 16); // 2018년 1월 16일
    System.out.println("date1 : " + date1.get(Calendar.YEAR) + " 년 " + date1.get(Calendar.MONTH)+1 + " 월 " + date1.get(Calendar.DATE) + " 일 ");
    System.out.println("date2 : " + date2.get(Calendar.YEAR) + " 년 " + date2.get(Calendar.MONTH)+1 + " 월 " + date2.get(Calendar.DATE) + " 일 ");
    long difference =  (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
    System.out.println("date1과 date2의 차이 일수 : " + difference/(24*60*60));

    System.out.println("****************************************************");
    final int[] TIME_UNIT = {3600, 60, 1};
    final String[] TIME_UNIT_NAME = {"시간", "분", "초"};

    Calendar time1 = Calendar.getInstance();
    Calendar time2 = Calendar.getInstance();

    time1.set(Calendar.HOUR_OF_DAY, 10);
    time1.set(Calendar.MINUTE, 20);
    time1.set(Calendar.SECOND, 30);

    time2.set(Calendar.HOUR_OF_DAY, 20);
    time2.set(Calendar.MINUTE, 30);
    time2.set(Calendar.SECOND, 10);

    System.out.println("time1 : " + time1.get(Calendar.HOUR_OF_DAY) + " 시 "
                                  + time1.get(Calendar.MINUTE) + " 분 "
                                  + time1.get(Calendar.SECOND) + " 초 ");

    System.out.println("time2 : " + time2.get(Calendar.HOUR_OF_DAY) + " 시 "
                                  + time2.get(Calendar.MINUTE) + " 분 "
                                  + time2.get(Calendar.SECOND) + " 초 ");

    long difference2 = Math.abs(time2.getTimeInMillis() - time1.getTimeInMillis())/1000;
    System.out.println("time1과 time2의 차이는 " + difference2 + " 초입니다.");
    String tmp = "";
    for (int i=0; i<TIME_UNIT.length; i++){
      tmp += difference2/TIME_UNIT[i] + TIME_UNIT_NAME[i];
      difference2 %= TIME_UNIT[i];
    }
    System.out.println("시분초로 변환하면 " + tmp + " 입니다.");


    System.out.println("****************************************************");
    Calendar dt1= Calendar.getInstance();
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd"); // import java.text.SimpleDateFormat
    dt1.set(2001, 3, 12);  // 2001년 4월 12일

    System.out.println(dt1.toString()); // Calendar structure?
    System.out.println(sdf.format(dt1.getTime()));
    System.out.println("== 1일 후 ==");
    dt1.add(Calendar.DATE, 1);
    System.out.println(sdf.format(dt1.getTime()));

    System.out.println("== 6개월 전 ==");
    dt1.add(Calendar.MONTH, -6);
    System.out.println(sdf.format(dt1.getTime()));

    System.out.println("== 40일 후 (roll) ==");
    dt1.roll(Calendar.DATE, 40);                    // roll : month는 바뀌지 않고 date만 40일 추가
    System.out.println(sdf.format(dt1.getTime()));

    System.out.println("== 40일 후 (add) ==");
    dt1.add(Calendar.DATE, 40);
    System.out.println(sdf.format(dt1.getTime()));

    System.out.println("****************************************************");
    System.out.println(" Calendar (해당월만) ");
    // if(args.length !=2) {
    //   System.out.println("Usage : java DateTime 2011 8 ");
    //   return;
    // }
    // int year = Integer.parseInt(args[0]);
    // int month = Integer.parseInt(args[1]);

    int year = 2015;
    int month = 11;

    int START_DAY_OF_WEEK = 0;
    int END_DAY = 0;

    Calendar sDay = Calendar.getInstance();     // 시작일
    Calendar eDay = Calendar.getInstance();     // 종료일

    sDay.set(year, month-1, 1);                 // 해당년월의 첫일
    eDay.set(year, month, 1);

    eDay.add(Calendar.DATE, -1);                // 해당년월의 마지막일

    START_DAY_OF_WEEK = sDay.get(Calendar.DAY_OF_WEEK);
    //System.out.println("week : " + START_DAY_OF_WEEK);
    END_DAY = eDay.get(Calendar.DATE);

    System.out.println("     " + year + " 년 " + month + " 월 ");
    System.out.println(" SU MO TU WE TH FR SA ");

    for (int i = 1; i < START_DAY_OF_WEEK; i++ ){
      System.out.print("   ");
    }

    for (int i = 1, n=START_DAY_OF_WEEK; i <= END_DAY; i++, n++){
      System.out.print((i<10)? "  "+i : " "+i);        // 10이하일 경우 " "을 한칸 더
      if (n%7==0) System.out.println();
    }

    System.out.println("****************************************************");
    System.out.println(" Calendar (이전달, 이후 달과 함께)  ");

    // if(args.length !=2) {
    //   System.out.println("Usage : java DateTime 2011 8 ");
    //   return;
    // }
    // int year = Integer.parseInt(args[0]);
    // int month = Integer.parseInt(args[1]);

    Calendar sDay1 = Calendar.getInstance();     // 시작일
    Calendar eDay1 = Calendar.getInstance();     // 종료일

    sDay1.set(year, month-1, 1);                 // 해당년월의 첫일
    eDay1.set(year, month-1, sDay.getActualMaximum(Calendar.DATE));
    sDay1.add(Calendar.DATE, -sDay1.get(Calendar.DAY_OF_WEEK)+1);  // 일요일
    eDay1.add(Calendar.DATE, 7 - eDay1.get(Calendar.DAY_OF_WEEK));    // 토요일

    System.out.println("     " + year + " 년 " + month + " 월 ");
    System.out.println(" SU MO TU WE TH FR SA ");

    for (int n=1; sDay1.before(eDay1) || sDay1.equals(eDay1); sDay1.add(Calendar.DATE, 1)){
      int day = sDay1.get(Calendar.DATE);
      System.out.print((day<10)? "  "+day : " "+day);        // 10이하일 경우 " "을 한칸 더
      if (n++%7==0) System.out.println();
    }

    System.out.println("****************************************************");
    String dateM1 = "201508";
    String dateM2 = "201405";

    int month1 = Integer.parseInt(dateM1.substring(0,4))*12 + Integer.parseInt(dateM1.substring(4));
    int month2 = Integer.parseInt(dateM2.substring(0,4))*12 + Integer.parseInt(dateM2.substring(4));

    System.out.println("개월 차이 : " + Math.abs(month1 - month2));

    System.out.println("****************************************************");
    System.out.println("2014.05.31 : " + getDayOfWeek(2014, 5, 31));
    System.out.println("2012.06.01 : " + getDayOfWeek(2012, 6, 1));
    System.out.println("2014.05.01 - 2014.4.28 : " + dayDiff(2014, 5, 1, 2014, 4, 28));
    System.out.println("2015.06.29 : " + convertDayToDay(2015, 6, 29));
    System.out.println("735778 : " + convertDayToDay(735778));

    System.out.println("****************************************************");
    System.out.println(" DecimalFormat (java.text.*)");
    double number = 1234567.89;

    String[] pattern = {
        "0",
        "#",
        "0.0",
        "#.#",
        "0000000000.0000",
        "##########.####",
        "#.#-",
        "-#.#",
        "#,###,##",
        "#,####,##",
        "#E0",
        "0E0",
        "##E0",
        "00E0",
        "####E0",
        "0000E0",
        "#.#E0",
        "0.0E0",
        "0.000000000E0",
        "00.00000000E0",
        "000.0000000E0",
        "#.#########E0",
        "##.########E0",
        "###.#######E0",
        //"#.###.##+;#.###.##-",
        "#.#%",
        "#.#\u2030",
        "\u00A4 #,###",
        "'#'#,###",
        "''#,###",
    };

    for (int i = 0; i < pattern.length; i++) {
      java.text.DecimalFormat df = new java.text.DecimalFormat(pattern[i]);
      System.out.printf("%19s : %s \n", pattern[i], df.format(number));
    }

    System.out.println("****************************************************");
    System.out.println(" SimpleDateFormat (java.text.*) ");
    Date tday = new Date();

    java.text.SimpleDateFormat sdf1, sdf2, sdf3, sdf4;
    java.text.SimpleDateFormat sdf5, sdf6, sdf7, sdf8;

    sdf1 = new java.text.SimpleDateFormat("yyyy-MM-dd");
    sdf2 = new java.text.SimpleDateFormat("''yy MMM dd일 E요일");
    sdf3 = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
    sdf4 = new java.text.SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");

    sdf5 = new java.text.SimpleDateFormat("오늘은 올 해의 D번째 날입니다.");
    sdf6 = new java.text.SimpleDateFormat("오늘은 이 달의 d번째 날입니다.");
    sdf7 = new java.text.SimpleDateFormat("오늘은 올 해의 w번째 날입니다.");
    sdf8 = new java.text.SimpleDateFormat("오늘은 이 달의 W번째 날입니다.");
    // sdf9 = new java.text.SimpleDateFormat("오늘은 이 달의 F번째 E요일입니다.");

    System.out.println(sdf1.format(tday));
    System.out.println(sdf2.format(tday));
    System.out.println(sdf3.format(tday));
    System.out.println(sdf4.format(tday));
    System.out.println();
    System.out.println(sdf5.format(tday));
    System.out.println(sdf6.format(tday));
    System.out.println(sdf7.format(tday));
    System.out.println(sdf8.format(tday));
    // System.out.println(sdf9.format(tday));

    System.out.println("****************************************************");
    System.out.println(" Calendar instance를 Date instance로 변환 ");

    Calendar cal1 = Calendar.getInstance();
    cal1.set(2005, 9, 3);

    Date dy1 = cal1.getTime();

    java.text.SimpleDateFormat sf1, sf2, sf3, sf4;
    sf1 = new SimpleDateFormat("yyyy-MM-dd");
    sf2 = new SimpleDateFormat("yyyy-MM-dd E요일");
    sf3 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS");
    sf4 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss a");

    System.out.println(sf1.format(dy1));
    System.out.println(sf2.format(dy1));
    System.out.println(sf3.format(dy1));
    System.out.println(sf4.format(dy1));

    System.out.println("****************************************************");
    System.out.println(" 문자열을 Date instance로 변환 ");
    java.text.DateFormat ddf1 = new java.text.SimpleDateFormat("yyyy년 MM월 dd일");
    java.text.DateFormat ddf2 = new java.text.SimpleDateFormat("yyyy/MM/dd");

    try {
      Date d = ddf1.parse("2015년 11월 23일"); // Convert String into Date
      System.out.println(ddf2.format(d));
    } catch (Exception e) {}

    System.out.println("****************************************************");
    System.out.println(" 정해진 format으로 입력 ");

    // String pttrn = "yyyy/MM/dd";
    // java.text.DateFormat ddf = new java.text.SimpleDateFormat(pttrn);
    // Scanner s = new Scanner(System.in);
    //
    // Date inDate = null;
    //
    // System.out.println("날짜를 " + pttrn + "의 형태로 입력해주세요. (입력예: 2015/12/31)");
    //
    // while(s.hasNextLine()) {
    //   try {
    //     inDate = ddf.parse(s.nextLine());
    //     break;
    //   } catch (Exception e) {
    //     System.out.println("날짜를 " + pttrn + "의 형태로 다시 입력해주세요. (입력예: 2015/12/31)");
    //   }
    // } //while
    //
    // Calendar ccal = Calendar.getInstance();
    // ccal.setTime(inDate);
    // Calendar ttday = Calendar.getInstance();
    // long day = (ccal.getTimeInMillis() - ttday.getTimeInMillis())/(60*60*1000);
    // System.out.println("입력하신 날짜는 현재와 " + day + " 시간 차이가 있습니다.");

    System.out.println("****************************************************");
    System.out.println(" ChoiceFormat : 특정범위에 속하는 값을 문자열로 변환. (java.text.*) ");

    double[] limits = {60, 70, 80, 90}; // 낮은 값부터 큰 값의 순서로 적어야 함
    String[] grades = {"D", "C", "B", "A"};

    int[] scores = {100, 95, 88, 70, 52, 60, 70};

    java.text.ChoiceFormat form = new java.text.ChoiceFormat(limits, grades);

    for (int i =0; i<scores.length; i++) {
      System.out.println(scores[i] + ":" + form.format(scores[i]));
    }

    System.out.println("****************************************************");
    System.out.println(" ChoiceFormat : limit#value (경계값 포함), limit<value (경계값 불포함) ");
    String grdPttrn = "60#D|70#C|80<B|90#A";
    int[] scrs = {91, 90, 80, 88, 70, 52, 60};

    java.text.ChoiceFormat frm = new java.text.ChoiceFormat(grdPttrn);
    for (int i=0; i<scrs.length; i++) {
      System.out.println(scores[i] + ":" + frm.format(scrs[i]));
    }

    System.out.println("****************************************************");
    System.out.println(" MessageFormat : 데이터를 정해진 양식에 맞게 출력 (java.text.*) ");

    String msg = "Name: {0} \n Tel: {1} \n Age: {2} \n Birthday: {3}";

    Object[] arguments = {
      "이자바", "02-123-1234", "27", "07-09"
    };

    System.out.println(java.text.MessageFormat.format(msg, arguments));

    System.out.println("****************************************************");
    System.out.println(" MessageFormat : INSERT 에 삽입 예제 (java.text.*) ");
    String tbl_name1 = "CUST_INFO";
    String msg1 = "INSERT INTO " + tbl_name1 +
                                " VALUES (''{0}'',''{1}'',''{2}'',''{3}'') ";

    Object[][] arguments1 = {
      {"이자바", "02-123-1234", "27", "07-09"},
      {"김프로", "031-333-1234", "33", "10-07"},
    };

    for (int i=0; i< arguments1.length; i++) {
      String result = java.text.MessageFormat.format(msg1, arguments1[i]);
      System.out.println(result);
    }

    System.out.println("****************************************************");
    System.out.println(" MessageFormat : INSERT 문에서 데이터 추출 (java.text.*) ");

    String[] data1 = {
      "INSERT INTO CUST_INFO VALUES ('이자바','02-123-1234','27','07-09');",
      "INSERT INTO CUST_INFO VALUES ('김프로','031-333-1234','33','10-07');"
    };

    String pattern1 = "INSERT INTO CUST_INFO VALUES ({0},{1},{2},{3});";
    java.text.MessageFormat mf = new java.text.MessageFormat(pattern1);

    for(int i=0; i<data1.length; i++){
      try {
        Object[] objs = mf.parse(data1[i]);
        for (int j=0; j<objs.length; j++){
          System.out.print(objs[j] + ",");
        }
      } catch (Exception e){ System.out.println(e);}
      System.out.println();
    }

    System.out.println("****************************************************");
    System.out.println(" MessageFormat : txt화일을 읽어 INSERT 에 데이터 삽입 예제 (java.text.*) ");

    String tbl_name2 = "CUST_INFO";
    String msg2 = "INSERT INTO " + tbl_name2 +
                                " VALUES ({0},{1},{2},{3}) ";
    String pattern2 = "{0},{1},{2},{3}";
    java.text.MessageFormat mf2 = new java.text.MessageFormat(pattern2);

    String fileName1 = "data4.txt";
    try {
      Scanner sc = new Scanner(new java.io.File(fileName1));
      while(sc.hasNextLine()){
        String line = sc.nextLine();
        Object[] objs = mf2.parse(line);
        System.out.println(java.text.MessageFormat.format(msg2, objs));
      }
      sc.close();
    } catch (Exception e){ System.out.println(e);}

    System.out.println("****************************************************");
    System.out.println(" java.time 패키지 ");
    System.out.println(" LocalDate : 날짜 ");
    System.out.println(" LocalTime : 시간 ");
    System.out.println(" LocalDateTime : 날짜 + 시간 ");
    System.out.println(" ZonedDateTime : 날짜 + 시간 + 시간대 ");
    System.out.println(" Period = 날짜 - 날짜  ");
    System.out.println(" Duration = 시간 - 시간 ");

    System.out.println("****************************************************");
    System.out.println(" LocalDate와 LocalTime ");
    java.time.LocalDate today1 = java.time.LocalDate.now(); // 현재의 날짜
    java.time.LocalTime now1 = java.time.LocalTime.now(); // 현재의 시간

    java.time.LocalDate birthday1 = java.time.LocalDate.of(1999, 12, 31); // 1999년 12월 31일
    java.time.LocalTime birthtime1 = java.time.LocalTime.of(23, 59, 59); // 23시 59분 59초

    System.out.println("today = " + today1);
    System.out.println("now = " + now1);

    System.out.println("birthday = " + birthday1);
    System.out.println("birthtime = " + birthtime1);

    System.out.println(birthday1.withYear(2000)); // 2000년 12월 31일
    System.out.println(birthday1.withMonth(3)); // 1999년 3월 31일
    System.out.println(birthday1.withDayOfMonth(3)); // 1999년 12월 3일
    System.out.println();

    System.out.println(birthday1.plusDays(1)); // 2000년 1월 1일
    System.out.println(birthday1.plusMonths(2)); // 2000년 2월 29일
    System.out.println(birthday1.plusYears(3)); // 2002년 12월 31일
    System.out.println();

    System.out.println(birthday1.minusDays(1)); // 1999년 12월 30일
    System.out.println(birthday1.minusMonths(2)); // 1999년 10월 31일
    System.out.println(birthday1.minusYears(3)); // 1996년 12월 31일
    System.out.println();

    System.out.println(birthday1.getYear());      // 1999
    System.out.println(birthday1.getMonthValue()); // 12
    System.out.println(birthday1.getMonth());      // DECEMBER
    System.out.println(birthday1.getDayOfMonth()); // 31
    System.out.println(birthday1.getDayOfYear()); // 365
    System.out.println(birthday1.getDayOfWeek()); // FRIDAY
    System.out.println(birthday1.getDayOfWeek().getValue()); // 5
    System.out.println(birthday1.lengthOfMonth()); // 해당월의 총일수 31
    System.out.println(birthday1.lengthOfYear()); // 해당년의 총일수 윤년일 경우 366, 아닐 경우 365
    System.out.println();

    System.out.println(birthtime1.getHour());
    System.out.println(birthtime1.getMinute());
    System.out.println(birthtime1.getSecond());
    System.out.println();

    System.out.println(birthday1.isLeapYear());


    System.out.println(birthday1.plus(1, java.time.temporal.ChronoUnit.DAYS)); // 2000년 1월 1일

    System.out.println(java.time.temporal.ChronoField.CLOCK_HOUR_OF_DAY.range()); // 1-24
    System.out.println(java.time.temporal.ChronoField.HOUR_OF_DAY.range()); // 0-23

    System.out.println("****************************************************");
    System.out.println(" LocalDateTime과 ZonedDateTime ");

    java.time.LocalDate date3 = java.time.LocalDate.of(2015, 12, 31); // 2015년 12월 31일
    java.time.LocalTime time3 = java.time.LocalTime.of(12, 34, 56);   // 12시 34분, 56초

    java.time.LocalDateTime dt3 = java.time.LocalDateTime.of(date3, time3);
    System.out.println(dt3);

    java.time.ZoneId zid3 = java.time.ZoneId.of("Asia/Seoul");
    java.time.ZonedDateTime zdt3 = dt3.atZone(zid3);
    System.out.println(zid3);
    System.out.println(zdt3);

    java.time.ZonedDateTime seoulTime = java.time.ZonedDateTime.now();
    java.time.ZoneId nyId = java.time.ZoneId.of("America/New_York");
    java.time.ZonedDateTime nyTime = java.time.ZonedDateTime.now().withZoneSameInstant(nyId);
    System.out.println(seoulTime);
    System.out.println(nyTime);

    java.time.OffsetDateTime odt3 = zdt3.toOffsetDateTime();
    System.out.println(odt3);

    System.out.println("****************************************************");
    System.out.println(" TemporalAdjusters (static java.time.temporal.TemporalAdjusters.*;)");

    java.time.LocalDate today4 = java.time.LocalDate.now();
    java.time.LocalDate date4 = today4.with(new DayAfterTomorrow());
    System.out.println(today4);
    System.out.println(date4);
    System.out.println(today4.with(firstDayOfNextMonth())); // 다음 달의 첫 날
    System.out.println(today4.with(firstDayOfMonth())); // 이 달의 첫 날
    System.out.println(today4.with(lastDayOfMonth())); // 이 달의 마지막 날
    System.out.println(today4.with(firstInMonth(java.time.DayOfWeek.FRIDAY)));    // 이 달의 첫번째 화요일
    System.out.println(today4.with(lastInMonth(java.time.DayOfWeek.TUESDAY))); // 이 달의 마지막 화요일
    System.out.println(today4.with(previous(java.time.DayOfWeek.TUESDAY))); // 지난 주 화요일
    System.out.println(today4.with(previousOrSame(java.time.DayOfWeek.TUESDAY))); // 지난 주 화요일 (오늘 포함)
    System.out.println(today4.with(next(java.time.DayOfWeek.TUESDAY))); // 다음 주 화요일
    System.out.println(today4.with(nextOrSame(java.time.DayOfWeek.TUESDAY))); // 다음 주 화요일 (오늘 포함)
    System.out.println(today4.with(dayOfWeekInMonth(4, java.time.DayOfWeek.TUESDAY))); // 이달의 4번째 화요일

    System.out.println("****************************************************");
    System.out.println(" Period와 Duration ");
    java.time.LocalDate date5 = java.time.LocalDate.of(2014, 1, 1);
    java.time.LocalDate date6 = java.time.LocalDate.of(2015, 12, 31);

    java.time.Period pe = java.time.Period.between(date5, date6);

    System.out.println("date5 = " + date5);
    System.out.println("date6 = " + date6);
    System.out.println("pe = " + pe);

    System.out.println("YEAR = " + pe.get(java.time.temporal.ChronoUnit.YEARS));
    System.out.println("MONTH = " + pe.get(java.time.temporal.ChronoUnit.MONTHS));
    System.out.println("DAY = " + pe.get(java.time.temporal.ChronoUnit.DAYS));

    java.time.LocalTime time5 = java.time.LocalTime.of(0, 0, 0);
    java.time.LocalTime time6 = java.time.LocalTime.of(12, 34, 56); // 12시 23분 56초

    java.time.Duration du = java.time.Duration.between(time5, time6);

    System.out.println("time5 = " + time5);
    System.out.println("time6 = " + time6);

    java.time.LocalTime tmpTime = java.time.LocalTime.of(0,0).plusSeconds(du.getSeconds());

    System.out.println("HOUR = " + tmpTime.getHour());
    System.out.println("MINUTE = " + tmpTime.getMinute());
    System.out.println("SECOND = " + tmpTime.getSecond());
    System.out.println("NANO = " + tmpTime.getNano());


  } // main

  public static int[] endOfMonth = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

  public static boolean isLeapYear(int year) {
    return ((year%4==0)&&(year%100!=0)&&(year%400==0));
  }

  public static int dayDiff(int y1, int m1, int d1, int y2, int m2, int d2) {
    return convertDayToDay(y1, m1, d1) - convertDayToDay(y1, m1, d1);
  }

  public static int getDayOfWeek(int year, int month, int day){
    return convertDayToDay(year, month, day)%7 + 1;
  }

  public static String convertDayToDay(int day) {
    int year = 1;
    int month = 0;
    int numOfLeapYear = 0;

    while(true) {
      int aYear = isLeapYear(year)? 366 : 365;
      if (day > aYear) {
        day -= aYear;
        year++;
      } else {
        break;
      }
    }

    while(true) {
      int endDay = endOfMonth[month];
      // 윤년이고 윤달이 포함되어 있으면, 1일을 더 뺀다.
      if (isLeapYear(year) && month == 1) endDay++;

      if(day > endDay) {
        day -= endDay;
        month++;
      } else {
        break;
      }
    }
    return year + "-" + (month+1) + "-" + day;
  }

  public static int convertDayToDay(int year, int month, int day) {
    int numOfLeapYear = 0;

    for (int i=1; i<year; i++) {
      if (isLeapYear(i))
        numOfLeapYear++;
    }
    // 전년까지의 일수를 구한다
    int toLastYearDaySum = (year-1)*365 + numOfLeapYear;

    // 올해의 현재 월까지의 일수 계산
    int thisYearDaySum = 0;

    for (int i =0; i < month-1; i++) {
      thisYearDaySum += endOfMonth[i];
    }

    // 윤년이고, 2월이 포함되어 있으면 1일을 증가시킨다.
    if (month > 2 && isLeapYear(year))
      thisYearDaySum++;

    thisYearDaySum+=day;

    return toLastYearDaySum + thisYearDaySum;
  }
}

class DayAfterTomorrow implements TemporalAdjuster {
    @Override
    public Temporal adjustInto(Temporal temporal) {
      return temporal.plus(2, java.time.temporal.ChronoUnit.DAYS);
    }
}
```
