# 27433 팩토리얼2

<h3>요약</h3>
<ul>
  <li>재귀를 이용한 반복 곱하기</li>
  <li>0! = 1</li>
  <li>int로 사용하면 자료형 크기가 작아 오류</li>
</ul>


<h3>풀이(오류)</h3>
<ul>
  <li>int로 함수 리턴, 오류</li>
</ul>
<pre>
<code>
import java.util.Scanner;


public class Main{
    public static void main(String[] args) throws Exception{
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        System.out.println(fact(n));


    }

    public static int fact(int num){
        if(num <= 0){
            return 1;
        }else{
            return fact(num - 1) * num;
        }
    }
}
</code>
</pre>

<h3>풀이(오류)</h3>
<ul>
  <li>더 큰 정수 자료형 long사용</li>
</ul>
<pre>
<code>
import java.util.Scanner;


public class Main{
    public static void main(String[] args) throws Exception{
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        System.out.println(fact(n));


    }

    public static long fact(int num){
        if(num <= 0){
            return 1;
        }else{
            return fact(num - 1) * num;
        }
    }
}
</code>
</pre>